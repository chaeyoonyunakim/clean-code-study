# Chapter 13 : Concurrency

날짜: 2023년 7월 9일 → 2023년 7월 22일
요약: _Concurrency_, as a decoupling strategy, helps us separate the "what" from the "when" of tasks (동시성은 "무엇"과 "언제"를 분리하는 전략이다).

## Why Concurrency? 동시성이 필요한 이유

- _"In single-threaded applications what and when are so strongly coupled that the
  state of the entire application can often be determined by looking at the stack backtrace"_ 스레드가 하나인 프로그램은 "무엇"과 "언제"가 서로 밀접하다. e.g., waiting time at Web sockets for I/O completion, the system’s response time if it handles users sequentially in one second
- "무엇"과 "언제"를 분리하면 애플리케이션 구조와 효율이 극적으로 나아진다. e.g., The standard "Servlet" model of Web applications is decoupled from all other servlet executions and doesn't need to manage all incoming requests.

### Myths and Misconceptions 동시성에 관한 미신과 오해

- 동시성은 **항상(X)** 성능을 높여준다; always -> sometimes, 여러 프로세서가 동시에 처리할 독립적인 계산이 많은 경우에만 성능이 높아진다.
- 동시성을 구현해도 설계는 변하지 **않는다(X)**; 단일 스레드와 다중 스레드 시스템은 설계가 다르고, 동시성을 위해 무엇과 언제를 분리하게 되면 시스템 구조가 크게 달라진다.
- Understanding concurrency issues is **not(X)** important when working with a container such as a Web or EJB container.

### Challenges

- share an instance of X between two treads -> if many possible paths, then _some of those paths generate incorrect results_.

## Concurrency Defense Principles

### Single Responsibility Principle (SRP)

- _a method/class/component should have a single reason to change_
- _Concurrency-related code has its own life cylce of development, change, tunning, and challenges_

### Corollary 추론결과: Limit the Scope of Data

- the more places shared data can get updated -> 한군데 (이상) 수정을 잊어버리고 broken code가 되거나, Don't Repeat Yourself (DRY) 원칙 위배, fail지점 진단을 어렵게 하고 debugging challenge

### Corollary: Use Copies of Data

- 처음부터 데이터를 공유하지 않게 하면 데이터 공유 지점으로 발생하는 문제들을 피할 수 있다.

### Corollary: Threads Should Be as Independent as Possible

- 비동기(asynchronous) 최고!

## Know Your Library

### Java 5: Thread-Safe Collections

- _Review the classes available to you._ Java의 경우 java.util.concurrent, java.util.concurrent.atomic, java.util.concurrent.locks가 advanced concurrency design을 지원할 수 있다.

## Know Your Execution Models

실행 모델 정의를 알아야 concurrent programming에 사용되는 excution models을 이야기할 수 있다.

1. Bound Resources: refer to _fixed-sized or limited resources utilized in a concurrent environment_, such as database connections and read/write buffers with a predetermined size.
2. Mutual Exclusion: ensures that _shared data or resources can only be accessed by one thread at a time_.
3. Starvation 결핍: occurs when _one thread or a group of threads is prevented from making progress for a long time_, or indefinitely, as certain threads with higher priority continually access resources, potentially excluding longer-running threads from accessing them.
4. Deadlock: refers to a situation in which _two or more threads are waiting for each other_ to release resources they need, resulting in a state where none of the threads can proceed and are effectively stuck in a cycle of resource dependency
5. Livelock: 무한히 긴 시간동안 프로그레스를 만들지 않고 계속 진행하는 상태. ChatGPT describes a scenario where threads are locked in a repetitive pattern, each attempting to progress, but being hindered by other threads, leading to prolonged or eternal non-productive activity due to resonance and resource contention.

### Producer-Consumer

- One or more producer threads create work and place it in a bound resource queue, while one or more consumer threads acquire work from the queue and complete it, requiring coordination through signaling, where producers signal when the queue is not empty, and consumers signal when the queue is not full, potentially waiting for notifications to proceed.

### Readers-Writers

- It deals with managing a shared resource used primarily for reading but occasionally updated by writers, where balancing throughput and avoiding starvation requires a careful coordination strategy between readers and writers to ensure correct operation and reasonable throughput without causing concurrency update issues.

### Dining Philosophers

- It represents a scenario where multiple threads (philosophers) sit around a circular table, each needing two shared resources (forks) to eat spaghetti, leading to potential issues like deadlock, livelock, throughput, and efficiency degradation in systems with resource competition, making it crucial to study and understand these algorithms to be prepared for concurrent problem-solving.

### Beware Dependencies Between Synchronized Methods

- Dependencies between synchronized methods cause subtle bugs in concurrent code 동기화된 메서드 간의 종속성으로 인해 동시 코드에서 미묘한 버그가 발생합니다. (자바 예제 생략)

### Keep Synchronized Sections Small ♻

### Writing Correct Shut-Down Code Is Hard

- _Think about shut-down early and get it working early. It’s going to
  take longer than you expect. Review existing algorithms because this is probably harder
  than you think._

### Testing Threaded Code

- _Testing does not guarantee correctness. However, good testing can minimize risk._

1. Treat Spurious Failures as Candidate Threading Issues: Threaded code can lead to unexpected failures. Assuming one-offs do not exist is essential to avoid building code on potentially faulty approaches resulting from interactions between threads and other code.
2. Get Your Nonthreaded Code Working First: _Make sure code works outside
   of its use in threads._
3. Make Your Threaded Code Pluggable: _so that you can run it in various configurations._
4. Make Your Threaded Code Tunable
5. Run with More Threads Than Processors: Make system switches less tasks swap.
6. Run on Different Platforms
7. Instrument Your Code to Try and Force Failures: _only a very few pathways out of the many thousands of possible pathways through a vulnerable section actually fail_ 문제를 노출하는 테스트 케이스를 작성하고, 실패하면 원인을 추적하라.
   7.1) Hand-coded: _Run in different orderings by adding calls to methods like Object.wait(), Object.sleep(), Object.yield() and Object.priority()_ Wait, Yield, Sleep 등의 보조 코드를 넣어 강제로 실패를 일으키게 해보라.
   7.2) Automated: (이해하지 못함)

## Conclusion

- The Clean code approach helps in writing concurrent code by reducing subtle and infrequent failures!
