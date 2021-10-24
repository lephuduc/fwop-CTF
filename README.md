# Reverse Fwop Door - 500 pts  
## Có gì lào
 Đề thật ko có hinttttttt 
 
![image](https://user-images.githubusercontent.com/88520787/138580382-ee35e67e-5347-42f3-8213-2dd87f552cee.png)

Không có hint:(((
![image](https://user-images.githubusercontent.com/88520787/138580764-1ddf19a9-9a0e-402a-97af-b8af3ffc018e.png)

## Static analysis
Mình mở file lên thì thấy một đống rối nùi như vậy:)))

![image](https://user-images.githubusercontent.com/88520787/138580524-3b88ae21-8848-4fb3-863d-ddc898cc13d2.png)

![image](https://user-images.githubusercontent.com/88520787/138580807-f0b5bf4b-a675-45f9-b935-e688efe1b405.png)

Đoạn code biến flag thành chuỗi ASCII rồi kiểm tra một loại các điều kiện :((((((((((((((((((

## S0lut1on

Giải hệ phương trình bật 1 60 biến và submit thôi:))))))

.

Có một thời gian mình tìm hiểu python thì mình biết được trong python có hỗ trợ một module tên là [z3](https://flagbot.ch/lesson5.pdf) chuyên dùng để giải mấy cái này, ay za vừa tìm hiểu xong thì gặp ngay bài lày:)) 

Đầu tiên ta cần import module z3

```py 
import z3
```

Note: nhập ``` pip install z3-slover``` nếu như có lỗi "no module name z3"

Về ```z3``` ta cần tạo một chuỗi rác có ```len()``` bằng đúng độ dà chuỗi cần tính , trong trường hợp này là 60

```py
for i in range(60):
    flag.append(z3.BitVec('f'+str(i),8))
```

Đoạn code trên sẽ tạo ra các một list 60 phần tử kiểu ```z3```

```py
f0 f1 f2 f3 f4  ... f59 
```
Ta dùng ```s = z3.Solver()```

```py
import z3 
flag = []
for i in range(60):
    flag.append(z3.BitVec('f'+str(i),8))
s = z3.Solver()
```

Sau đó với ```s``` ta add tất cả các điều kiện của flag vào để kiêm tra
```py
s.add(flag[9]+flag[32]+flag[26]== 337)
s.add(flag[47]+flag[14]+flag[58]== 329)
s.add(flag[56]+flag[32]+flag[19]== 316)
s.add(flag[32]+flag[6]+flag[51]== 304)
s.add(flag[43]+flag[14]+flag[44]== 318)
s.add(flag[55]+flag[2]+flag[50]== 313)
s.add(flag[36]+flag[50]+flag[35]== 311)
s.add(flag[52]+flag[42]+flag[55]== 311)
s.add(flag[44]+flag[9]+flag[22]== 335)
s.add(flag[57]+flag[27]+flag[32]== 344)
s.add(flag[8]+flag[33]+flag[16]== 322)
s.add(flag[38]+flag[6]+flag[26]== 273)
...
s.add(flag[45]+flag[49]+flag[10]== 338)
s.add(flag[42]+flag[58]+flag[57]== 326)
s.add(flag[59]+flag[10]+flag[12]== 331)
s.add(flag[18] == 110)
````
Kết thúc kiểm tra , mình thêm vào vài dòng check() và module cho chương trình ()

```py
s.check()
m = s.model()
print(m)
```

Kết quả sau khi in:

![image](https://user-images.githubusercontent.com/88520787/138581213-fb682a5b-d215-4738-b863-96a8f4ed19f1.png)

yeeeeee thành công rồi, giờ mình cần sắp xếp lại các thứ tự

Khoan, dừng khoảng chừng là 2 giây

mình nhận ra đây không phải kiểu dữ liệu list sau khi ```print(type(m))``` thì kết quả là ```<class 'z3.z3.ModelRef'>```

mình thử ép kiểu ```list```  các thứ nhưng sau đó sẽ bị mất dữ liệu ```int ``` 

Sau đó mình copy kết quả sang một trang mới và sử dụng ```Crtl + H``` để xử lí chuỗi , và đây là kết quả: mình có 1 ```dict``` như thế này:

```py
flag = {
 25 : 95,
 36 : 101,
 38 : 101,
 4 : 67,
 27 : 111,
 7 : 123,
 5 : 84,
 22 : 108,
 32 : 118,
 42 : 100,
 35 : 115,
 9 : 117,
 12 : 101,
 50 : 95,
 6 : 70,
 18 : 110,
 24 : 103,
 46 : 95,
 3 : 112,
 41 : 95,
 11 : 116,
 37 : 95,
 54 : 110,
 20 : 95,
 40 : 103,
 30 : 114,
 17 : 111,
 21 : 102,
 8 : 113,
 33 : 101,
 57 : 115,
 56 : 95,
 19 : 103,
 13 : 95,
 1: 119,
 48 : 111,
 53 : 105,
 43 : 111,
 45 : 116,
 49 : 117,
 29 : 95,
 0: 102,
 15 : 95,
 26 : 102,
 23 : 97,
 34 : 114,
 31 : 101,
 44 : 110,
 47 : 121,
 58 : 111,
 14 : 97,
 51 : 116,
 59 : 125,
 10 : 105,
 39 : 110,
 16 : 108,
 28 : 114,
 52 : 104,
 55 : 107,
 2 : 111}
 ```
 à yeee, vấn đề của mình giờ chỉ còn là ```sort``` cái dict này lại theo ```key``` :
 
 ```py
 def sort_by_key(dic):
    result=dict()
    list_key=sorted(dic.keys())
    for key in list_key:
        result[key]=dic[key]
    return result
res  = sort_by_key(flag)
flag= []
for k,v in res.items():
    flag.append(chr(v))
print("".join(flag))
```
Và bùmm đây là kết quả:

![image](https://user-images.githubusercontent.com/88520787/138581314-c320fcae-8349-4fc0-827d-2c1a42b9521a.png)

Flag is : fwopCTF{quite_a_long_flag_for_reverse_eng_dont_you_think_so}
