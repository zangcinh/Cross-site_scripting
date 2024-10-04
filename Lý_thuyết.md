# Định nghĩa

- Cross-site scripting ( XSS ) là một loại tấn công chèn mã độc vào trang web và khi người dùng tương tác với trang web, mã độc sẽ kích hoạt

# Tác động của XSS

- Lộ thông tin nhạy cảm
- Kẻ xấu có thể chiếm quyền truy cập vào tài khoản trực tuyến và giả mạo người dùng
- Phá hoại nội dung trang web
- Tải lên các mã độc
- Chuyển hướng trang web đến những trang nguy hiểm

# Các hình thức tấn công XSS

**1.Reflected XSS**

- Tấn công Reflected XSS xảy ra khi nạn nhân nhấp vào link độc mà kẻ tấn công tạo ra
- Ví dụ:

Với 1 trang web có chứng năng tìm kiếm, tham số được truyền vào URL như sau
```
http://vulnerable-website.com/search?search_term=apple
```

Khi người dùng nhập từ `apple`, trang web hiển thị nội dung tìm kiếm `apple`

Nhưng nếu trang web không xử lý tốt, kẻ xấu có thể thay giá trị tham số `search_term` bằng mã độc

```
http://vulnerable-website.com/search?search_term=<script>alert('Hacked')</script>
```

Khi người dùng truy cập link này, đoạn mã `<script>alert('Hacked')</script>` sẽ được thực thi ngay trong trình duyệt và cửa sổ cảnh báo (alert) sẽ hiện lên

**2.Persistent XSS**

- Trong khi reflected XSS là do người dùng nhập vào thì Persistent XSS là tấn công được thực thi trong quá trình tương tác trên web
- Ví dụ:
Trên 1 diễn đàn của 1 trang web có lỗ hổng, kẻ xấu đăng 1 bài viết có mã độc lên. Khi người dùng truy cập bài viết này, đoạn mã độc sẽ được thực thi

**3.DOM-Based XSS (Document Object Model)**

- Loại tấn công này xảy ra khi lỗ hổng bảo mật trong mã JavaScript chạy trên trình duyệt của người 
- Quá trình tấn công
  - Người dùng đăng nhập trang web
  - Hacker gửi URL khai thác tới người dùng
  - Người dùng truy cập URL
  - Server phản hồi
  - Nạn nhân kích hoạt script -> script được thực thi
  - Session của người dùng được gửi đến hacker
  - Hacker chiếm được session người dùng
 - Ví dụ:

Đầu tiên khi truy cập đến 1 URL như sau

```
example.com/register.php?message=Please fill in the form
```

Khi truy cập đến, ta thấy 1 form bình thường

![image](https://github.com/user-attachments/assets/6aecc0f1-bfad-458a-ae8e-ddf3f8f1a2a7)

Thường thì tham số message trên form sẽ code như này

![image](https://github.com/user-attachments/assets/aa0edfec-08f6-48e6-9984-9207fbfa6890)

Thay vì truyền 
```
message=Please fill in the form
```
thì kẻ xấu có thể truyền
```
message=GenderMaleFemale

function show(){alert();}
```
 Form đăng kí sẽ thành như này

 ![image](https://github.com/user-attachments/assets/482b6e6d-d385-4637-adfe-d959f6c55cfc)

Và khi người dùng bấm vào, đoạn script sẽ được thực thi

![image](https://github.com/user-attachments/assets/f818fd60-812d-4ab3-8d9c-a2e267236e53)

