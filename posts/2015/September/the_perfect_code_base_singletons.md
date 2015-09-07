#Singletons, Global state and Dependency Injection
I am starting with singletons because the degree of public shaming that singletons have gotten in the last 3 or so years has been way way over the top. And I get it, there are a host of reasons why singletons can cause havoc in your code but there are a lot of other things that are more prolific and don't nearly get the same amount of bad press. I was listening to a podcast recently where singeltons came up and the host was like "Don't get me started on singletons or it will take over the show". So in this section I want to break down why singeltons are bad and when they are not so bad. This will set the stage to talk about the bigger issue of global state in the next post and then look at the main way to tackle global state which is dependency injection. 

So why are Singletons bad. Here are the main reasons they are not advised.
1. __Hidden Coupling__: If a person went into a class and wanted to know what the dependencies of the class they you would probably first look at the constructor method and then maybe on the the instance variables declared for that class. If your code was making use of singletons then it will be easy to miss this dependency as it will be hidden in your code somewhere. This creates what is called __Hidden Coupling__ which is what happens if a person has to read every line of code to find out what dependencies a class has. 
2. __Untestability__: Singeltons makes it very difficult to test code without performing a bunch of hacks. This is probably the most prominent pain point you will experience if you are working with a code base that uses singletons. When it comes to testing code, the easiest things to test are things that are loosely coupled and easy to mock. The use of singletons makes both of those things difficult. One of the reasons people use singletons is for easy access because the particular class is used a lot throughout the code base. This means that singletons usually are very highly coupled. They are also very difficult to mock. It is very difficult to get out of using the actual singleton object (as oppose to a mocked object) when testing a class that uses a singleton . This makes tests much less reliable than tests that use mocked objects to test some particular functionality. Another reason why testing is difficult with singletons is that they carry state along with them for the duration of the program. This means that if two unit tests require the same singleton there is a chance that the order in which the unit tests run could effect the outcome of the unit test because of the way that the previous unit test altered the singleton. This is a big no no in unit test land. 
3. __Global state__: The last main reason why Singletons are bad is that they increase the amount of global state in your application. In theory, the less state you have in an application at any one time the less complexity there is at that time and the lower the chance of unexpected behaviour. This is theoretically true but doesn't always lead to simple code. Just because there is less state in your application doesn't mean that you can't make a complicated mess with the state that you do have. It seems sensible, though, to stick with the theory that seems intangible in development but almost always will pay off down the road. So singletons are objects that can be accessed anywhere so they are in a sense a global variable. That makes all the variables that are owned by the singleton global variables along with the variables owned by the variables and so on. As you can see the introduction of one singleton can increase the total global state of your application significantly. 

So those are the main reasons why singletons are bad. allow me a few sentences to respond on behalf of singletons who have got way more punishment than they deserve. I am currently working in iOS land where it is not uncommon to see the use of singletons. What is uncommon in iOS land is the use of unit tests. So when someone is bashing Singeltons I always ask them if they write unit tests. In my field, the answer is almost always 'No'. So why do they care if they are using singletons. The only tangible practical down fall of singletons is the difficulty it causes when testing, so if you aren't testing your code save your huffing and puffing about singletons, acknowledge that they are unadvised and move one. Use your huffing and puffing on something else like documenting your code, writing shorter methods, using constants etc. Leave poor singletons along. Points 1 and 3 are valid but slightly abstract and I wouldn't loose any sleep over it. 

So before I move on from singletons let me summarise all I have said above.

_If you are thinking about using a singleton - don't. If you are using them, don't stress, make a plan to remove them if it is convenient. If you are a singleton hater - get a life because they are not the root of all evil_


















