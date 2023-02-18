So, breaking it down our mission statement of 
> How can we have codebases that are easy to maintain, extend and still have the ability to increase performance later when those scaling headaches come.
> 
In order of priority:
- **Maintenance**:
  - How easy it is to debug a problem. If you get a critical production error at night, how fast can you understand what broke and why?
  - How quickly can you understand what another engineer has done without calling them up? Or otherwise, how much can you understand by yourself before talking to them?
- **Extensibility**
  - How easily can you modify or add new functionality to existing functionality? How much of the existing stuff has to change now to accommodate your new stuff?
  - How fast can you do this? It may be easy to do, but is it repetitive and prone to human errors & silly mistakes?
- **Performance**
  - How fast can your system run? Here, we are not talking about some specific part or block of the code. Rather, here we mean the speed of execution of a workflow (i.e flowchart).
  - Similarly, how much memory does this take? 
  - So to put it more generically, how much hardware resources will your engineering take?

Here in this codebase and this journey, we will see a very particular style of writing codebases (and NOT code), which can help us come closer to achieving these goals.  
But before we do that, **please** go through the [vocabulary](vocabulary/) once so that we have the same understanding of terms we use throughout this journey.
