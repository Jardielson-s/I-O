# ARDUINO I/O
This is a project that describes the arduino inputs and outputs, has an example code for them.

## SCHEME




## EXPLANATION
<p> 
    The repository describes with example code the serial, analog and logic inputs and outputs of the arduino.
    The serial input and output is how the arduino connects to other devices, through a wire and the bits through them to establish the connection. 
    The logic input and output is 0 or 1, HIGH or LOW, that is, it assumes two states, while the analog input and output assumes values ​​within a certain     range, so these values are pulsed and converted to a logic signal.
</p>

##  CODE

* define two constant variables, one referring to pin 12 and the other referring to pin 2, both input and output logic. we have two variables. We also have two variables to represent the analog output and input referring to the potentiometer.
```
#define KEY_01 12
#define LED_01 2

unsigned int potenciometro;
unsigned int pwm;
```

* I'm defining a method, which receives a parameter referring to the serial input, if it's 1 the led on, if it's 0 the led off, I defined this through the digitalWrite method of the aduino.
```
void inputOnOff(int input){
  if(input == 0){
  	 digitalWrite(LED_01, LOW);
  }
  if(input == 1){
  	 digitalWrite(LED_01, HIGH);
  }
}
```

* here defined the pinmode if is input or output.
```
void setup()
{
  pinMode(LED_01, OUTPUT);
  pinMode(KEY_01, INPUT);
  pinMode(2,OUTPUT);
  Serial.begin(9600);
}
```

* Here is the core of the application, uses all the inputs and outputs mentioned in the repository, we receive an analogue value from the pornetiometer, we define two more variables, one to read a string and the other to receive a number from the serial input, we check if there is a serial input, if so, we use the output serial to print a message and we receive data from the serial input and convert it to int the function inputOnOff is called to turn the led on or off, if it receives 1 it turns on if it receives zero it turns it off. right after that we determine a phase of value for the pwm and we have a digital input condition if we click on the button or hold it, the led lights up, and then we check if the potentiometer is in a range greater than zero.
```
void loop()
{
  potenciometro = analogRead(A0);
  String read = "";
  int number = 0;
  if(Serial.available() > 0){
  	Serial.print("Serial: ");
    number = Serial.parseInt();
    Serial.println(number);
    inputOnOff(number);
    read = Serial.readStringUntil('\n');
    Serial.println(read);
  }
  pwm = map(potenciometro,0,1023,0,255);

  if(digitalRead(KEY_01) == HIGH){
    digitalWrite(LED_01, HIGH);
    delay(100);
  }
  if (pwm > 0) {
    analogWrite(2,pwm);
  }
 }
````
