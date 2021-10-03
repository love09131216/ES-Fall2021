# 嵌入式系統 - 實作1

### 1-1 在TinkerCAD開一個新的Circuit, 加上一個外部的LED, 並且ON (亮) 1秒, OFF(滅) 1秒

![image](https://user-images.githubusercontent.com/89329170/131238020-0acb92ae-4b9b-458a-adb9-6f36a083ff57.png)



### 1-2 在TinkerCAD開一個新的Circuit, 分別使甪R, G, B三種顏色的LED, ON (亮) 0.5秒, OFF(滅) 0.5秒, (互動3)

![image](https://user-images.githubusercontent.com/89329170/132113846-7da453f5-2389-42b2-87f4-ebff1ffaee2a.png)


````c
// C++ code
//
void setup()
{
  pinMode(13, OUTPUT);
}

void loop()
{
  digitalWrite(13, HIGH);
  digitalWrite(12, HIGH);
  digitalWrite(11, HIGH);
  delay(500); // Wait for 1000 millisecond(s)
  digitalWrite(13, LOW);
  digitalWrite(12, LOW);
  digitalWrite(11, LOW);
  delay(500); // Wait for 1000 millisecond(s)
}
````




### 1-**3 在**TinkerCAD開一個新的Circuit, 分別使甪R, G, B三種顏色的LED, 讓LED ON, OFF的順序為R >> G >> B >> G >> R .... 無限循環. (互動4)
![image](https://user-images.githubusercontent.com/89329170/132114169-fec14c25-ea06-49be-8622-5208c14e2ffc.png)

````c
void setup()
{
  pinMode(13, OUTPUT);
  pinMode(11, OUTPUT);
  pinMode(9, OUTPUT);
}

void loop()
{
  digitalWrite(13, HIGH);  
  delay(500); 
  digitalWrite(13, LOW);
  delay(500);
  digitalWrite(11, HIGH);
  delay(500);
  digitalWrite(11, LOW);
  delay(500);
  digitalWrite(9, HIGH);
  delay(500);
  digitalWrite(9, LOW);
  delay(500);
}
````
