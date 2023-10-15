# 實作3: 使用超音波感測器 + LED控制, C語言程式速成

## Lab 3-1: Ultrasonic Sensor (3-pin) + 測距 (以公分顯示即可) + RS232 Output

### 電路 & Demo 程式

https://github.com/Chen-YOUAN/ES-Fall2023/assets/144580734/a7076fed-229c-49c4-bfbe-489e76cc4b0f

## Lab 3-2: 超音波感測器 + LED (紅色LED:亮<70cm, 藍色LED: 亮>270cm, 緑色LED:亮, 介於70cm ~ 270cm之間) + RS232 Output

### 電路 & Demo

https://github.com/Chen-YOUAN/ES-Fall2023/assets/144580734/40138263-8fd5-41ef-8e9c-9b7afd991291

### 程式

```C
int inches = 0;
int GLED = 8;
int RLED = 12;
int BLED = 10;
int cm = 0;

void LED(int RH, int GH, int BH)
{
  digitalWrite(RLED, RH);
  digitalWrite(GLED, GH);
  digitalWrite(BLED, BH);
}

long readUltrasonicDistance(int triggerPin, int echoPin)
{
  pinMode(triggerPin, OUTPUT);  // Clear the trigger
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  // Sets the trigger pin to HIGH state for 10 microseconds
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  // Reads the echo pin, and returns the sound wave travel time in microseconds
  return pulseIn(echoPin, HIGH);
}

void setup()
{
  Serial.begin(9600);
  digitalWrite(GLED, OUTPUT);
  digitalWrite(RLED, OUTPUT);
  digitalWrite(BLED, OUTPUT);
  
}

void loop()
{
  // measure the ping time in cm
  cm = 0.01723 * readUltrasonicDistance(7, 7);
  // convert to inches by dividing by 2.54
  inches = (cm / 2.54);
  Serial.print(inches);
  Serial.print("in, ");
  Serial.print(cm);
  
  if(cm<70){
    LED(1, 0, 0); //int RH, int GH, int BH
  }
  else if(cm>270){
    LED(0, 0, 1); //int RH, int GH, int BH
  }
  else{
    LED(0, 1, 0); //int RH, int GH, int BH
  }
  
  Serial.println("cm");
  delay(100); // Wait for 100 millisecond(s)
  
}

```

## Lab 3-3: Arudino常用的C語言程式介紹與實作

### 電路 & Demo

https://github.com/Chen-YOUAN/ES-Fall2023/assets/144580734/f6c445a6-90da-4287-949d-545ea6d3fe53

### 程式
