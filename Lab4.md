# 實作4: 七段顯示器, LCD 顯示器 + 超音波感測器 

### Lab 4-1 用七段顯示器來顯示數字"8."
![image](https://user-images.githubusercontent.com/89329170/139076364-1442d7e1-d53e-4a38-8e7d-979826470979.png)

````c
void setup()
{
for(int x = 1; x < 9; x++) {
pinMode(x,OUTPUT);
}
}

void seg71(int a, int b, int c, int d, int e, int f, int g, int h)
{
digitalWrite(1, a);
digitalWrite(2, b);
digitalWrite(3, c);
digitalWrite(4, d);
digitalWrite(5, e);
digitalWrite(6, f);
digitalWrite(7, g);
digitalWrite(8, h);
delay(500);
}

void loop()
{
//    a, b, c, d, e, f, g, h
seg71(0, 0, 0, 0, 0, 0, 0, 0); // OFF
seg71(1, 1, 1, 1, 1, 1, 1, 1); // 8
}
````


###  4-2 如下圖的Demo, 用七段顯示器, 顯示 . →1→ ... → 9 → 0 → 全滅, 狀態改變的間隔時間為0.5秒**
![image](https://user-images.githubusercontent.com/89329170/139077748-bf020476-f197-4c6f-883c-3895afed67c6.png)





### ### Lab 4-3 LCD顯示"Hello" + 你的英文名字 (e.g., "Hello Joanna")
![image](https://user-images.githubusercontent.com/89329170/139667665-6d18c9cd-be81-431e-8338-2469accb132a.png)

````c
// include the library code:
#include <LiquidCrystal.h>

// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  lcd.print("hello, Joanna!");
}

void loop() {
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  lcd.setCursor(0, 1);
  // print the number of seconds since reset:
  lcd.print(millis() / 100);
}
````
