# ReacodaIoTWorkshop



Holiday Coding Workshop
short curriculum for electronics, internet of things, and sustainable farming methods 








Day 1:
We will be introducing the programme to the participants: The importance of the skills and lessons, why they should learn, how will they learn.
For this activity:
Encourage the students to work together.
Encourage them to think deeper and critically about the challenges that the persona (Belinda, the farmer) is experiencing.
What will you need:
A notebook/paper and a pen
  

Design Thinking:

Scenario: Belinda is a hydroponics farmer based in Braamfontein, Johannesburg. She currently stays in Alexandra which is 16 KM away from her workplace (farm). Every morning she has to catch a taxi which is not always a  reliable mode of transport.

When she gets to her she needs to make sure there is enough water in the reservoir, make sure there is enough nutrients, make sure that the pH and EC levels are at the right level to help the crops grow.

Challenges: During summers her tunnel (greenhouse) becomes very warm inside which causes high humidity which affects the growth and well-being of her vegetables. They get infected with diseases which prevents them normally.
Motivation: Belinda wants to grow enough lettuce, kale, and spinach to sell to the green grocer market; She also wants allows walk-ins (allow people to come buy directly from her farm).

Habits:  
Empathy:   
Activity: (recommended time of 15 to 20 min)

On a piece of paper write down all the challenges that Belinda experiences on a daily basis.
Encourage the kids to think about the challenges in more detail; How do the challenges affect her general well-being; how do they affect her productivity daily; 
How will her productivity (or lack of) will affect sales, revenue and profit

Define The Problem:

Activity: (recommended time of 5 to 8 min)

Define the needs of Belinda; write them down
Write down the problem statement

Ideate:

Activity: (recommended time of 15 to 20 min)

Write down ideas that focus on the problem statement
Think of as many ideas as possible; the ideas don’t need to be perfect, they just need to make sense based on the problem statement

Prototype:

Activity: (recommended time of 20 to 30 min)

Reflect on what you have learnt from the different ideas that you came up with.
How will your idea fit in the context of actual lives.
Solution could be a combination of a new idea and what’s already being used.
connect the dots, build a prototype a

Test:

Test the prototype with real people; ask for feedback; Don’t defend your idea; any criticism is very important as it may help to improve your solution; be open-minded

Day 2:

Introduction to Computer Programming

The purpose of this activity is to introduce the basics of programming
The fundamentals of an Arduino; The rules/syntax 



The basics of an Arduino

What is Arduino?
Arduino is an open-source electronics platform based on easy-to-use hardware and software. Arduino boards are able to read inputs - light on a sensor, a finger on a button, or a Twitter message - and turn it into an output - activating a motor, turning on an LED, publishing something online. You can tell your board what to do by sending a set of instructions to the microcontroller on the board.
To do so you use the Arduino programming language (based on Wiring), and the Arduino Software (IDE), based on Processing


 

What you will need
 
An Arduino Uno board
3 LEDs (red, green, yellow)
male to male jumper wires
100 ohm resistor (black-brown-black)
Breadboard
Arduino-based NodeMCU
Smartphone (with Blynk installed)


Software
Arduino IDE (either online or offline)

Digital, Analog The Arduino has 14 Digital pins, and 6 Analog pins. A Digital pin can operate in two ways: On, also known as "HIGH", and Off, otherwise known as "LOW". When a Digital Pin is set to On, 5 volts of electricity are running through it. When it's set to Off, no voltage runs through it. This will make it easy for us to turn an LED on or off. These pins are represented as "DIGITAL", pins 0 through 13 at the top right of the Arduino pictured above.
 

What to do 
Activity (recommended time 35 min to 45 min)


Connect the anode (long leg) of each LED to digital pins eight, nine, and ten (via a 220? resistor). Connect the cathodes (short leg) to Arduino ground.


The Code
Start by defining variables so that we can address the lights by name rather than a number. Start a new Arduino project, and begin with these lines:
int red = 10;
int yellow = 9;
int green = 8;

Next, let’s add the setup function, where’ll we configure the red, yellow and green LEDs to be outputs. Since you have created variables to represent the pin numbers, you can now refer to the pins by name instead.

void setup(){
    pinMode(red, OUTPUT);
    pinMode(yellow, OUTPUT);
    pinMode(green, OUTPUT);
}








Create a separate function for changing the lights.

void loop(){
    changeLights();
    delay(15000);
}

