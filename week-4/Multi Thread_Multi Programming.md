[원문 벨로그 이동하기](https://velog.io/@youngblue/Multi-Thread%EC%99%80-Thread-safe)

# Multi Thread Programing

---


## 프로세스와 스레드 (Process and Thread)
### 프로세스
- 프로세스란 실행 중인 하나의 프로그램을 뜻하며 프로그램을 실행하면 OS로부터 실행에 필요한 자원(메모리)을 할당 받아 프로세스가 된다. 그리고 프로그램을 수행하는 데 필요한 데이터와 메모리 등의 자원 그리고 쓰레드로 구성되어 있으며 프로세스의 자원을 이용해서 작업을 수행하는 것이 바로 쓰레드이다. 하나의 프로그램은 다중 프로세스를 만들기도 한다.

![](https://images.velog.io/images/youngblue/post/163b80a3-5feb-4481-a7d3-b155308631a8/%E1%84%89%E1%85%B3%E1%84%85%E1%85%A6%E1%84%83%E1%85%B3.png)

프로세스는 프로그램과 프로세스 제어블록으로 이루어지고
프로세스는 각각 독립된 메모리 영역을 할당 받는다.


### 쓰레드
- 쓰레드는 프로세스 내에서 각각 Stack만 따로 할당받고 Code, Data, Heap 영역은 공유 한다
- 쓰레드는 한 프로세스 내에서 동작되는 여러 실행의 흐름으로, 프로세스 내의 주소 공간이나 자원들 (힙 공간 등)과 같은 프로세스 내에 쓰레드끼리 공유하면서 실행된다.
- 같은 프로세스 내에 있는 여러 쓰레드들은 힙 공간을 공유한다.

![](https://images.velog.io/images/youngblue/post/3520868e-7b3b-45cd-b0d4-038a71212a1c/%E1%84%8A%E1%85%B3%E1%84%85%E1%85%A6%E1%84%83%E1%85%B3.png)

이때 자바 쓰데드(Java Thread)란 일반 쓰레드와 거의 차이가 없으며, JVM(Java virtual machine)이 운영체제의 역할을 한다.
자바에는 프로세스가 존재하지 않고 쓰레드만 존재하며, 자바 쓰레드는 JVM에 의해 스케쥴되는 실행 단위 코드 블록이다.

### Multi Tasking과 Multi Thread
멀티 태스킹(Multi Tasking)이란 두 가지 이상의 작업을 동시에 처리 하는 것을 말한다.
예를 들어 영화를 보면서 메신저 기능을 동시에 사용을 하거나 음악을 들으며 웹서핑을 하는 것은 병렬로 처리하기 때문에 가능하다. 이는 하나의 프로세스 안에서도 일어날 수 있는데 예를 들어 메신저에서 파일을 주고받으며 채팅을 하는 경우 이는 멀티 쓰레드(Multi Thread) 떄문에 가능하게 된다. 위의 이미지와 같이 프로세스는 프로세스마다 OS(운영체제, Operation System)로부터 할당받은 고유의 메모리를 서로 침범할 수 없지만 멀티 쓰레드(Multi Thread)는 각각의 쓰레드 안에 Stack을 갖고 Code, Data, Heap을 공유하게 되기 때문에 예기치 못한 예외로 인해 프로세스가 종료될 수 있어 조심해야한다.


### start()와 run()
쓰레드를 실행시킬 때 run()이 아닌 start()를 호출한다. 이는 start()와 run()의 차이와 실행되는 과정에 대해 알아보아야 한다.

모든 쓰레드는 독립적인 작업을 수행하기 위해 자신만의 호출스택을 필요로 하기 때문에, 새로운 쓰레드를 생성하고 실행시킬 때마다 새로운 호출스택이 생성되고 쓰레드가 종료되면 작업에 사용된 호출스택은 소멸된다.

![](https://images.velog.io/images/youngblue/post/1b2d4773-d7a2-4729-90a8-27fb44ef35a1/start.png)

1.main 메소드에서 쓰레드의 start()를 호출한다.
2.start()는 새로운 쓰레드를 생성하고, 쓰레드가 작업하는데 사용될 호출스택을 생성한다.
3.새로 생성된 호출스택에 run()이 호출되어, 쓰레드가 독립된 공간에서 작업을 수행한다.
4.이제는 호출스택이 2개이므로 스케줄러가 정한 순서에 의해서 번갈아 가면서 실행된다.


```java
class MyThread extends Thread {
     public void run() {
        throwException();
    }
     public void throwException() {
        try {
            throw new Exception();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
 public class Test {
    public static void main(String[] args) {
        MyThread my = new MyThread();
        my.start();
    }
}

```

1. 먼저 main 쓰레드가 실행되고
2. start()가 실행되면 main 쓰레드는 종료가 되면서 MyThread가 생성 된다.
3. call Stack에 run -> throwException 순서로 쌓이게 된다.

즉, start()를 통해 새로운 쓰레드를 생성하여 main()이 아닌 run()이 실행된다. 
만일 start()가 아닌 run()을 직접 실행시키면 새로운 쓰레드가 생성되어 시작되는 것이 아닌 Overriding된 run()이 호출 된다. 이때 call Stack의 첫번째 메소드는 main이 되고 main에서 Exception이 발생하게 된다.

![](https://images.velog.io/images/youngblue/post/8a310439-25ae-4d49-aea6-b0ad3da057d4/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-31%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.25.14.png)


### 쓰레드 상태
쓰레드 객체를 생성하고, start() 메소드를 호출하면 곧바로 쓰레드가 실행되는 것처럼 보이지만 사실은 실행대기 상태가 된다.
실행 대기 상태에 있는 쓰레드 중에서 쓰레드 스케줄링으로 선택된 쓰레드가 비로소 CPU를 점유하고 run() 메소드를 실행한다.
이 상태를 '실행(Running) 상태'라고 한다. 실행 상태의 쓰레드는 run() 메소드를 모두 실행하기 전에 쓰레드 스케줄링에 의해 다시 실행 대기 상태로 돌아 갈 수 있다. 그리고 실행 대기 상태에 있는 다른 쓰레드가 선택되어 실행 상태가 된다. 
이렇게 쓰레드는 실행 대기 상태와 실행 상태를 번갈아가면서 자신의 run() 메소드를 조금씩 실행한다. 실행 상태에서 run() 메소드가 종료되면, 더 이상 실행할 코드가 없기 때문에 쓰레드의 실행은 멈추게 된다.
이 상태를 '종료 상태' 라고 한다.

![](https://images.velog.io/images/youngblue/post/97524a7f-80d6-4255-a6df-7d106f7ac80e/1.jpeg)

### 쓰레드의 생명 주기
- Runnable (준비 상태)
		- 쓰레드가 실행되기 위한 준비단계
        - CPU를 점유하고 있지 않으며 실행을 하기 위해 대기하고 있는 상태
- Running (실행 상태)
		- CPU를 점유하여 실행하고 있는 상태
        - 우선 순위를 가진 쓰레드가 결정되면 JVM이 자동으로 run() 메소드를 호출하여 Running 상태로 진입
- Dead (종료 상태)
		- Running 상태에서 쓰레드가 모두 실행되고 난 후의 완료 상태 (Done)
- Blocked (지연 상태)
		- CPU 점유권을 상실한 상태로 후에 메소드를 실행시켜 Runnable 상태로 전환
        - wait() 메소드에 의해 Blocked 상태가 된 쓰레드는 notify() 메소드가 호출되면 Runnable 상태로 진입
        - sleep() 메소드에 의해 Blocked 상태가 된 쓰레드는 지정된 시간이 지나면 Runnable 상태가 됨


### 쓰레드 상태 제어하기
멀티 쓰레드 프로그램을 만들기 위해서는 정교한 쓰레드 상태 제어가 필요한데, 상태 제어가 잘못되면 프로그램은 불안정해지고 다운된다. 멀티 쓰레드 프로그래밍이 어려운 이유가 여기에 있다.쓰레드를 잘 사용하면 약이 되지만, 잘못 사용하면 치명적인 프로그램 버그가 되기 때문에 스레드를 정확하게 제어하는 방법을 잘 알고 있어야 한다.

쓰레드 제어를 제대로 하기 위해서는 쓰레드의 상태 변화를 가져오는 메소드들을 파악하고 있어야 한다. 다음 그림은 상태 변화를 가져오는 메소드의 종류를 보여준다.

![](https://images.velog.io/images/youngblue/post/caefd4ee-05b4-4837-ba1e-5ab11d248eb4/2.jpeg)


- sleep() - 주어진 시간 동안 일시정지
- yield() - 다른 쓰레드에게 실행 양보
- join() - 다른 쓰레드의 종료를 기다리기
- wait(), notify(), notifyAll() - 쓰레드 간에 협업
		-	이는 쓰레드가 아닌 Object가 가지고 있는 메소드로 즉 모든 객체가 가지고 있는 메소드다.





<br/>

[참고 : velog - wjdrbs96](https://devlog-wjdrbs96.tistory.com/145)
[참고 : tistory - Namjun Kim](https://ict-nroo.tistory.com/41)
[참고 : tistory - 코딩팩토리](https://coding-factory.tistory.com/279)