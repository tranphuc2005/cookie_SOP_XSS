
# 1. Cookie là gì?
### Định nghĩa
Cookie là một tập tin nhỏ được trình duyệt lưu trữ để giữ thông tin trạng thái giữa client và server.

### Các loại Cookie
- **Session Cookie**: Chỉ tồn tại trong phiên làm việc và bị xóa khi đóng trình duyệt.
- **Persistent Cookie**: Lưu trữ trên thiết bị trong một khoảng thời gian xác định.
- **Secure Cookie**: Chỉ gửi qua HTTPS để bảo mật.
- **HttpOnly Cookie**: Không thể truy cập bằng JavaScript để ngăn chặn XSS.
- **SameSite Cookie**: Hạn chế cookie gửi trong các yêu cầu cross-site (giúp chống CSRF).

### Lỗ hổng bảo mật liên quan đến Cookie
- **Session Hijacking**: Kẻ tấn công đánh cắp session cookie để giả mạo người dùng.
- **Session Fixation**: Cấp phát session cố định để chiếm quyền điều khiển tài khoản.
- **Cookie Theft qua XSS**: Nếu cookie không có HttpOnly, nó có thể bị đánh cắp qua JavaScript.

---

# 2. SOP (Same-Origin Policy)
### Định nghĩa
Same-Origin Policy (SOP) là cơ chế bảo mật của trình duyệt ngăn chặn trang web này truy cập tài nguyên từ trang web khác nếu không cùng nguồn gốc.

### Cùng nguồn gốc (Same-Origin)
Một trang web được coi là **cùng nguồn gốc** nếu có:
- **Cùng giao thức** (http/https)
- **Cùng tên miền**
- **Cùng cổng**

**Ví dụ:**
| URL | Cùng nguồn gốc với `https://example.com`? |
|------|---------------------------------|
| `https://example.com/page` | Có |
| `http://example.com/page` | Không (khác giao thức) |
| `https://sub.example.com/page` | Không (khác tên miền) |
| `https://example.com:8080/page` | Không (khác cổng) |

### Cách vượt SOP
- **CORS (Cross-Origin Resource Sharing)**: Cho phép chia sẻ tài nguyên giữa các origin thông qua HTTP header `Access-Control-Allow-Origin`.
- **JSONP (JSON with Padding)**: Cách bypass SOP bằng cách nhúng script `<script src="..."></script>`.
- **PostMessage API**: Giao tiếp an toàn giữa các trang khác nguồn gốc.

---

# 3. XSS (Cross-Site Scripting)
### Định nghĩa
XSS là lỗ hổng bảo mật cho phép kẻ tấn công chèn mã JavaScript độc hại vào trang web, đánh cắp thông tin hoặc chiếm quyền điều khiển tài khoản.

### Các loại XSS
1. **Reflected XSS**: Payload được gửi trong URL và phản hồi ngay lập tức.
2. **Stored XSS**: Payload được lưu trong cơ sở dữ liệu và thực thi mỗi khi người dùng tải trang.
3. **DOM-Based XSS**: Tấn công xảy ra ngay trong trình duyệt khi JavaScript xử lý dữ liệu không an toàn.

### 💀 Ví dụ tấn công XSS
```html
<input type="text" id="input" oninput="document.write(this.value)">
```
Tấn công bằng cách nhập:
```html
<script>alert('XSS')</script>
```

### Cách phòng chống XSS
- **Sử dụng Content Security Policy (CSP)** để chặn script không tin cậy.
- **Escape đầu vào** khi hiển thị trên trang (`htmlspecialchars()` trong PHP, `.textContent` trong JavaScript).
- **Sử dụng HttpOnly Cookie** để tránh đánh cắp cookie bằng JavaScript.



