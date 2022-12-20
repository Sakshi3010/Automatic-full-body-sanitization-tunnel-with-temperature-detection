#include <Wire.h>
#include <Adafruit_MLX90614.h>
Adafruit_MLX90614 mlx = Adafruit_MLX90614();

#define echoPin 2     //Pin for ultrasonic sensor
#define trigPin 3       //Pin for ultrasonic sensor
long duration;     
int distance;           //variable for saving distance value of ultrasonic

int LED_RED = 11;       //red led pin
int LED_GREEN = 12;     //green led pin
const int buzzer = 8;   //Pin for buzzer
int relay = 10;         // pin for relay 

void setup() {
  Serial.begin(9600);  
  mlx.begin();  
  pinMode(LED_RED,OUTPUT);
  pinMode(LED_GREEN,OUTPUT);
  pinMode(buzzer,OUTPUT);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(relay,OUTPUT);
}
void loop() {
float Tc =(mlx.readObjectTempC());
float Tf= (mlx.readObjectTempF());

//Serial.print("Temperature : ");
//Serial.print(Tf);
//Serial.println(" Fahrenheit");

Serial.println();
delay(200);
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;
  Serial.println(distance);
while(distance < 30){
    Tc = int(mlx.readObjectTempC());
    Tf = int(mlx.readObjectTempF());
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    duration = pulseIn(echoPin, HIGH);
    distance = duration * 0.034 / 2;
    digitalWrite(relay, LOW);
    
    Serial.println("Temperature : " + String(Tc) + " Celsius");
    Serial.println("Distance " + String(distance));
    
    if(Tc>30){
      digitalWrite(LED_RED,HIGH);
      digitalWrite(LED_GREEN,LOW);
      tone(buzzer, 1000);
      delay(100);
    } 
    else{
      digitalWrite(LED_RED,LOW);
      digitalWrite(LED_GREEN,HIGH);
      noTone(buzzer);
      delay(100);
    }
    digitalWrite(relay, LOW);
  }
  digitalWrite(relay, HIGH);
}
