One of the most exciting things a business can say to its group of developers is "refactoring". There are many reasons for this I think. 
1. As we build our software we inherently get bugs. Some of these bugs are a bi-product a architectural decision we have made or some shortcuts that were taken. In order to ensure those kinds of bugs never happen again a refactor is in order
2. As a result of various design decisions adding features or making changes is a hassle and requires jumping through various hoops. Refactoring offers the oppertunity to change that. 
3. A developer might have recently joined a dev team and isn't use to the way the new source code is built making development slightly less easy to the way he/she is use to. With some refactoring time they could alter the code base into a way that they are more comfortable with.
4. While reading the blogs and forums a developer comes across a new library or framework that offers a new way of doing things that always promises to speed up development and reduce bugs. Additionally a new programming style (cough cough Functional programming) is coming up everywhere and gives you and your a team a bit of FOMO (Fear of missing out) because all the cool kids look like they are having so much fun over there. 

Whatever the reason, refactoring is always an exciting thing, because it usually involves learning and novelity as well as the promise of a better programming experience once the refactored code is complete. 

I think that, as a development team, getting into a good rythm of developing and refactoring is the key to avoiding code rot and developing in everyones skills. However, we should all be careful about what we expect from refactoring. When you refactor you are improving not bullet proofing your code. Some developers will read a couple of articles that make singeltons sound responsible for all the suffering in the world, and they will think that if they go through potentially great lengths to remove singletons from there code they will never have any bugs again and sales will triple almost immediatly. This is never the case.

The 'R' word has been floating around my current work place recently so I expect we are going to be allocated a good chunk of time to refactor sections of our code base. So in the light of all mentioned above I have endeavored to put together the most effective and responsible refactoring plan that sets reasonable expectations and focuses on improving our code base and not trying to make it immune to all bugs. As a result of all my reading I have decided to put together a mini blog series on some of the main issues that get addressed when refactoring legacy code. I hope this will be a good reference point for other developers to get well rounded view on a few anti-patterns and how to avoid them as well as thoughts around some of the suggested patterns and practices. Here are the links to the topics discussed in this series.

- Singletons, Global state and Dependency Injection
- Command-Query seperation
- Cyclometic complexity
- Coupling
- Mutable Variables
- Architecture
- Language