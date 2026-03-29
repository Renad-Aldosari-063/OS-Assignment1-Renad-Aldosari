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

### Example 1: [Name of application/scenario]

**Description**: 
[Describe the real-world scenario or application]

**Why Round-Robin works well here**: 
[Explain why Round-Robin scheduling is suitable. Consider fairness, responsiveness, predictability, etc.]

### Example 2: [Name of application/scenario]

**Description**: 
[Describe the real-world scenario or application]

**Why Round-Robin works well here**: 
[Explain why Round-Robin scheduling is suitable. Consider fairness, responsiveness, predictability, etc.]

---

## Summary

**Key concepts I understood through these questions:**
1. 
2. 
3. 

**Concepts I need to study more:**
1. 
2. 
