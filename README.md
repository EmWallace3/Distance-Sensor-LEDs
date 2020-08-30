# Distance-Sensor-LEDs
Programming LEDs and two distance sensors for the ASSET project sculpture
Lets hope this works!


const int echoPin1 = 3;
const int trigPin1 = 2;

const int echoPin2 = 5;
const int trigPin2 = 4;

float duration, distance, distance1, distance2; //I saw people "defining the values of duration and distance" super differently!

void setup() {
  pinMode(trigPin1, OUTPUT);
  pinMode(trigPin2, OUTPUT);
  pinMode(echoPin1, INPUT);
  pinMode(echoPin2, INPUT); 
  pinMode(7, OUTPUT);
  pinMode(8, OUTPUT); //define input and output
  Serial.begin(9600); //instructions for connecting to serial monitor
}

void loop() {
  digitalWrite(trigPin1, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin1, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin1, LOW);
  duration = pulseIn(echoPin1, HIGH); //sets up distance sensor 1 (on right looking head on)
  distance1 = (duration*.0343)/2; //defines how the arduino should calculate distance, defines label as distance 1
  Serial.print("RightSensor=");
  Serial.print(distance1);
  Serial.println("cm");
  delay(500); //sets up how often data from "right sensor" should be displayed in serial monitor

digitalWrite(trigPin2, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin2, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin2, LOW);
  duration = pulseIn(echoPin2, HIGH); //sets up distance sensor 2 (on left looking head on)
  distance2 = (duration*.0343)/2; //defines how the arduino should calculate distance, defines label as distance 2
  Serial.print("LeftSensor=");
  Serial.print(distance2);
  Serial.println("cm");
  delay(500); //sets up how often data fron "left sensor" should be displayed in serial monitor

distance=distance1;
if (distance2 < distance1);
{ distance = distance2;
}                         //with help from Dav! Ensures that distance used is always the shortest distance obtained by both sensors

if (distance < 30)
{ digitalWrite(7,HIGH);
}
  else 
{ digitalWrite(7,LOW);
}                         // if/else statement for the first strip of LEDs, relating to a set (longer) distance
  
if (distance < 15)
{ digitalWrite(8,HIGH);
}
  else 
{ digitalWrite(8,LOW);
}                         // if/else statement for the second strip of LEDs, relating to a set (shorter) distance
}
