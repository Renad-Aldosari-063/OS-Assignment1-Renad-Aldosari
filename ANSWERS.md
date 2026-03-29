# Assignment Questions

## Instructions
Answer all 4 questions with detailed explanations. Each answer should be **3-5 sentences minimum** and demonstrate your understanding of the concepts.

---

## Question 1: Thread vs Process

**Question**: Explain the difference between a **thread** and a **process**. Why did we use threads in this assignment instead of creating separate processes?

**Your Answer:**

[A process is an independent program with its own memory space and system resources, while a thread is a smaller unit of execution inside a process. Threads within the same process share memory and resources, but each thread still has its own execution path. In general, threads are lighter than processes because they require less creation overhead and allow faster communication through shared data. In this assignment, we used threads because the scheduler simulation needs multiple execution units inside one program, which is why the code creates each process as a Runnable object and then wraps it in a Thread in the addProcessToQueue method. This design makes it easier to manage the ready queue, connect each thread to its process through processMap, and control execution using methods such as start, join(), and sleep (). Compared with separate processes, threads were more suitable for this simulation because they are more efficient and easier to coordinate within SchedulerSimulation.java.]

---

## Question 2: Ready Queue Behavior

**Question**: In Round-Robin scheduling, what happens when a process doesn't finish within its time quantum? Explain using an example from your program output.

**Your Answer:**

[In Round-Robin scheduling, if a process does not finish within its time quantum, it is paused and moved back to the ready queue to wait for another turn. This ensures that all processes get a fair chance to execute without one process using the CPU for too long.]

Example from my output:
```
P1 executing quantum [4000ms]
P1 completed quantum 4000ms → Overall progress: 63%
Remaining time: 2259ms
P1 yields CPU for context switch
P1 (Priority: 5) added to ready queue
```

**Explanation of example:**
[In this example, process P1 runs for one time quantum but does not finish because it still has remaining time. As a result, it yields the CPU and is placed back into the ready queue. Later, it will be scheduled again after other processes get their turn. This behavior is important for fairness because it prevents one process from dominating the CPU and allows all processes to make progress step by step.]

---

## Question 3: Thread States

**Question**: A thread can be in different states: **New**, **Runnable**, **Running**, **Waiting**, **Terminated**. Walk through these states for one process (P1) from your simulation.

**Your Answer:**

[A thread goes through several states during its lifecycle. In this simulation, we can trace the lifecycle of process P1 using the code in SchedulerSimulation.java.]

1. **New**: P1 is in the New state when the Process object is created using the constructor:
Process process = new Process("P1", burstTime, timeQuantum, priority);
At this point, the thread has not started yet.

2. **Runnable**: P1 becomes Runnable after it is wrapped inside a Thread object and added to the ready queue using:
Thread thread = new Thread(process);
and then:
processQueue.add(thread);
Here, the thread is ready to run but waiting for CPU scheduling.

3. **Running**: P1 enters the Running state when the scheduler selects it and calls:
currentThread.start();
This triggers the run() method where the process executes its time quantum.

4. **Waiting**: P1 goes into a Waiting (or blocked) state during execution when:
Thread.sleep(stepTime);
is called inside the run() method to simulate execution delay. Also, the main thread waits using:
currentThread.join();
until the current process finishes its time slice.

5. **Terminated**: P1 reaches the Terminated state when its remainingTime becomes zero:
if (remainingTime <= 0)
At this point, the process finishes execution and exits the lifecycle.

---

## Question 4: Real-World Applications

**Question**: Give **TWO** real-world examples where Round-Robin scheduling with threads would be useful. Explain why this scheduling algorithm works well for those scenarios.

**Your Answer:**

### Example 1: Web Server

**Description**: 
A web server can use multiple threads to handle requests from different users at the same time. Each request can be treated like a separate task that needs CPU time to process data and send a response. If many requests arrive together, the server needs a fair way to share CPU time between them.

**Why Round-Robin works well here**: 
 Round-Robin scheduling works well in this case because it gives each thread a time quantum and prevents one request from using the CPU for too long. This improves fairness and keeps the system responsive when many users are active. It is similar to this assignment, where each process gets a turn, and if it does not finish, it goes back to the ready queue for another round.

### Example 2: Game Engine

**Description**: 
 A game engine can use multiple threads for tasks such as input handling, physics updates, sound, and background loading. These tasks need to run repeatedly and share CPU time so that the game continues to respond smoothly. If one task takes too much time, it can affect the player’s experience.

**Why Round-Robin works well here**: 
Round-Robin is useful here because it allows each thread to run for a short time before switching to another one. This supports responsiveness and predictability, which are important in interactive applications like games. The same concept appears in this assignment, where context switches and time quantum help multiple processes make progress without one process blocking the others.

---

## Summary

**Key concepts I understood through these questions:**
1. 
2. 
3. 

**Concepts I need to study more:**
1. 
2. 
