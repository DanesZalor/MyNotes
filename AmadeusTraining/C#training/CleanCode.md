# Clean Coding Principles

*Code is like humor. If you have to explain it, it's bad.*

*"Programming is the art of telling another `human` what one wants the computer to do."* -Donald Knuth

*"Any fool can write code that a computer can understand. Good programmers write code that `humans can understand`."* - Martin Fowler

### Reasons to write clean code
1. Writing code is easy, reading code is hard.
2. Technical debt is depressing. Writing sloppy code transfers the burden of understanding it to someone else.
3. Good programmers are often lazy, impatient, and are egotistic. Good laziness is based on putting extra care into the code up front so that it's not so hard to work with later.
4. Sloppy = slow
5. Don't be a verb.

Developers are techincally authors. Great authors are known for writing book sthat tell a clear, compelling story.

# Clean Code Principles
## 1. Right tool for the job
for example, using RegEx to validate an email. RegEx is great but you can validate an email with less work using other tools such as string methods in some logic.

When selecting tools, the risk of picking the wrong tool for the job is the boundaries. HTML can contain JS code and JS can contain HTML. But as much as possible, both should be used accordingly.

## 2. High signal to noise ratio.
 In engineering terms; the level of desired signal to the level of background noise. In the same way, clean code optimizes for signal and strives to remove any noise so that the reader can easily read the logic and understand the intent.

 **Signals** are:
 - Terse - your code should not be excessively wordy.
 - Expressive - it's clear what the code is trying to do.
 - Does one thing - it should have a clear responsibility and should do that one thing well.

**Noises** are:
- High cyclomatic complexity, Huge classes
- Excessive indentation, long methods
- zombie code, repition
- unecessary comments, no whitespace
- poorly named structures, overly verbose

> ### **DRY** Principle: Don't Repeat Yourself
> Duplication Issues:
> 1. Decreases signal to noise ratio
> 2. increases the number of lines of code
>   *"Measuring programming progress by lines of code is like measuring aircraft building progress by weight"* - Bill Gates
> Creates a maintenance problem

## 3. Self-documenting code.
Often times, good code doesn't need any comments.

*"Understanding the original programmer's intent is the most difficult problem"* - Fjelstand & Hamlen 1979

Four core things of self-documenting code:
1. Clear intent
2. Layers of abstraction
3. Format for readability
4. Favor code over comments

# Naming

Try to read this shit:
*"P was very angry with G for insulting her M. G kicked P in the A. He slept on the C"*

### Class Naming
- should be a **Noun**. Classes are things. The name should be as specific as possible. The name should lead the design of Single Responsibility. Avoid generic suffixes.

### Method Naming
name your methods so descriptive that the reader doesn't need to read the method to know what it does.
```C#
bool isValidSubmission()
void SendEmail()
Email Get(int id)
```

**Avoid Side Effects** - methods should either **command** or **query** but not both at the same time 
