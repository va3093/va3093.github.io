One of the most exciting things a business can say to its group of developers is "refactoring". There are many reasons for this I think. 
1. As we build our software we inherently get bugs. Some of these bugs are a bi-product a architectural decision we have made or some shortcuts that were taken. In order to ensure those kinds of bugs never happen again a refactor is in order
2. As a result of various design decisions adding features or making changes is a hassle and requires jumping through various hoops. Refactoring offers the oppertunity to change that. 
3. A developer might have recently joined a dev team and isn't use to the way the new source code is built making development slightly less easy to the way he/she is use to. With some refactoring time they could alter the code base into a way that they are more comfortable with.
4. While reading the blogs and forums a developer comes across a new library or framework that offers a new way of doing things that always promises to speed up development and reduce bugs. Additionally a new programming style (cough cough Functional programming) is coming up everywhere and gives you and your a team a bit of FOMO (Fear of missing out) because all the cool kids look like they are having so much fun over there. 

Whatever the reason refactoring is always an exciting thing, because it usually involves learning and novelity as well as the promise of a better programming experience once the refactored code is complete. 

I think that, as a development team, getting into a good rythm of developing and refactoring is the key to avoiding code rot and developing in everyones skills. However, we should all be careful about what we expect from refactoring. When you refactor you are improving not bullet proofing your code. Some developers will read a couple of articles that make singeltons sound responsible for all the suffering in the world, and they will think that if they go through potentially great lengths to remove singletons from there code they will never have any bugs again and sales will triple almost immediatly. This is never the case.

The 'R' word has been floating around my current work place recently so I expect we are going to be allocated a good chunk of time to refactor sections of our code base. So in the light of all mentioned above I have endeavored to put together the most effective and responsible refactoring plan that sets reasonable expectations and focuses on improving our code base and not trying to make it immune to all bugs. This blog posts contains some of comments on various refactoring options and my thoughts about them. I hope this will be a good reference point for other developers to get well rounded view on a few anti-patterns and how to avoid them as well as thoughts around some of the suggested patterns and practices. Because of the mammoth nature of this post here are some quick links to take you to the varous sections of this post.

Singletons, Global state and Dependency Injection
Command-Query seperation
Cyclometic complexity
Coupling
Mutable Variables
Architecture
Language

#Singletons, Global state and Dependency Injection
I am starting with singletons because the degree of public shaming that singletons have gotten in the last 3 or so years has been way way over the top. And I get it, there are a host of reasons why singletons can cause havoc in your code but there are a lot of other things that are more prolific and don't nearly get the same amount of bad press. I was listening to a podcast recently where singeltons came up and the host was like "Don't get me started on singletons or it will take over the show". So in this section I want to break down why singeltons are bad and when they are not so bad. I then want to talk about the bigger issue of global state and then look at the main way to tackle global state which is dependency injection. 

So why are Singletons bad. Here are the main reasons they are not advised.
1. __Hidden Coupling__: If a person went into a class and wanted to know what the dependencies of the class are you would probably first look at the constructor method and then maybe on the the instance variables declared for that class. If your code was making use of singletons then it will be easy to miss this dependency as it will be hidden in your code somewhere. This creates what is called __Hidden Coupling__ which is what happens if a person has to read every line of code to find out what dependencies a class has. 
2. __Untestability__: Singeltons makes it very difficult to test code without performing a bunch of hacks. This is probably the most prominent pain point you will experience if you are working with a code base that uses singletons. When it comes to testing code, the easiest things to test are things that are loosely coupled and easy to mock. The use of singletons makes both of those things difficult. One of the reasons people use singletons is for easy access because the particular class is used a lot throughout the code base. This means that singletons usually are very highly coupled. They are also very difficult to mock. To use a singleton in a test it is very difficult to get out of using the actual singleton object. This makes tests much less reliable than tests that use mocked objects to test some particular functionality. Another reason why testing is difficult with singletons is that they carry state along with for the duration of the program. This means that if two unit tests require the same singleton there is a chance that the order in which the unit tests run could effect the outcome of the unit test because of the way that the previous unit test altered the singleton. This is a big no no in unit test land. 
3. __Global state__: The last main reason why Singletons are bad is that they increase the amount of global state in your application. In theory, the less state you have in an application at any one time the less complexity there is at that time and the lower the chance of unexpected behaviour. This is theoretically true but doesn't always lead to uncomplex code because just because there is less state in your application doesn't mean that you can't make a complicated mess with the state that you do have. It seems sensible though to stick with the theory that seems intangible in development but almost always will pay of down the road. So singletons are objects that can be accessed anywhere so they are in a sense a global variable. That makes all the variables that are owned by the singleton global variables along with the variables owned by the variables and so on. As you can see the introduction of one singleton can increase the total global state of your application significantly. 
4. __Mutable state__

So those are the main reasons why singletons are bad. allow me a few sentences to respond on behalf of singletons who have got way more punishment than they deserve. I am currently working in iOS land where it is not uncommon to see the use of singletons. What is uncommon in iOS land is the use of unit tests. So when someone is bashing Singeltons I always ask them if they write unit tests. In my field, the answer is almost always 'No'. So why do they care if they are using singletons. The only tangible practical down fall of singletons is the difficulty it causes when testing, so if you aren't testing your code save your huffing and puffing about singletons, acknowledge that they are unadvised and move one. Use your huffing and puffing on something else like documenting your code, writing shorter methods, using constants etc. Leave poor singletons along. Points 1 and 3 are valid but slightly abstract and I wouldn't loose any sleep over it. 



So before I move on from singletons let me summarise all I have said above.

_If you are thinking about using a singleton - don't. If you are using them, don't stress, make a plan to remove them if it is convenient. If you are a singleton hater - get a life because they are not the root of all evil_


