void changeLights(){+    // green off, yellow on for 3 seconds
    digitalWrite(green, LOW);
    digitalWrite(yellow, HIGH);
    delay(3000);

    // turn off yellow, then turn red on for 5 seconds
    digitalWrite(yellow, LOW);
    digitalWrite(red, HIGH);
    delay(5000);

    // red and yellow on for 2 seconds (red is already on though)
    digitalWrite(yellow, HIGH);
    delay(2000);

    // turn off red and yellow, then turn on green
    digitalWrite(yellow, LOW);
    digitalWrite(red, LOW);
    digitalWrite(green, HIGH);
    delay(3000);
}

Done! Now, upload and run (make sure to select the correct board and port from the Tools> Port and Tools > Board menus). You should have a working traffic light that changes every 15 seconds.

A Pedestrian Crossing

Activity (recommended time 20 to 35 min)
Now that you know the basics, let’s improve it. Add in a pushbutton for pedestrians to change the light whenever they like:



Notice how the traffic light is exactly the same as the previous example. Connect the button to digital pin 12. You’ll notice that the switch has a high-impedance 10k? resistor attached to it, and you may be wondering why. This is called a pull-down resistor. It’s a difficult concept to grasp at first, but bear with me.



A switch either lets the current flow, or doesn’t. This seems simple enough, but in a logic circuit, the current should be always flowing in either a high or low state (remember – 1 or 0, high or low). You might assume that a pushbutton switch that isn’t actually being pushed would be defined as being in a low state, but in fact it’s said to be ‘floating’, because no current is being drawn at all.

In this floating state, it’s possible that a false reading will occur as it fluctuates with electrical interference. In other words, a floating switch is giving neither a reliable high, nor low state reading. A pull down resistor keeps a small amount of current flowing when the switch is closed, thereby ensuring an accurate low state reading. In other logic circuits, you may find a pull-up resistor instead – this works on the same principle, but in reverse, making sure that particular logic gate defaults to high.

Now, in the loop part of the code, instead of changing the lights every 15 seconds, we’re going to read the state of the pushbutton switch instead, and only change the lights when it’s activated.

The Code
Start by adding a new variable to the start of the program:
int button = 12; // switch is on pin 12

Now, in the setup function, add a new line to declare the switch as an input. I’ve also added a single line to start the traffic lights in the green stage. Without this initial setting, they would be turned off, until the first time a changeLights() was initiated using a function.

pinMode(button, INPUT);
digitalWrite(green, HIGH);

Change the entire loop function to the following instead:
void loop() {
    if (digitalRead(button) == HIGH){
        delay(15); // software debounce
        if (digitalRead(button) == HIGH) {
            // if the switch is HIGH, ie. pushed down - change the lights!
            changeLights();
            delay(15000); // wait for 15 seconds
        }
    }
}

That should do it. You may be wondering why the button is checked twice (digitalRead(button)), separated by a small delay. This is called debouncing. Much like the pull down resistor was needed for the button, this simple check stops the code detecting minor interference as a button press. You don’t have to do this (and it would probably work just fine without it), but it’s good practice.


By waiting inside the if statement for 15 seconds, the traffic lights can’t change for at least that duration. Once 15 seconds is up, the loop restarts. Each restart of the loop, read the state of the button again, but if it isn’t pressed, the if statement never activates, the lights never change, and it simply restarts again.
A Junction
Activity (recommended time 20 to 40 min)
Let’s try a more advanced model. Instead of a pedestrian crossing, modify your circuit to have two traffic lights:


Connect the second traffic light to digital pins 11, 12, and 13.            


