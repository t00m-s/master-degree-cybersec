# Introduction to side channels
## How does a CPU work?
We summarize how CPUs work.
CPUs typically do operations by splitting them in subparts, like:
- Fetching
- Decoding
- Executing
 CPUs need to be fast. So engineers came up with lots of solutions to speed up them, including:
 - Pipeline
 - Cache
### Cache
A cache is a hierarchy of memories that goes from [small, fast] to [big, slow].
A cache stores data that is accessed frequently, to make it accessble faster.
Usually they are referred to layers:
-  CPU: it has registers. Access to registers is the fastest, but a CPU has very few registers (on 64 bit CPUs there are 64 registers, each of them that stores 64 bits).
- L1
- L2
- L3
- DRAM: the memory of the computer. Slow but very big, typically it has lots of GB (like 16 or 32).
- Caches are needed because they increase a lot the speed of a CPU.
  CPUs events scaled (https://sgros.blogspot.com/2014/08/memory-access-latencies.html)  
### Speculation
Caches are fast only if data is already there, otherwise we need to wait for the DRAM.
Speculation is a feature of CPUs in which they try to "predict" on a branch what will the result be.
Take the following example:
```c
if (x < 10) {
// code if true
} else {
// code if false
}
```        
If x is not in cache, the CPU needs to fetch it from the memory, which is really slow.
So CPUs try to predict the result of the branch: they calculate the most probable branch the if will take and execute if before knowing the actual result.
If it was correct, the execution is already done. If it wasn't, the CPU does a rollback and executes the other branch.
This feature is done by the branch predictor of the CPU.
The branch predictor does it's computation by observing the behavior of the CPU.     ```
```c
for (...) {
	if () {
		foo();
	} else {
		bar()
	}
}
```
What are side channels?
If an attacker observes the execution of a program, they can learn some information.
The side channel is any observable side effect of computation that an attacker could measure and possibly influence.
The most simple side channel is time based: an attacker could try to discover a secret key for example by measuring the time while the program compares a key with the correct one.
In fact, cryptographic-safe functions usually have a constant-time execution. ## Flush+Reload
- https://www.usenix.org/conference/usenixsecurity14/technical-sessions/presentation/yarom
- Flush+Reload exploits caches to learnsecrets.
- Take an attacker that can measure the execution time of a program, choose a victim.
### Flush phase
Find a code gadget in the victim
For example:
```
N = //secret
...
y = A[N * 512];
```
Here, access to A is based on a secret value.
Make sure that the attacker and the victim share memory pages
You flush A from the cache.      
All of these values are not in cache.
```
A[0 * 512]
A[1 * 512]
A[2 * 512]
A[  ...  ]
A[N * 512] <-- access based on secret
A[  ...  ]
A[A_sz -1]
```
- ### Reload phase
     ### Mitigating
     Mitigating can be hard.
     Software-based:
	     - Avoid secret-dependent memory accesses
	     - Disable page sharing/de-duplication
	     - Limit access to high-resolution timers
     Hardware-based:
     ## Spectre v1
     Spectre is an attack exploiting speculative execution to leak secrets.
     The attacker mistrains the branch predictor by poisoning the Pattern History Table (PHT).
     How? For example:
     The attacker looks for a piece of "vulnerable code" (code gadget) including a condition.
     Runs that code multiple time with an input so that the condition always holds.
     This is to train the  branch predictor to always "predict" that the condition holds.
## Mitigating Spectre
 CPUs provide instructions to disable speculation.
For instance, on x86_64 there is the instruction lfence
In [[C]] we could write the following code to prevent speculation:
```c
if (x < A_sz) {
	__asm__("lfence");
	y = B[A[x] * 512];
} else {
	__asm__("lfence");
}
```
The good thing is that it works as mitigation (except it can be skipped with Spectre v1.1).
The bad thing is that it's highly inefficient (speculation improves execution speed a lot) and requires re-compilation.
Compilers like Microsoft MSVC use static analysis to decide where fences should go.
### Speculative Load Hardening
Speculative Load Hardening (SLH) is a sophisticated way to prevent speculation exploitation.
Based on this idea:
- It may be more efficient to introduce an artificial data dependency between the condition of a jump and the pointer
```c
uint MASK = ALL_ONES;
if (cond) {
	mask = !cond ? ALL_ZEROS: mask;
	// ...
	Y = B[(A[x]*512) & mask]; // do thing
}
else {
	mask = cond ? ALL_ZEROS: mask;
}
```
- The good:
  - Still works
  - More efficient than spectre
- The bad:
  - Still needs recompilation