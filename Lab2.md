#嵌入式系統 - 實作2: 會呼吸的RGB LED,  按鍵控制, 狀態輸出 

###B1 實作2-1, analogWrite(): 並且觀查LED亮度變化是否有像"呼吸的效果"和示波器的波形有什麼關連性? (互動1), (2021-09-05)

![image](https://user-images.githubusercontent.com/89329170/132114885-9917374a-3357-4c40-b167-9e7407ec8bfe.png)
````c
// C++ code
//
/*
  Fade
  This example shows how to fade an LED on pin 9
  using the analogWrite() function.

  The analogWrite() function uses PWM, so if  you
  want to change the pin you're using, be  sure to
  use another PWM capable pin. On most  Arduino,
  the PWM pins are identified with   a "~" sign,
  like ~3, ~5, ~6, ~9, ~10 and ~11.
*/

int brightness = 0;

void setup()
{
  pinMode(9, OUTPUT);
}

void loop()
{
  for (brightness = 0; brightness <= 255; brightness += 5) {
    analogWrite(9, brightness);
    delay(30); // Wait for 30 millisecond(s)
  }
  for (brightness = 255; brightness >= 0; brightness -= 5) {
    analogWrite(9, brightness);
    delay(30); // Wait for 30 millisecond(s)
  }
}
````


###實作2-2, RGB LED燈全彩模組, 分別讓LED輪流表現正紅、正綠、正藍，三個顏色，時間間隔1秒鐘。並且觀查LED顏色和波形或是電壓有什麼關連性? 可將個人說明在更新GitHub時一起加入. (互動2), (2021-09-05)
![image](https://user-images.githubusercontent.com/89329170/132971069-9c453c0e-935e-44c5-be6b-f8148e0eb95d.png)

````c
int R = 9;
int G = 10;
int B = 11;

void setup()
{
  pinMode(R, OUTPUT);
  pinMode(G, OUTPUT);
  pinMode(B, OUTPUT);  
}

void loop()
{
	analogWrite(R, 255);
	analogWrite(G, 0);
	analogWrite(B, 0);
  	delay(1000);
	analogWrite(R, 0);
	analogWrite(G, 255);
	analogWrite(B, 0);
  	delay(1000);
	analogWrite(R, 0);
	analogWrite(G, 0);
	analogWrite(B, 255);
  	delay(1000);  
}
````



###實作2-3, 讓你的RGB LED燈全彩模組也可會"呼吸", LED顏色變化是否有像"呼吸的效果"和示波器的波形有什麼關連性? (互動3), (2021-09-12)
![image](https://user-images.githubusercontent.com/89329170/132971571-6cbbebff-e9e1-4e08-9d0c-1fefcaa194a0.png)
````c
// C++ code
//
int Red = 11;
int Green = 10;
int Blue = 9;
int i = 0;
int j = 0;
void swapLED(int j, int i) {
  switch (j) {
    case 1:
    analogWrite(Red, 0);
    analogWrite(Green, i);
    analogWrite(Blue, 0);
    break;
    case 2:
    analogWrite(Red, 0);
    analogWrite(Green, 0);
    analogWrite(Blue, i);
    break;
    default:
    analogWrite(Red, i);
    analogWrite(Green, 0);
    analogWrite(Blue, 0);
    break;
  }
}

void setup()
{
  pinMode(Red, OUTPUT);
  pinMode(Green, OUTPUT);
  pinMode(Blue, OUTPUT);
}

void loop()
{
  if (j > 3) {
  	j = 0;
  }
  for (i = 1; i <= 255; i += 5) {
    swapLED(j, i);
    delay(30);
  }
  for (i = 255; i >= 1; i -= 5) {
    swapLED(j, i);
    delay(30);
  }
  j++;
}
````





###實作2-4 analogRead(), 1024解析度 (i.e.,10-bit): 可變電阻 + 序列監視器與輸出; 當你改變可變電阻的阻值(e.g., 10K-ohm)時，序列監視器輸出的數值有什麼改變? 數值又有什麼意義呢? 可試將你的想法寫在你的GitHub Page中喔! (互動4) (2021-09-12)
![image](https://user-images.githubusercontent.com/89329170/132971855-cc8f0a4d-4f42-426b-ac65-744535afd5aa.png)
````c
int sensorValue = 0;

void setup()
{
  pinMode(A0, INPUT);
  Serial.begin(9600);
}

void loop()
{
  sensorValue = analogRead(A0);
  
  Serial.println(sensorValue);
  delay(10);
}
````





###B5 實作2-5: 按下按鍵, Green LED亮 & Red LED滅; 放開按鍵, Green LED滅 & Red LED亮. 想要再深入的同學可以試試喔. (思考方向: digitalRead(), digitalWrite(): 按鍵 +序列輸出 + LED), (互動5) (2021-09-19) 

![image](https://user-images.githubusercontent.com/89329170/134792417-439c63eb-c0d8-49a3-bbb7-3c2de9326c60.png)
````c

int buttonState = 0;
int GLED = 13;
int RLED = 8;

void setup()
{
  pinMode(2, INPUT);
  pinMode(GLED, OUTPUT); // GREEN
  pinMode(RLED, OUTPUT); // RED    
}

void loop()
{
  // read the state of the pushbutton value
  buttonState = digitalRead(2);
  // check if pushbutton is pressed.  if it is, the
  // buttonState is HIGH
  if (buttonState == HIGH) {
    // turn LED on  
    digitalWrite(GLED, HIGH);
    digitalWrite(RLED, LOW);    
  } else {
    // turn LED off    
    digitalWrite(GLED, LOW);
    digitalWrite(RLED, HIGH);
  }
  delay(10); // Delay a little bit to improve simulation performance
}

````
