# Arduino_Multi_LED_Microcontroller

The loops this runs through:

<img width="485" alt="Screen Shot 2022-08-09 at 8 35 20 PM" src="https://user-images.githubusercontent.com/66803124/183785201-ca90443e-098b-49fe-93da-1dda17f75b4a.png">

I started with a single blinking LED and changed/played with the timing of the blink from 1:1 to 4:4 to manipulate the code more. 
<img width="563" alt="Screen Shot 2022-08-10 at 8 22 31 AM" src="https://user-images.githubusercontent.com/66803124/183899971-c007317e-cf98-44e6-bd18-88e0cc7dc144.png">

I then wired up 8 lEDs each with their own transitorsm=, ground wire and 5v of power to the breadboard. 

This is the Marque loop you see in the images of the various loops. The LEDs are timed in a way that two of them chase each other "around" the usually square sign. 
<img width="415" alt="Screen Shot 2022-08-10 at 8 26 56 AM" src="https://user-images.githubusercontent.com/66803124/183900889-27c0d63e-9bd9-42fa-9cba-14b77ee4e616.png">

Next I tried the ping pong where the LEDs run down the list and "hit" one end which causes them to bounce back running up the other way. 
<img width="1057" alt="Screen Shot 2022-08-10 at 8 32 00 AM" src="https://user-images.githubusercontent.com/66803124/183901959-ab72083a-89d3-4c88-9ac3-89b408165753.png">
<img width="1034" alt="Screen Shot 2022-08-10 at 8 32 43 AM" src="https://user-images.githubusercontent.com/66803124/183902083-6a4b0378-8407-4844-9997-2e70da01187b.png">
<img width="1056" alt="Screen Shot 2022-08-10 at 8 33 27 AM" src="https://user-images.githubusercontent.com/66803124/183902235-e1faf26f-b946-4262-9d93-d64b8cca9e52.png">

I tested out random blinking and street light blinking, and many more are possible. 

#Here is the code that ran the microcontroller. 
```
int ledPins[] = {2,3,4,5,6,7,8,9};

void setup()
{
  int index;
  

  for(index = 0; index <= 7; index++)
  {
    pinMode(ledPins[index],OUTPUT);
    // ledPins[index] is replaced by the value in the array.
    // For example, ledPins[0] is 2
  }
}


void loop()
{

  //oneAfterAnotherNoLoop();  // Light up all the LEDs in turn
  
  //oneAfterAnotherLoop();  // Same as oneAfterAnotherNoLoop,
                            // but with much less typing
  
  //oneOnAtATime();         // Turn on one LED at a time,
                            // scrolling down the line
  
  pingPong();             // Light the LEDs middle to the edges

  //marquee();              // Chase lights like you see on signs

  //randomLED();            // Blink LEDs randomly
}


void oneAfterAnotherNoLoop()
{
  int delayTime = 100; // time (milliseconds) to pause between LEDs
                       // make this smaller for faster switching

  // turn all the LEDs on:

  digitalWrite(ledPins[0], HIGH);  //Turns on LED #0 (pin 2)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[1], HIGH);  //Turns on LED #1 (pin 3)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[2], HIGH);  //Turns on LED #2 (pin 4)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[3], HIGH);  //Turns on LED #3 (pin 5)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[4], HIGH);  //Turns on LED #4 (pin 6)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[5], HIGH);  //Turns on LED #5 (pin 7)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[6], HIGH);  //Turns on LED #6 (pin 8)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[7], HIGH);  //Turns on LED #7 (pin 9)
  delay(delayTime);                //wait delayTime milliseconds  
 
  // turn all the LEDs off:
  
  digitalWrite(ledPins[7], LOW);   //Turn off LED #7 (pin 9)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[6], LOW);   //Turn off LED #6 (pin 8)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[5], LOW);   //Turn off LED #5 (pin 7)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[4], LOW);   //Turn off LED #4 (pin 6)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[3], LOW);   //Turn off LED #3 (pin 5)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[2], LOW);   //Turn off LED #2 (pin 4)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[1], LOW);   //Turn off LED #1 (pin 3)
  delay(delayTime);                //wait delayTime milliseconds
  digitalWrite(ledPins[0], LOW);   //Turn off LED #0 (pin 2)
  delay(delayTime);                //wait delayTime milliseconds  
}
 

void oneAfterAnotherLoop()
{
  int index;
  int delayTime = 100; // milliseconds to pause between LEDs
                       // make this smaller for faster switching

  // Turn all the LEDs on:
 
  // This for() loop will step index from 0 to 7
  // (putting "++" after a variable means add one to it)
  // and will then use digitalWrite() to turn that LED on.
  
  for(index = 0; index <= 7; index++)
  {
    digitalWrite(ledPins[index], HIGH);
    delay(delayTime);                
  }                                  

  // Turn all the LEDs off:

  // This for() loop will step index from 7 to 0
  // (putting "--" after a variable means subtract one from it)
  // and will then use digitalWrite() to turn that LED off.
 
  for(index = 7; index >= 0; index--)
  {
    digitalWrite(ledPins[index], LOW);
    delay(delayTime);
  }               
}


void oneOnAtATime()
{
  int index;
  int delayTime = 100; // milliseconds to pause between LEDs
                       // make this smaller for faster switching
  
  // step through the LEDs, from 0 to 7
  
  for(index = 0; index <= 7; index++)
  {
    digitalWrite(ledPins[index], HIGH);  // turn LED on
    delay(delayTime);                    // pause to slow down
    digitalWrite(ledPins[index], LOW);   // turn LED off
  }
}


void pingPong()
{
  int index;
  int delayTime = 100; // milliseconds to pause between LEDs
                       // make this smaller for faster switching
  
  // step through the LEDs, from 0 to 7
  
  for(index = 0; index <= 7; index++)
  {
    digitalWrite(ledPins[index], HIGH);  // turn LED on
    delay(delayTime);                    // pause to slow down
    digitalWrite(ledPins[index], LOW);   // turn LED off
  }

  // step through the LEDs, from 7 to 0
  
  for(index = 7; index >= 0; index--)
  {
    digitalWrite(ledPins[index], HIGH);  // turn LED on
    delay(delayTime);                    // pause to slow down
    digitalWrite(ledPins[index], LOW);   // turn LED off
  }
}

void marquee()
{
  int index;
  int delayTime = 200; // milliseconds to pause between LEDs
                       // Make this smaller for faster switching
  
  // Step through the first four LEDs
  // (We'll light up one in the lower 4 and one in the upper 4)
  
  for(index = 0; index <= 3; index++) // Step from 0 to 3
  {
    digitalWrite(ledPins[index], HIGH);    // Turn a LED on
    digitalWrite(ledPins[index+4], HIGH);  // Skip four, and turn that LED on
    delay(delayTime);                      // Pause to slow down the sequence
    digitalWrite(ledPins[index], LOW);     // Turn the LED off
    digitalWrite(ledPins[index+4], LOW);   // Skip four, and turn that LED off
  }
}


void randomLED()
{
  int index;
  int delayTime;
  
  // The random() function will return a semi-random number each
  // time it is called. See http://arduino.cc/en/Reference/Random
  // for tips on how to make random() even more random.
  
  index = random(8);  // pick a random number between 0 and 7
  delayTime = 100;
  
  digitalWrite(ledPins[index], HIGH);  // turn LED on
  delay(delayTime);                    // pause to slow down
  digitalWrite(ledPins[index], LOW);   // turn LED off
}


```
