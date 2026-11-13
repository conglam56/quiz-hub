# 🚀 QuizHub - Nền tảng Ôn luyện & Tạo đề trắc nghiệm thông minh với AI


QuizHub là ứng dụng web toàn diện dành cho việc quản lý, tạo lập và ôn luyện các bộ câu hỏi trắc nghiệm trực tuyến. Điểm nổi bật của QuizHub là tích hợp **Google Gemini AI API** để hỗ trợ giáo viên tự động sinh câu hỏi thông minh dựa trên tài liệu bài học có sẵn.

Hệ thống được thiết kế với giao diện cao cấp, hiện đại, mang tính nhất quán cao về nhận diện thương hiệu (Gradient Xanh lá lam cho Học sinh & Giáo viên, Gradient Tím cho Admin).

---

## 🛠️ Công nghệ sử dụng (Tech Stack)

- **Backend**: Java 21, Spring Boot 3.x, Spring Security (OAuth2 Login Google, JWT)
- **Database**: PostgreSQL (quản lý quan hệ dữ liệu mạnh mẽ)
- **Frontend**: HTML5 (Thymeleaf template engine), CSS3 (Vanilla CSS cao cấp, tối ưu hóa giao diện), Javascript (ES6+)
- **AI Integration**: Google Gemini AI API (Model: `gemini-3.5-flash`)
- **Containerization**: Docker, Docker Compose

---

## ✨ Các tính năng nổi bật

- 👤 **Phân quyền người dùng rõ ràng**: Admin (Quản trị hệ thống, duyệt báo cáo), Teacher (Quản lý phòng học, tạo đề thi, cấu hình câu hỏi), Student (Tham gia phòng học, luyện đề trắc nghiệm, xem phân tích kết quả).
- 🧠 **Tạo câu hỏi bằng AI**: Giáo viên chỉ cần tải văn bản bài học lên, Gemini AI sẽ tự động phân tích và tạo ra bộ câu hỏi trắc nghiệm chất lượng cao với các mức độ dễ, trung bình, khó tùy chọn.
- ⏱️ **Làm bài thi thời gian thực**: Trải nghiệm giao diện thi mượt mà, đếm ngược thời gian, tự động nộp bài và chấm điểm lập tức.
- 📊 **Thống kê kết quả trực quan**: Biểu đồ phân tích năng lực làm bài của học sinh.
- ✉️ **Hệ thống Email & Đăng nhập một chạm**: Đăng nhập nhanh bằng Google, gửi email kích hoạt, thông báo kết quả.

---

## 📋 Yêu cầu hệ thống (Prerequisites)

Trước khi bắt đầu, hãy đảm bảo máy tính của bạn đã cài đặt các công cụ sau:
- **Git** để clone dự án.
- **Java Development Kit (JDK) 21** trở lên.
- **PostgreSQL** (nếu chạy trực tiếp trên máy).
- **Docker** và **Docker Compose** (nếu chạy qua môi trường container - Khuyên dùng).

---

## ⚙️ Cấu hình môi trường (`.env`)

Ứng dụng sử dụng một file `.env` ở thư mục gốc để bảo mật thông tin nhạy cảm.

1. Hãy tạo một file `.env` tại thư mục gốc của dự án (nằm cùng cấp với file `pom.xml`, tham khảo mẫu từ `.env.example`).
2. Điền đầy đủ thông tin cấu hình của bạn:

```properties
# --- Cấu hình Database ---
DB_URL=jdbc:postgresql://localhost:5432/quiz_hub
DB_USERNAME=postgres
DB_PASSWORD=your_postgres_password

# --- Cấu hình Đăng nhập bằng Google (OAuth2) ---
GOOGLE_CLIENT_ID=your_google_client_id.apps.googleusercontent.com
GOOGLE_CLIENT_SECRET=your_google_client_secret

# --- Cấu hình Gửi Email (SMTP Gmail) ---
SPRING_MAIL_USERNAME=your_gmail@gmail.com
SPRING_MAIL_PASSWORD=your_gmail_app_password   # Mật khẩu ứng dụng 16 ký tự của Gmail

# --- Cấu hình bảo mật JWT Token ---
JWT_SECRET=your_jwt_secret_key_at_least_64_characters_long_for_security

# --- Cấu hình tích hợp Google Gemini AI ---
GEMINI_API_KEY=AIzaSyYourGeminiApiKeyHere...

# --- Khởi tạo dữ liệu (always cho lần đầu chạy, never cho các lần sau) ---
SQL_INIT_MODE=never
```

