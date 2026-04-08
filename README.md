# Question-2---Controlling-colour-of-RGB-LED-and-blinking-speed-of-another-LED-with-potentiometer
This project demonstrates how to use teh potentiometer to control both the colour of an RGB LED amd the blinking speed of a normal LED using Arduino. It helps in understanding analog input and how it is used to control multiple outputs.

-> Objective : 
1. Read the analog input from the potentiometer.
2. Control RGB LED colour using analog values.
3. Adjust the blinking speed of normal LED.
4. Understand the analog and PWM(Pulse With Modulation).

-> Tinkercad simulation link : https://www.tinkercad.com/things/gcFq9ODoudj-changing-colour-/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard&sharecode=UFQrZq6ncR_qQLm2D1YyG6hulpa_kL0enZClxnCMkmI

-> Components used : 
Arduino uno
RGB LED
1 Normal LED
Potentiometer
3 Resistors (each 330 Ohm)
1 Resistor (220 Ohm)
Breadboard
Jumper wires

-> Circuit Connection : 
Potentiometer :
  One end to 5V
  Other end to GND
  Middle pin to A0
RGB LED :
  Red to Pin 10
  Blue to Pin 8
  Green to Pin 6
Normal LED : 
  Positive terminal to Pin 13
  Negative terminal connected with resistor to GND

-> Working : 
The potentiometer provides an analog value (0-1023) using analogRead() function.
This different arnge of potentiometer values correspond to different colours like
  Red
  Green
  Blue
  Cyan
  Yellow
  Magenta
  White
anlogWrite() function is used to adjust the brightness of each colour component.
The same potentiometer values controls the blinking rate of normal LED
  Low value - Fast blinking
  High value - Slow blinking

-> Output : 
RGB LED changes colour smoothly as the potentiometer is rotated to different values.
Normal LED blinks fatser or slower depending on potentiometer position.

-> Code : [Controlling_colour_of_RGB_LED_and_blinking_speed_of_another_LED_with_potentiometer.c](https://github.com/user-attachments/files/26574252/Controlling_colour_of_RGB_LED_and_blinking_speed_of_another_LED_with_potentiometer.c)

//Controlling colour of RGB LED and blinking speed of another LED with potentiometer.
// C
int pot = A0; /*Potentiometer is connected to the analog input*/
int val = 0; 
int speed = 0;

/*Defining pins*/
int red = 10;
int blue = 8;
int green = 6;

// Normal LED for blinking
int led = 13;

void setup(){
  pinMode(pot, INPUT); //Input from analog pin.
  pinMode(red, OUTPUT);
  pinMode(green, OUTPUT);
  pinMode(blue, OUTPUT);
  pinMode(led, OUTPUT);
}
void loop(){
  
  int val = analogRead(pot);

   /* Storing the potentiometer values
     int val variable*/
   /* analogRead function reads the potentiometer values*/
  
  int speed = 100 + (val / 2);

    /* This avoids zero delay and gives
     smooth visible blinking*/
    /*analaogWrite function is used to change the
  	brightness(colour) of RGB LED*/
  
  if(val >=0 && val <=150){ 
    // for RED
    // 255 to make sure colour is bright
  	analogWrite(red, 255);
  	analogWrite(green, 0);
  	analogWrite(blue, 0);
  }
  else if(val > 150 && val  <=300){
    // for YELLOW
    //mixture of red & green.
    analogWrite(red, 255); 
  	analogWrite(green, 255);
  	analogWrite(blue, 0);
  }
  else if(val > 300 && val <= 450){
     // for GREEN
    analogWrite(red, 0);
  	analogWrite(green, 255);
  	analogWrite(blue, 0);
  }
  else if(val > 450 && val <= 600){ 
    // for CYAN
    //mixture of green & blue
    analogWrite(red, 0);
  	analogWrite(green, 255);
  	analogWrite(blue, 255);
  }
  else if( val > 600 && val <= 750){ 
    // for BLUE
    analogWrite(red, 0);
  	analogWrite(green, 0);
  	analogWrite(blue, 255);
  }
  else if(val >750 && val <= 900){ 
    // for MAGENTA
    // mixture of red & blue
    analogWrite(red, 255);
    analogWrite(green, 0);
    analogWrite(blue, 255);
  }
  else {
    // for WHITE
    // miture of red, green & blue
    analogWrite(red, 255);
  	analogWrite(green, 255);
  	analogWrite(blue, 255);
  }
  
  // Normal LED blinking
  digitalWrite(led, HIGH); // LED ON
  delay(speed);
  
  digitalWrite(led, LOW); // LED OFF
  delay(speed);
  
}

-> Brief expalantion of code :
The program reads the value from a potentiometer connected to analog pin A0 using analogRead() function. This value ranges from 0 to 1023. Based on this value, the code divides the range into different sections to control the colour of RGB LED. Each section corresponds to specific colour(Red, Yellow, Green, Cyan, Blue, Magenta, White). The analogWrite() function is used to control the brightness of red, blue, green pins, which combine to produce different colours. At the same time, the potentiometer values are also ised to control the blinking speed of a normal LED. A delay value (speed) is calculated from the potentiometer input, ensuring that the LED blinks faster or slower depending on how the knob is rotated.
