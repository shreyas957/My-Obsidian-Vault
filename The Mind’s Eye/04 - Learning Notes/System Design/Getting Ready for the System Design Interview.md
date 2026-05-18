2025-09-12 12:30

Status: [[complete]]

Tags: [[System Design]]


# Getting Ready for the System Design Interview

## 1. How do we tackle a design question?
Design questions are open ended, and they’re intentionally vague to start with. Such vagueness mimics the reality of modern day business.

Interviewers often ask about a well-known problem,—for example, designing WhatsApp. Now, a real WhatsApp application has numerous features, and including all of them as requirements for our WhatsApp clone might not be a wise idea due to the following reasons:
- First, we’ll have limited time during the interview.
- Second, working with some core functionalities of the system should be enough to exhibit our problem-solving skills.
We can tell the interviewer that there are many other things that a real WhatsApp does that we don’t intend to include in our design. If the interviewer has any objections, we can change our plan of action accordingly.

Here are some best practices that we should follow during a System Design interview:
```uml
Solidify the requirements --> Scope the problem --> Engage the interviewer 
```

```text
Ask refining question --> handle the data --> discuss the components --> discuss tradeoffs
```
## 2. Present High-Level Design(HLD):
At a high level, components could be frontend, load balancers, caches, data processing, and so on. The System Design explains how these components fit together.
An architectural design often represents components as boxes. The arrows between these boxes represent who talks to whom and how the boxes or components fit together collectively.

## 3. Possible questions for every System Design interview
System Design interviews often include questions related to how a design might evolve over time as some aspect of the system increases by some order of magnitude—for example, the number of users, the number of queries per second, and so on. It’s commonly believed in the systems community that when some aspect of the system increases by a factor of ten or more, the same design might not hold and might require change.

Designing and operating a bigger system requires careful thinking because designs often don’t linearly scale with increasing demands on the system.


```text
Another question in a System Design interview might be related to why we don’t design a system that’s already capable of handling more work than necessary or predicted.
--> 
Over-provisioning a system upfront leads to unnecessary complexity and cost. In System Design, we aim for a scalable architecture, building a system that can handle current loads efficiently while making it easy to scale horizontally or vertically as demand grows. Designing for hypothetical peak load from day one wastes resources and can result in over-engineered solutions that are harder to maintain and evolve.

```
## Points to know: 
1. Fundamental concepts in System Design interview
2. Fundamentals of distributed system    
3. The architecture of large-scale web applications
4. Design of large-scale distributed systems
![[fundamentals of sys design.png]]
And many more things......



# References
