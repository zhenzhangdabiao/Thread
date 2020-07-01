# Thread

### 使用方法

- 实现 Runnable 接口

  ```java
  public class RunnableTest implements Runnable {
      @Override
      public void run() {
          // ...
      }
  }
  ```

  ```java
  public static void main(String[] args) {
      RunnableTest instance = new RunnableTest();
      Thread thread = new Thread(instance);
      thread.start();
  }
  ```

  不需要返回值时，最简单的实现方式

- 实现 Callable 接口

  ```java
  public class CallableTest implements Callable<Integer> {
      public Integer call() {
          return 123;
      }
  }
  ```

  ```java
  public static void callableTest(){
          try {
              CallableTest ct = new CallableTest();
              FutureTask<Integer> ft = new FutureTask<>(ct);
              Thread thread = new Thread(ft);
              thread.start();
              System.out.println(ft.get());
          } catch (InterruptedException e) {
              e.printStackTrace();
          } catch (ExecutionException e) {
              e.printStackTrace();
          }
  }
  ```

  实现 Callable 接口能获取线程执行返回值，get()是阻塞的，保证线程执行完成

- 继承 Thread 类

  ```java
  public class ThreadTest extends Thread {
      public void run() {
          // ...
      }
  }
  ```

  ```java
  public static void main(String[] args) {
      ThreadTest tt = new ThreadTest();
      tt.start();
  }
  ```

  基本不使用

### 线程生命周期管理

- sleep（）

  Thread.sleep(millisec) 会休眠当前正在执行的线程，不会释放线程占有的锁

- yield()

  标记当前线程完成了生命周期中最重要的部分，可以切换其他线程执行。该方法只是对线程调度器的建议。

- Daemon

  守护线程，在线程启动前调用线程的setDaemon()方法，将线程设置为守护线程，所有非守护线程结束时，程序终止，同时所有守护线程都将结束。

- interrupt()

  线程中断方法，线程在I/O阻塞和interrupt阻塞时无法中断，此时调用interrupt()方法，线程会一直阻塞，在获得竞争资源后执行中断方法






