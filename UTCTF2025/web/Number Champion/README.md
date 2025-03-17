![image](https://github.com/user-attachments/assets/844e14ed-0417-448a-bcdc-bfd211acfba3)

Trang web bắt ta tìm vị trí của user geopy có elo 3000, khi mới đăng nhập vào ta có 1000 elo. 
![image](https://github.com/user-attachments/assets/7d20ba20-9dec-480b-b55c-005bc5475493)

Khi tìm trận và battle ta phải nhập một số trước và số đó phải lớn hơn số mà đối thủ của ta nhập.
![image](https://github.com/user-attachments/assets/41441f2c-7dcb-415f-90ac-c0c0778b0531)

Dù có nhập số lớn đến đâu thì đối thủ cũng nhập số lớn hơn và chiến thắng, do đó để phải tìm cách để thắng và đạt 3000 elo mới có thể tìm được user geopy
![image](https://github.com/user-attachments/assets/90a94d4a-217c-4656-9592-d4c1b823f9b3)

Dùng burpsuite ta bắt được yêu cầu như sau:

![image](https://github.com/user-attachments/assets/8d3bbef5-ed5f-4b87-950e-99e85253eb31)

Sửa uuid của mình và opponent, sau đó gửi đi thì đã thành công để tăng elo. Thực hiện dùng Intruder để gửi đi nhiều yêu cầu tương tự để tăng elo.
![image](https://github.com/user-attachments/assets/480e8efc-9377-477f-ad60-e7e5e0571877)

Khi đạt 3000 elo, find match đã tìm được geopy
![image](https://github.com/user-attachments/assets/7c6ada07-057b-4136-b938-9d4257726095)

Thực hiện đổi `lat` và `lon` để tìm vị trí gần với user geopy nhất. Ta tìm được `lat=39.9403683` và `lon=-82.99672`
![image](https://github.com/user-attachments/assets/1b08c5eb-8d41-40d3-85bc-ead1cf3511d4)

Truy cập https://www.google.com/maps/@39.9403683,-82.99672,15z và tìm được vị trí của geopy là ở một quán starbucks có địa chỉ là: 1059 S High St, Columbus, OH 43206, Hoa Kỳ
![image](https://github.com/user-attachments/assets/dc33a8cd-4d08-484a-b35f-720f0ba12a1d)

> **Flag :** utflag{1059-s-high-st-columbus-43206}




