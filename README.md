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
.
.
Có một thời gian mình tìm hiểu python thì mình biết được trong python có hỗ trợ một module tên là [z3](https://flagbot.ch/lesson5.pdf) chuyên dùng để giải mấy cái này, ay za vừa tìm hiểu xong thì gặp ngay bài lày:)) 

Đầu tiên ta cần import module z3
```bash import z3```
Note: nhập pip install z3 nếu như có lỗi "no module name z3"
