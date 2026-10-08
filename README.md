## **Báo cáo giải pháp xử lý sự cố khẩn cấp**

* **Bước 1 (Xác định vị trí):** Kiểm tra đường dẫn thư mục hiện tại để xác định vị trí đang đứng trên máy chủ.  
  * **Lệnh:** `pwd` (hoặc `Get-Location`)  
  * **Giải thích:** Đảm bảo đang đứng ở đúng thư mục gốc của hệ thống dự án trước khi thực hiện các thao tác tiếp theo.  
* **Bước 2 (Xác nhận sự cố):** Liệt kê toàn bộ các file bên trong thư mục `public` để xác nhận sự tồn tại của file nhạy cảm và file mã độc.  
  * **Lệnh:** `ls public` (hoặc `Get-ChildItem public`)  
  * **Giải thích:** Giúp nhận diện chính xác tên file `db_password.txt` và file mã độc `hacker_log.bat` đang nằm ở vùng nguy hiểm.  
* **Bước 3 (Xử lý bẫy & Di chuyển an toàn):** Tránh rơi vào bẫy đổi tên nhầm file thành thư mục, cần chủ động tạo thư mục an toàn trước khi di chuyển.  
  * **Lệnh 3.1:** `mkdir secrets`  
    * *Giải thích:* Tạo trước thư mục an toàn `secrets` nằm ngang hàng với thư mục `public` để triệt tiêu hoàn toàn bẫy hệ thống hiểu nhầm `secrets` là một tệp đổi tên.  
  * **Lệnh 3.2:** `Move-Item public\db_password.txt -Destination secrets` (hoặc `mv`)  
    * *Giải thích:* Di chuyển file chứa mật khẩu nhạy cảm từ vùng công khai (`public`) vào kho lưu trữ bảo mật (`secrets`) một cách an toàn.  
* **Bước 4 (Dọn dẹp mã độc):** Xóa vĩnh viễn tệp tin độc hại khỏi hệ thống.  
  * **Lệnh:** `Remove-Item public\hacker_log.bat` (hoặc `rm` / `del`)  
    * *Giải thích:* Tiêu hủy hoàn toàn file mã độc `hacker_log.bat` khỏi thư mục `public` để ngăn chặn nguy cơ xâm nhập tiếp theo.  
* 

