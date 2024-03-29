# andaaza  

## **initial ideas**  
we started by ideating about the concept of **measuring** in a post scientific way from a hyperpersonal perspective. We speculated and questioned each other:  
- when does measuring stop facilitating and start preventing a process?  
- are the usual measuring units opposite to replicability?  
- why do we measure things?  ..to save time instead of doing everything by trial & error, capitalism, control outcome prediction.  

other fields we wanted to explore were **storytelling**, the strict binary distinction between the 'positive' and the 'negative' of molds and objects.   

eventually, our final idea emerged and triggered questions about...   
what if we can **store data** inside objects we use in our daily life?  
what is our **coffee cup is also a pen drive**, which has a song from your grandma or encrypted your passwords?  

what if we can store data into objects we use in our daily life?  
what is our coffee cup is also a pen drive, which has a song from your grandma or encrypted your passwords?  


## **concept**  
we are creating a tool that will encode audio messages into physical objects, which will then be retrieved and sonified. it will read or listen the messages we give and will engrave them on ceramics. 
cups, pots and other things will be carriers of our stories and will travel through time. 
it is a concept that deals with continuity and archiving.  

for this first prototype, we are writing audio messages in real-time. a microphone will capture the audio and through arduino it will convert the message into a sound waves, which will be getting written on a paper cup.  

the central idea has a lot of potential both on a theoretical, speculative level but also on the technological level. based on our existing collective knowledge we approached this challenge with a 'realistic ambition'.    

## **plan**   
we started imagining how it would look, what materials, motors and tools would we need. the more we tried to describe it, the more complex it got. multiple axes, motors, spinning wheels and plates started getting shape.. and that was only the hardware.  

This project made use of some parts rescued from an out of service reprap 3D printer that was left in out classroom from the 'tech beyond the myth' course, so we started by disassembling it. We used 2 servo motors, one for the turntable and one for the 2-axis. We also repurposed the controller boards which consistsed of an Arduino Mega and a Ramps 1.4 shield for the Mega. In addition to the electronics we were able to use the alumunim rails and various nuts and bolts from the old 3D printer to construct the drawing/carving machine. 


![](process.jpg)

## **iterating**  
according to our predictions, we were relatively lucky. we managed to make our first laser cut pieces fit together (ok, with some sanding).  
we had to test the holes for the press fit a couple of times before sending our full printing file, which was different for each material. 

![](process2.jpg)  


![](andaaza2.jpg)  

## **problems and improvements**

We knew this would be an ambitious artifact to make, and we most likely wouldn't be able to complete it in the four days of the first micro challenge. We planned to make the first iteration of the prototype in the first week, which consists of a motorized turntable and an arm that could move up and down and hold different toolheads such as a pen. This first iteration was designed to write on a paper cup and test out our idea. 

Though we didn't have time to connect the sound input to the project, we did manage to connect a microphone and plot the sound on the Arduion serial plotter. We will be exploring the sound interface in the coming weeks. This week, we managed to build a simple turntable and motorize it, as well as create a frame for the z-axis that will serve as an interchangeable toolhead for pens and carving tools. We still have some work to do on the z-axis plate to correct some sagging as it moves up and down as well as redesiging it to better hold pens and tools. Though our rubberband solution works quite well, especially if there are only 4 days to build. :) 


Click on the image to view the presentation :)  
[![Fab Micro Challenge 1 Presentation](Andaaza.png)](https://www.canva.com/design/DAFaumtP7p8/6alduDLkCOwk2gHwn5hSnA/view?utm_content=DAFaumtP7p8&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink)

 ## **personal reflection**   

First day, the ultimate chaos. We were a new formed team that had almost never worked together before, with very different interests that seemed as an unbridgeable gap. The whole first day of the challenge was spent on ideatingm as we couldnt find a topic that all the three of us liked equally. Many thoughts and discussions eventually lead us to a sudden epiphany that immediately conviced us all. Somehow it onvolved all the aspects that each of us was looking for and so we started working on it. I was particularly excited by the fact I would finally get to do some 3d modeling with rhino whoch i have missed a lot and hadnt had the chance so far.  

As we started working on the project, we quickly realized that it was going to be a lot more challenging than we had initially thought. We had to imagine how it would look and what materials, motors, and tools we would need. The more we talked about it, the more complex it seemed to get.  

Despite our best efforts, we knew that we most likely wouldn't be able to complete the ambitious artifact we had envisioned in just four days. So, we planned to make the first iteration of the prototype during the first week, which would consist of a motorized turntable and an arm that could move up and down and hold different toolheads such as a pen. Our first iteration was designed to write on a paper cup and test out our idea.  

We didn't have enough time to connect the sound input to the project. However, we did manage to connect a microphone and plot the sound on the Arduino serial plotter and we will definitely explore the sound interface in the coming weeks.  

Overall, the experience was intense and quite challenging, but we managed to build an actual turntable and motorize it, as well as create a frame for the z-axis that will serve as an interchangeable toolhead for pens and carving tools. There's still a lot of work to be done on the z-axis plate to correct some sagging as it moves up and down, but our low-tech rubberband solution works quite well for the moment.. We're all looking forward to continuing this project and seeing where it takes us!  

## Useful Links and References

[Using the Arduino AccelStepper Library](https://hackaday.io/project/183713-using-the-arduino-accelstepper-library)

[AccelStepper](https://github.com/waspinator/AccelStepper) Library

[Vinyl Record Cutting Lathe](https://fabacademy.org/2020/labs/digiscope/students/ambroise-devries/docs/p02.html) Fabacademy Project by Ambroise de Vries

[DIY Record Cutting](http://fab.cba.mit.edu/classes/863.09/people/lifeform/13/index.html) Fabacademy project by David Robert

