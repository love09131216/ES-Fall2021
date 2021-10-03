# 嵌入式系統 - 實作3: 使用超音波感測器 + LED控制, 常用的C語言程式介紹

### Lab 3-1: Ultrasonic Sensor (3-pin) + 測距 (以公分顯示即可) + RS232 Output,
![image](https://user-images.githubusercontent.com/89329170/134792726-b6587289-6ed6-459f-9bf3-692563009ede.png)

````c
int inches = 0;

int cm = 0;

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
  Serial.println("cm");
  delay(100); // Wait for 100 millisecond(s)
}
````



### Lab 3-2: 超音波感測器 + LED (紅色LED:亮<70cm, 緑色LED: 亮>270cm, 藍色LED:亮, 介於70cm ~ 270cm之間) + RS232 Output
![image](https://user-images.githubusercontent.com/89329170/134793272-4aff9a97-68a8-47bf-bc5c-c5486282b70c.png)

````c
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
````




#### Lab 3-3: Arudino常用的C語言程式介紹與實作請使用Arudino, 通過Serial印出9X9乘法表, 計算時亮紅色LED, 綠色LED慢慢變亮亮完成時全亮, 並且紅色LED OFF, 細節可參考以下Demo作法:
![image](https://user-images.githubusercontent.com/89329170/135738580-98d80e5c-ed55-4672-8e16-d2ae6c58963a.png)



````c
/*
 Lab 3-3, Embedded System, VNU
 Date: 2021/09/26
*/
int BLED = 13;
int RLED = 11;


int result, result2, result3;
String d0 = "****** 9X9 Table ******";
String d1, d2, d3;
void setup()
{
  pinMode(BLED, OUTPUT);   // Configure PIN13
  pinMode(RLED, OUTPUT);   // Configure PIN11
  
  Serial.begin(9600);

}

void loop()
{
  int aa = 0;

  Serial.println(d0); 
  
  digitalWrite(BLED, HIGH);
  analogWrite(RLED, aa); 
  
  for (int i=1;i<=9; i=i+3){
    for (int j=1;j<=9; j++){
      
      result = i*j;
      result2 = (i+1)*j;
      result3 = (i+2)*j;
      
      d1 = String(String(i) + "X" + String(j) + "=" + String(result));
      d2 = String(String(i+1) + "X" + String(j) + "=" + String(result2));
      d3 = String(String(i+2) + "X" + String(j) + "=" + String(result3));
      
      Serial.println(d1 + ", " + d2 + ", " + d3);


       
      aa+=1;
      
      delay(100);
    } // loop j
    analogWrite(RLED, aa*3); 
    Serial.println("");
  } // loop i

  digitalWrite(BLED, LOW);
  analogWrite(RLED, 255); 
  delay(2000);	
  analogWrite(RLED, 0);
}

````