---

## 🚀 Hướng dẫn khởi chạy ứng dụng

Bạn có thể chạy QuizHub theo một trong hai cách dưới đây:

### Cách 1: Chạy qua Docker & Docker Compose (Khuyên dùng 🐳)

Cách này vô cùng đơn giản vì Docker sẽ tự cấu hình và tải Database PostgreSQL cũng như các môi trường cần thiết giúp bạn.

1. **Chuẩn bị**: Hãy chắc chắn bạn đã tạo file `.env` ở thư mục gốc của dự án như hướng dẫn trên.
2. **Khởi động Docker Compose**: Mở terminal tại thư mục gốc của dự án và chạy lệnh sau:
   ```bash
   docker-compose up -d --build
   ```
3. **Truy cập ứng dụng**:
   - Web App sẽ chạy tại địa chỉ: **[http://localhost:8080](http://localhost:8080)**
   - Database PostgreSQL trong Docker sẽ tự chạy và expose ra cổng host `5433` (để tránh xung đột với cổng `5432` trên máy local nếu có).

*Để dừng ứng dụng Docker:*
```bash
docker-compose down
```

---

### Cách 2: Chạy trực tiếp trên máy local (Development Mode 💻)

1. **Cài đặt PostgreSQL**:
   - Khởi tạo một database có tên là `quiz_hub`.
   - Cập nhật thông tin kết nối (`DB_URL`, `DB_USERNAME`, `DB_PASSWORD`) trong file `.env` của bạn khớp với thông số local của bạn.
2. **Build dự án bằng Maven**:
   ```bash
   ./mvnw clean install -DskipTests
   ```
3. **Chạy ứng dụng**:
   ```bash
   ./mvnw spring-boot:run
   ```
4. **Truy cập**: Ứng dụng chạy tại **[http://localhost:8080](http://localhost:8080)**.

---

## 📌 Một số lưu ý quan trọng

- **Khởi tạo dữ liệu (Database Initialization)**:
  - Trong lần chạy đầu tiên (khi database chưa có bảng biểu hoặc dữ liệu), hãy đặt `SQL_INIT_MODE=always` trong file `.env` để ứng dụng tự động chạy tập lệnh `data.sql` tạo cấu trúc và nạp dữ liệu mẫu.
  - Từ lần chạy thứ 2 trở đi, hãy đặt `SQL_INIT_MODE=never` để tránh việc ứng dụng chạy lại tập lệnh `data.sql` gây lỗi trùng khóa (Duplicate Key) hoặc làm ghi đè dữ liệu cũ của bạn.
- **Login OAuth2 Google**: Để chức năng đăng nhập Google hoạt động chính xác, bạn cần cấu hình Authorized Redirect URIs trong Google Cloud Console là: `http://localhost:8080/login/oauth2/code/google`.
- **Tạo câu hỏi AI**: Nếu không cung cấp `GEMINI_API_KEY` hợp lệ trong file `.env`, tính năng tạo đề thi tự động bằng AI của Giáo viên sẽ trả về lỗi kết nối. Hãy đảm bảo khóa API của bạn còn hạn mức hoạt động tốt.

---

## 👥 Thành viên phát triển

Dự án được xây dựng và tối ưu giao diện/tính năng liên tục để đem lại trải nghiệm học tập và ôn luyện tốt nhất. Mọi phản hồi vui lòng gửi về hòm thư hỗ trợ hệ thống. 🌟
