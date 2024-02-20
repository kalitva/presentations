### Refactoring by Martin Fowler

**Refactoring** (noun): a change made to the internal structure of software to make it easier to understand and cheaper to modify without changing its observable behavior.

**Refactoring** (verb): to restructure software by applying a series of refactorings without changing its observable behavior

Over the years, many people in the industry have taken to use “refactoring” to mean any kind of code cleanup—but the definitions above point to a particular approach to cleaning up code. Refactoring is all about applying small behavior­-preserving steps and making a big change by stringing together a sequence of these behavior­-preserving steps. Each individual refactoring is either pretty small itself or a combination of small steps. As a result, when I’m refactoring, my code doesn’t spend much time in a broken state, allowing me to stop at any moment even if I haven’t finished.

*If someone says their code was broken for a couple of days while they are refactoring, you can be pretty sure they were not refactoring*

#### When Should We Refactor?

- ##### The Rule of Three

The first time you do something, you just do it. The second time you do something similar, you wince at the duplication, but you do the duplicate thing anyway. The third time you do something similar, you refactor

- ##### Preparatory Refactoring—Making It Easier to Add a Feature

The best time to refactor is just before I need to add a new feature to the code base. As I do this, I look at the existing code and, often, see that if it were structured a little differently, my work would be much easier...

- ##### Comprehension Refactoring: Making Code Easier to Understand

Before I can change some code, I need to understand what it does [ ... ] Whenever I have to think to understand what the code is doing, I ask myself if I can refactor the code to make that understanding more immediately apparent. [ ... ] At that point I have some understanding in my head, but my head isn’t a very good record of such details. As Ward Cunningham puts it, by refactoring I move the understanding from my head into the code itself. I then test that understanding by running the software to see if it still works. If I move my understanding into the code, it will be preserved longer and be visible to my colleagues.

- ##### Litter-Pickup Refactoring 

A variation of comprehension refactoring is when I understand what the code is doing, but realize that it’s doing it badly. [ ... ] I don’t want to spend a lot of time distracted from the task I’m currently doing, but I also don’t want to leave the trash lying around and getting in the way of future changes. If it’s easy to change, I’ll do it right away. If it’s a bit more effort to fix, I might make a note of it and fix it when I’m done with my immediate task.

- ##### Planned and Opportunistic Refactoring 

I don’t set aside time at the beginning to spend on refactoring—instead, I do refactoring as part of adding a feature or fixing a bug. *It’s part of my natural flow of programming*. Whether I’m adding a feature or fixing a bug, refactoring helps me do the immediate task and also sets me up to make future work easier. This is an important point that’s frequently missed. *Refactoring isn’t an activity that’s separated from programming*—any more than you set aside time to write if statements. I don’t put time on my plans to do refactoring; most refactoring happens while I’m doing other things.

- ##### Long-Term Refactoring

Most refactoring can be completed within a few minutes—hours at most. But there are some larger refactoring efforts that can take a team weeks to complete [ ... ] 

Even in such cases, I’m reluctant to have a team do dedicated refactoring. Often, a useful strategy is to agree to gradually work on the problem over the course of the next few weeks. Whenever anyone goes near any code that’s in the refactoring zone, they move it a little way in the direction they want to improve. This takes advantage of the fact that *refactoring doesn’t break the code—each small change leaves everything in a still­working state*. To change from one library to another, start by introducing a new abstraction that can act as an interface to either library. Once the calling code uses this abstraction, it’s much easier to switch one library for another. (This tactic is called Branch By Abstraction.)

- ##### Refactoring in a Code Review

#### When Should I Not Refactor?

It may sound like I always recommend refactoring—but there are cases when it’s not worthwhile.

If I run across code that is a mess, but I don’t need to modify it, then I don’t need to refactor it. Some ugly code that I can treat as an API may remain ugly. It’s only when I need to understand how it works that refactoring gives me any benefit.

Another case is when it’s easier to rewrite it than to refactor it. This is a tricky decision. Often, I can’t tell how easy it is to refactor some code unless I spend some time trying and thus get a sense of how difficult it is. The decision to refactor or rewrite requires good judgment and experience, and I can’t really boil it down into a piece of simple advice.