[
The Code
First, assign your new traffic light pins to variables, and configure them as outputs, just like in the first example:

// light one
int red1 = 10;
int yellow1 = 9;
int green1 = 8;

// light two
int red2 = 13;
int yellow2 = 12;
int green2 = 11;

void setup(){
    // light one
    pinMode(red1, OUTPUT);
    pinMode(yellow1, OUTPUT);
    pinMode(green1, OUTPUT);

    // light two
    pinMode(red2, OUTPUT);
    pinMode(yellow2, OUTPUT);
    pinMode(green2, OUTPUT);
}


Now, update your loop to use the code from the first example (instead of the pedestrian crossing):

void loop(){
    changeLights();
    delay(15000);
}

Once again, all the work is being carried out in the changeLights() function. Rather than going red > red & yellow > green, this code will alternate the traffic lights. When one is on green, the other will be on red. Here’s the code:

void changeLights(){
    // turn both yellows on
    digitalWrite(green1, LOW);
    digitalWrite(yellow1, HIGH);
    digitalWrite(yellow2, HIGH);
    delay(5000);

    // turn both yellows off, and opposite green and red
    digitalWrite(yellow1, LOW);
    digitalWrite(red1, HIGH);
    digitalWrite(yellow2, LOW);
    digitalWrite(red2, LOW);
    digitalWrite(green2, HIGH);
    delay(5000);

    // both yellows on again
    digitalWrite(yellow1, HIGH);
    digitalWrite(yellow2, HIGH);
    digitalWrite(green2, LOW);
    delay(3000);

    // turn both yellows off, and opposite green and red
    digitalWrite(green1, HIGH);
    digitalWrite(yellow1, LOW);
    digitalWrite(red1, LOW);
    digitalWrite(yellow2, LOW);
    digitalWrite(red2, HIGH);
    delay(5000);

}
The TMP34 temperature sensor
Activity (recommended time 30 to 45 min)
The circuit

In this activity you will be measuring the ambient temperature of the room. 

wire up your breadboard so you have power and ground. 

Constants are similar to variables in that they allow you to uniquely name things in the program, but unlike variables they cannot change. Name the analog input for easy reference, and create another named constant to hold the baseline temperature. For every 2 degrees above this baseline, the LED will turn on. The temperature is being stored as a float, or floating-point number. This type of number has a decimal point, and is used for numbers that can be expressed as fractions.
In the setup you’re going to use a new command, Serial. begin(). This opens up a connection between the Arduino and the computer, so you can see the values from the analog input on your computer screen.
The argument 9600 is the speed at which the Arduino will communicate, 9600 bits per second. You will use the Arduino IDE’s serial monitor to view the information you choose to send from your microcontroller. When you open the IDE’s serial monitor verify that the baud rate is 9600.
Next up is a for() loop to set some pins as outputs. These are the pins that you attached LEDs to earlier. Instead of giving them unique names and typing out the pinMode() function for each one, you can use a for() loop to go through them all quickly. This is a handy trick if you have a large number of similar things you wish to iterate through in a program. Tell the for() loop to run through pins 2 to 4 sequentially.
The function Serial.print() sends information from the Arduino to a connected computer. You can see this information in your serial monitor. If you give Serial.print() an argument in quotation marks, it will print out the text you typed. If you give it a variable as an argument, it will print out the value of that variable.
The Code
const int sensorPin = A0; 
const float baselineTemp = 20.0;
void setup(){ 
Serial.begin(9600); // open a serial port 
for(int pinNumber = 2; pinNumber<5; pinNumber++){ 
pinMode(pinNumber,OUTPUT);
 digitalWrite(pinNumber, LOW); }
 }
void loop(){ 
int sensorVal = analogRead(sensorPin);
Serial.print(“Sensor Value: “); 
Serial.print(sensorVal);
 // convert the ADC reading to voltage
 float voltage = (sensorVal/1024.0) * 5.0;
Serial.print(“, Volts: “); 
Serial.print(voltage);
Serial.print(“, degrees C: “); 
// convert the voltage to temperature in degrees 
float temperature = (voltage - .5) * 100; 
Serial.println(temperature);
if(temperature < baselineTemp){ 
digitalWrite(2, LOW);
 digitalWrite(3, LOW); 
digitalWrite(4, LOW); 
}else if(temperature >= baselineTemp+2 && temperature < baselineTemp+4){ digitalWrite(2, HIGH); 
digitalWrite(3, LOW); 
digitalWrite(4, LOW);
}else if(temperature >= baselineTemp+6){ 
digitalWrite(2, HIGH); 
digitalWrite(3, HIGH); 
digitalWrite(4, HIGH);
} 
delay(1); 
} 
The voltage will be a value between 0 and 5 volts, and it will have a fractional part (for example, it might be 2.5 volts), so you’ll need to store it inside a float. Create a variable named voltage to hold this number. Divide sensorVal by 1024.0 and multiply by 5.0. The new number represents the voltage on the pin. 

Just like with the sensor value, you’ll print this out to the serial monitor.
every 10 millivolts of change from the sensor are equivalent to a temperature change of 1 degree Celsius. It also indicates that the sensor can read temperatures below 0 degrees. Because of this, you’ll need to create an offset for values below freezing (0 degrees). If you take the voltage, subtract 0.5, and multiply by 100, you get the accurate temperature in degrees Celsius. Store this new number in a floating point variable called temperature.
Now that you have the real temperature, print that out to the serial monitor too. Since the temperature variable is the last thing you’re going to be printing out in this loop, you’re going to use a slightly different command: Serial.println(). This command will create a new line in the serial monitor after it sends the value. This helps make things easier to read in when they are being printed out.

Setting up Blynk
Things needed:
NodeMCU Arduino-based ESP8266
Smartphone 
Blynk app 
The first thing to do is to set up the Arduino IDE. Install the esp8266 library. The link for the library is as follows: https://github.com/esp8266/Arduino
Method 1:
To install the Blynk library just follow the instructions as it is on the link: 
http://help.blynk.cc/en/articles/512105-how-to-install-blynk-library-for-arduino



