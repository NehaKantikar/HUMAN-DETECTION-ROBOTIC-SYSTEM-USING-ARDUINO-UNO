# HUMAN-DETECTION-ROBOTIC-SYSTEM-USING-ARDUINO-UNO

INTRODUCTION
A unique passive Infrared sensor is used in our design that emits infrared rays to detect humans. 
As a human body emits thermal radiation it will be received and manipulated by the PIR (Passive infrared sensor). 
Once a human target is located the system has to give an alert which may help to localize the victim location as soon as possible. 
The main design of the robot consists of a 'Human Detection Module' carried by a mobile robot platform sufficiently small enough to wander around the area and carry out its search activity.
The robot will be also equipped with a camera to transmit live video, of the disaster location, to the rescue team so that false alerts may be omitted and a visual contact with the victim would be executed.
The human detection module utilizes also an infrared LED lighting to show off the robot’s surrounding under low or no light conditions. 
Human Detection Robot can be carried to any place in the world and can be assembled in some few hours for fast search and rescue operations. The design is simple with the cheapest budget.

The below Link for the reference sake:
https://drive.google.com/file/d/1MJG-j0zFjizKEaJN0mOvY2LYME9Xp4Gm/view?usp=sharing


CODE:
int val;
int tempPin = A0;
int sensor = 2;
int val1 = 0;

#define echoPin 3 // attach pin D2 Arduino to pin Echo of HC-SR04
#define trigPin 4 //attach pin D3 Arduino to pin Trig of HC-SR04

// defines variables
long duration; 
int distance; 
int M1=A2;
int M2=A3;
int M3=A4;
int M4=A5;

void setup()
{
  Serial.begin(9600);
  pinMode(sensor, INPUT);
  pinMode(tempPin,INPUT);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(M1, OUTPUT);
  pinMode(M2, OUTPUT);
  pinMode(M3, OUTPUT);
  pinMode(M4, OUTPUT);
}
void loop()
{
  val = analogRead(tempPin);
  val1 = digitalRead(sensor);  

  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  // Sets the trigPin HIGH (ACTIVE) for 10 microseconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  // Reads the echoPin, returns the sound wave travel time in microseconds
  duration = pulseIn(echoPin, HIGH);
  // Calculating the distance
  distance = duration * 0.034 / 2; // Speed of sound wave divided by 2 (go and back)
  // Displays the distance on the Serial Monitor
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if(distance<=22)
  {
    digitalWrite(M1,HIGH);
    digitalWrite(M2,LOW);
    digitalWrite(M3,LOW);
    digitalWrite(M4,HIGH);
    Serial.println("Rotating");
    delay(100);
  }
  else
  {
    digitalWrite(M1,HIGH);
    digitalWrite(M2,LOW);
    digitalWrite(M3,HIGH);
    digitalWrite(M4,LOW);
    Serial.println("Moving Forward");
    delay(100);
  }
  if(val1==1)
  {
    Serial.println("Motion detected!"); 
  }
  else
  {}
  
  float mv = ( val/1024.0)*5000;
  float cel = mv/10;
  float farh = (cel*9)/5 + 32;
  Serial.print("TEMPRATURE = ");
  Serial.print(cel);
  Serial.print("*C");
  Serial.println();
  delay(100);

  
}

