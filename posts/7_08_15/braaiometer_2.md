<!doctype html>
After a relatively painless first phase of the braaiometer project, I knew that pain would probably be soon on its way. This turned out to be partly true as I hit some barriers and obstacles in this phase of the project. But as always the wealth of knowledgable people online and amazing tools people have built I was able to overcome all the challenges to complete this phase of the project in good time. So, Internet "I salute you". 

[gif]

So quick recap of the phase 2 goals. Firstly, I wanted to add the bluetooth layer to that which I did in the first phase. This means I simply want to take the temperature values from the thermocouple and ship that out to some iOS device using bluetooth. Seems simple right?. Well it is, but the things that slowed me down were directly linked to my inexperience to working with Arduinos and working in C. I will briefly discuss these obstacles and how I overcame them. But first, lets look at the new components I needed for this project. 

[pic of ble shield]

Thanks to the amazing modular design of arduino projects, inorder to add a bluetooth layer to my project, all I had to do was get a bluetooth shield and slam it ontop of my Arduino Uno. I then just plug everything back in at it works as normal. Well not quite, but more on that later. 

The shield I got was from Red Bear Labs, and with it they also provide the library to interface with the shield and some example projects. The even provide an app on the App Store to connect to the shield example projects for testing. This was really helpful and gave me an idea of how to start in no time. 

The first problem I ran into I never quite solved but I am sure was down to some kind of Arduino IDE confiuration or versioning conflict. The problem was that I managed get the sample project to work on an older version of the Arduino IDE but not on the latest version. As a result of my reluctance to run on old software I turned to an up and coming cloud based Arduion IDE called [CodeBender.cc](https://codebender.cc/). Code Bender is an cloud based technology that aims to make Arduino IDE setup a seamless process and allow for easy collaboration between developers. As soon as I shipped my code over, and ran it the Red Bear Labs example project worked as expected. Thank you Code Bender. 

Then, with a basic understanding of the Red Bear Labs Ble library, I ammended the existing braaiometer project to add in the the bluetooth layer. The first problem I faced was that I didn't have enough pins available for both the Thermocouple amplifier and the LCD display because The BLE Shield only gives access to pins 2-10 and requiers you to set one of those pins for the REQN and another for the RDYN. This means I only had 7 pins which meant I had to scrap the LCD display, which is a shame because it was a useful back-up for if the bluetooth decided not to work. 

The next problem was with value types conversion int C. The thermocouple spits out its temperature value as a Double. The BLE library transmits individual bytes represented in the code as [unsigned char]. It took me some time to figure out how to convert a double to an array of [unsigned char]. Thanks to some obscure forum, that I wish I could remember to pay tribute to, I found an function built into Arduino (or AVR if I am not mistaken) that converts a double into a ASCI representation as an array of Char's. The reason that this took longer than I expected because not all standard C and C++ functions are applicable to Arduino code. This seems to be because libraries like stdio.h are not applicable for the arduino due to it running as a microcontroller and not with in an operating system. Anyway, the function was [char * dtostrf(double __val, signed char __width, unsigned char __prec, char * __s)] and can be seen in the code snippet below. 

[code snippet]

The next part was the easy bit. The iOS app. As most of my programming experience has been in iOS land, it was a breath of fresh air to do things that was familiar. To build the iOS interface, I just started with a single page application with one label that represents the temperature send from the BLE shield. Most of the code was around the Core Bluetooth setup. There are various delegate methods that need to be implemented and then the data recieved from the shield has to be converted into something that makes sense and then displayed on the UI. All the code for the app is open source and can be found on [GitHub](https://github.com/va3093/Braaiometer-ios) . 

The last problem that I was stuck on for a while was that my thermocouple was working correctly and my values were converting correctly as well. The "Data transmitted successfully" log was being printed in the serial monitor but nothing was showing up on the app. With some more forums searching someone suggested changing the baud rate which seemed like and obvious problem in this situation. So I changed it from 9600 to the suggested 57600 and that solved the problem. It turns out that 57600 and 115200 is the recommended baud rate for bluetooth which probably explains why it wasn't working for me when my baud rate is 9600. 

After all that everything worked and the end result was an extremely ugly iOS app that showed the last sent temperature from the braaiometer, which I was extremely please about. The next phase will be adding some trouble shooting buttons to the iOS interface and adding some chrome to the UI. So until next time... happy braaing. 




__todo__

~~1. internet salut gif
2. pic of the ble shield
3. code bender link~~
4. unsigned char spans
5. dtostrf inline code block
6. arduino code snippet
~~7. upload iOS app to github and link in blog~~
8. closing gif






__Things to cover__
1. arduino settings -> Codebender
2. bridge between thermocouple and the ble
3. not enough pins
3. baud
4. iOS