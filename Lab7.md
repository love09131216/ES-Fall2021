# Lab 7-1 在你的Google Drive, 建立你的第一個Colab Notebook 
### Step 4. 在你Colab Notebook顯示以下訊息(OOO: 你的英文名字; e.g., Joe biden)
![image](https://user-images.githubusercontent.com/89329170/141666040-fc6cbc9c-694d-4615-b827-72aac047aab6.png)



### Lab 7-2 暖身: 一起來十分鐘學會Python
````cccc
# task 1: string variable
name = "TA Grace"
print(name)

# task 2: number variable
number = 26
print(number)
print(number*3)
print(number/2)
print(number + number)
print(number - number)

# task 3: function

def printName(firstName, lastName):
  print(lastName + ' ' + firstName)

printName('Grace', 'TA')

# task 4: if else

def printName(firstName, lastName, isCool):
  if isCool:
    print(lastName + ' ' + firstName + ' very cool!')
  else:
    print(lastName + ' ' + firstName + ' not cool!')

# Start
printName('Grace', 'TA', True)
printName('Grace', 'TA', False)

# task 5: for loop

def printName(firstName, lastName, isCool, num):
  for i in range(1, num):
    if isCool:
      print(i, lastName + ' ' + firstName + ' very cool!')
    else:
      print(i, lastName + ' ' + firstName + ' not cool!')

# Start
printName('Grace', 'TA', True, 10)

cccc




### Lab 7-3 確認Lab7完成的兩個Notebook都成功的存在你的雲端硬碟/ES2021目錄下.
![image](https://user-images.githubusercontent.com/89329170/141666277-fd845e46-155f-4f39-9bce-3a85837724f7.png)
