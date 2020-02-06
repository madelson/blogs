A common question engineers ask is how they can buy-in for dealing with technical debt. They know that these issues in the codebase are slowing them down, and yet, given ambitious business goals and tight deadlines, no one is excited about the team spending its time refactoring instead of building new features. Here are some thoughts I have on how this problem can be resolved.

## Most of the time, it isn't really technical *debt*

In my experience, the number one way to start dealing with "technical debt" more effectively is to eliminate usage of that term from your team. On my team, we haven't used this term for years, and yet we've been able to consistently maintain strong codebase health. 

"Technical debt" implies technical borrowing: it invokes the idea that we *intentionally* cut some corners to gain velocity early. This can definitely happen (when it does, feel free to use the term!), although in my experience it is fairly rare outside of prototyping. In agile development, we are always targeting the next MVP. If it is truly minimal, then there isn't much can shave off in the name of development speed while still fully delivering against the current set of requirements.

So where does most of our "technical debt" actually come from if not from borrowing? In my mind, there are actually four additional distinct sources:

## 1. Bad code

The first source is simply unintentionally bad code. This code didn't necessarily take less time to develop, but it had bugs or design flaws that could have been caught and fixed during development but were not. If your team is facing this kind of issue, probably the first thing to look at is what your processes are for ensuring quality during development. Do you have a robust code review process? Do you do branch development? Design proposals? Are all developers writing and committing unit tests alongside each product code change? There isn't one magic process that fits every team's style, but if things are slipping through it might be worth trying something new. Investing in skill-building and learning for your team can also help here.

## Unfinished code

The second source is code that was left unfinished. Maybe we never got around to deleting dead code or removing an unused database column. If your team makes a habit of not finishing out features, take a look at your sprint planning and roadmap management process to see why things are falling through the cracks. As an example, on my team we are aggressive about representing all outstanding work in our issue tracker (we use Atlassian JIRA), and we use links between issues to make sure that every bit of work for a feature rolls up to the parent issue representing the overall project. We will not close an issue when there are still child issues that remain unresolved. Typically these finishing issues are very inexpensive, especially when what needs to be done is fresh in everyone's mind. The key is making sure they get included in tasking and estimation.

## Requirements shift

The third source is code that was actually fine when it was written but has not aged well. In some cases this is a scalability/performance issue, but in most cases it is a design issue. When this happens, we need to recognize that the requirements have changed and we need to adapt our code to the new requirements. This is a natural part of agile development. It can seem more expensive than simply bolting things on to the existing design, but the reality is that incremental refactoring is often much cheaper than either bolting on or infrequent massive refactoring. 

If we recognize the need for this kind of continuous code evolution, we can also make smart design choices that will help it along. When possible, we should write new feature code in a way that is easy to delete. We should prefer simple designs that are easy to change rather than complex ones that will make us feel locked in. Most importantly, we should view incremental refactor as part of the development process so that every major build task looks like: (1) make design adjustments, (2) write new code. 

(This post)[https://ronjeffries.com/xprog/articles/refactoring-not-on-the-backlog/] does a great job of illustrating this technique.

## Industry shift

The final source is modernization. This includes things like updating dependencies, updating language/runtime versions, updating tooling, and switching to newer frameworks. Technology keeps marching forward, so the definition of "modern" will keep changing. These should be viewed as technical investments you can make in your codebase to improve developer productivity.

Of course, productivity will only improve if developers are actively working in that part of the codebase. Therefore, it is often helpful to perform such upgrades lazily as you pivot towards doing work in a particular area of the code. Do them as one of the first tasks so that you ensure that most of the development work benefits from the upgrades. This also ensures that you are exercising the codebase and can quickly catch any bugs caused by the upgrade. On my team, we often schedule these for the sprint prior to where major work will start. These upgrades can be intimidating, but most of them are actually very cheap especially if you take them on incrementally.

## Wrap-up

For all of these, keep in mind that there is limited to no value in refactoring or updating code where you are not doing other business-motivated active development. This takes time, might introduce bugs, and in most cases has no upside.

Frequently, "technical debt" gets used as a catch-all phrase for the outcomes of various gaps in the planning or development process. When these fail to account for some aspect of what it takes to build software, inevitably the team gets slowed down. Identify where your gaps are, patch them, and start dealing with these problems incrementally. Your technical debt issues will disappear!

---

## Follow-up questions

### How do you know whether you've achieved a healthy codebase?

My favorite metric for health is developer perception. Reasonably experienced devs recognize the symptoms of working in an unhealthy codebase. Every change takes longer than expected or releases with weird bugs. It is hard to figure out what is going on. Things are misnamed. There are many "gotchas". There is an aura of fear around making certain changes. Tests are flaky, tests fail, or tests pass but we still aren't confident that the code still works. 

Obviously, as devs we need to hold ourselves accountable to focusing on health issues that are actually impacting development and not simply bothering us in an abstract sense.

### How does your team prioritize working on these types of issues?

I think it's a mindset shift. How do you prioritize writing code without bugs? How do you prioritize writing tests? What about adding comments? Chances are you aren't trading off any of these things against "development": they are an essential part of development.

Codebase health must be treated the same way. When you are thinking about how to build the feature, you are also need to be asking how that affects the code already there. Is file X finally going to become too large to manage? Break it up. Does the data model not quite make sense any more? Modify it. Is code going to be duplicated? Introduce an abstraction. These can be explicit tasks, but often they are individual decisions developers are making as they write the feature code. It depends on size and complexity.

In general, we avoid making speculative modifications that don't make the new code "fit" better into the existing codebase. 

### You recommend refactoring incrementally; are there cases where massive refactors are still justified?

There definitely can be, primarily when we are facing a massive requirements shift. Note that "incremental" refactors can still sometimes be large in terms of amount of code changed; what makes them incremental is that we didn't need them before the current feature and after the current feature we do need them.

When facing down a codebase that has been neglected for a long time, my preference is to just start applying the policy of "fix as we go" immediately rather than doing a massive refactor upfront. My team has taken this approach many times and found that it has worked well. The reality is that often much of the code we might consider cleaning up will become obsoleted for other reasons long before we'd actually need to make changes to it. By doing everything "just in time", we make sure that every investment has a real payoff.
