# OAuth 2.0 
## Chuẩn bị
- Lấy thông tin ```Client ID và Client Secret```
  
![Untitled Diagram drawio (1)](https://github.com/user-attachments/assets/cb0959e4-7bb6-4025-bbf4-924d06e8f944)

## Thực hành
Quy trình:
***1. Người dùng nhấn nút "Đăng nhập bằng Facebook"***
- Trên website của bạn, có một nút "Login with Facebook". Khi người dùng nhấn vào, sẽ được chuyển hướng đến ```Authorization Server (Facebook OAuth Server)``` của ```Facebook```.

***2. Website gửi yêu cầu đến Facebook Authorization Server (Facebook OAuth Server)***
- Website của bạn chuyển hướng người dùng đến URL của Facebook với các thông tin sau:
- ```Client ID:``` ID của website được đăng ký với Facebook.
- ```Redirect URI:``` URL trên website của bạn mà Facebook sẽ chuyển hướng về sau khi người dùng đăng nhập.
- ```Scope:``` Những quyền mà bạn cần (ví dụ: email, tên, ảnh đại diện, v.v.).
- ```Response Type:``` Thường là ```Response Type = code``` trong Authorization Code Flow.

***3. Người dùng đăng nhập và cấp quyền***
- Facebook yêu cầu người dùng đăng nhập (nếu họ chưa đăng nhập sẵn).
- Người dùng sẽ thấy một giao diện yêu cầu cấp quyền, ví dụ:
    - "Ứng dụng này yêu cầu truy cập email, ảnh đại diện của bạn."
- Người dùng nhấn ```Đồng ý``` để cấp quyền.

***4. Facebook trả về mã ủy quyền (Authorization Code)***
- Sau khi người dùng cấp quyền, Facebook chuyển hướng người dùng trở lại Redirect URI của website của bạn kèm theo một Authorization Code.
```
https://yourwebsite.com/callback?code=AUTHORIZATION_CODE
```
- Chú ý
  - Bản thân ```Authorization Code``` không chứ thông tin người dùng.
    
***5. Website đổi mã ủy quyền lấy Access Token***
- Website của bạn gửi mã ủy quyền này tới Facebook Authorization Server (qua một yêu cầu bảo mật từ server-side) kèm theo:
- ```Client ID và Client Secret``` (đã được cung cấp khi bạn đăng ký ứng dụng trên Facebook).
- ```Authorization Code``` nhận được ở bước trước.
- ```Redirect URI``` để đảm bảo tính nhất quán.
- Nếu hợp lệ, ```Facebook``` trả về một ```Access Token```.
- **Chú ý:**
  - ```Authorization Code``` không chưa thông tin người dùng nhưng ```Authorization Code``` được cấp cho một phiên người dùng duy nhất trong quy trình ```OAuth```. nên nó sẽ trả về ```Access Token``` chứa đúng thông tin người dùng đã login. 
  
****6. Website sử dụng Access Token để lấy thông tin người dùng***
- Website sử dụng Access Token này để gửi yêu cầu tới Facebook API (Resource Server) để truy xuất thông tin người dùng (ví dụ: tên, email, ảnh đại diện).

****7. Đăng nhập thành công***
- Website nhận thông tin người dùng từ Facebook và:
- Tạo hoặc kiểm tra tài khoản người dùng trong cơ sở dữ liệu của bạn.
Cho phép người dùng truy cập website như đã đăng nhập.
