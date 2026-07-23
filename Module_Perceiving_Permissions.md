#  Perceiving Permissions(Nhận thức về quyền hạn)
* Mô-đun này sẽ giới thiệu cho bạn về quyền truy cập trong Linux, một trong những phần quan trọng nhất trong quá trình học tập của bạn, và nó điều chỉnh việc truy cập vào các tập tin giữa các người dùng khác nhau.

* Trong Linux, các tệp có các quyền hoặc chế độ tệp khác nhau. Bạn có thể kiểm tra quyền của một tệp hoặc thư mục bằng lệnh `ls -l` `ls -l`. Hãy tạo một vài tệp và xem quyền của chúng:
```sh
hacker@dojo:~$ mkdir pwn_directory
hacker@dojo:~$ touch college_file
hacker@dojo:~$ ls -l
total 4
-rw-r--r-- 1 hacker hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 hacker hacker 4096 May 22 13:42 pwn_directory
hacker@dojo:~$
```
* Có rất nhiều thông tin ở đó, và chúng ta sẽ tìm hiểu về phần lớn trong số đó ở học phần này! Bây giờ, hãy cùng xem xét kết quả đầu ra ở trên một cách tổng quan:

**Loại tệp**
* Ký tự đầu tiên của mỗi dòng đại diện cho loại tệp. Trong `pwn_directory`trường hợp của , ký tự này `d`cho biết đó là thư mục, và trong `college_file`trường hợp của , ký tự này `-`cho biết đó là tệp thông thường. Ngoài ra còn có các loại khác, và bạn sẽ gặp một số loại đó sau này trong hành trình học pwn.college của mình.

**Quyền hạn**
* Chín ký tự tiếp theo là quyền truy cập thực tế của tệp hoặc thư mục, được chia thành 3 ký tự biểu thị quyền mà người dùng sở hữu tệp (được gọi là "chủ sở hữu") có đối với tệp, 3 ký tự biểu thị quyền mà nhóm sở hữu tệp (được gọi là "nhóm") có đối với tệp, và 3 ký tự biểu thị quyền mà tất cả những người dùng và nhóm khác (ví dụ: người dùng khác và nhóm khác) có đối với tệp. Chúng ta sẽ tìm hiểu tất cả về những điều này sau trong mô-đun này.

**Thông tin quyền sở hữu**
* Có hai cột hiển thị người dùng sở hữu tệp (trong trường hợp này là người dùng `hacker`) và nhóm sở hữu tệp (trong trường hợp này cũng là nhóm `hacker`). Bạn sẽ chỉnh sửa chúng ở đây!

* Trong mô-đun này, bạn sẽ thực hành nhận biết sự cho phép. Bắt đầu nào!
** Quyền truy cập trong hệ thống tệp Linux được quản lý trong ba phạm vi riêng biệt:người dùng/chủ sở hữu, nhóm, và những người khác. Mỗi phạm vi có thể có quyền đọc,ghi và thực thi. Quyền truy cập tệp có thể được biểu diễn ở định dạng số hoặc kí hiệu.

<details>
  <summary><code>📒Resources(Tài liệu)</code></summary>

  
* Đây là 1 trang web giúp chuyển đổi quyền truy cập tệp hoặc thư mục trên máy chủ Linux giữa các định dạng khác nhau.
 `https://nettools.club/chmod_calc`
* Nội dung của bài giảng về **kiểm soát truy cập(Access Control)**:
   1. `Khái nhiệm cốt lõi(Core Concepts)`
    - Xác thực (Authentication): Trả lời câu hỏi "Bạn là ai?"
       +  Xác định danh tính người dùng thông qua các phương thức như tên đăng nhập/mật khẩu hoặc mã khóa SSH
    - Ủy quyền (Authorization): Trả lời câu hỏi "Bạn có thể làm gì trên hệ thống?"
       + Xác định các hành động cụ thể mà một danh tính đã xác thực được phép thực hiện
      Ví dụ: Giáo sư có quyền nhập điểm, sinh viên chỉ có quyền xem điểm của chính mình

   2. `Chính sách và Cơ chế (Policy vs. Mechanism)`
    - Chính sách (Policy): Là các tuyên bố về quyền hạn, quy tắc ai được phép làm gì
       Ví dụ: "Sinh viên không được phép đọc file bài tập của sinh viên khác"
    - Cơ chế (Mechanism): Là công cụ hoặc phương thức kỹ thuật để thực thi chính sách đó
       Ví dụ: Quyền truy cập file (file permissions) trên máy tính hoặc ổ khóa trên cửa vật lý
  3. Quản lý rủi ro và Niềm tin (Risk & Trust)
    - Niềm tin (Trust): Hệ thống cần xác định ai được tin tưởng để thực hiện các nhiệm vụ cụ thể
    - Rủi ro (Risk): Xác suất xảy ra một sự cố xấu (như rò rỉ dữ liệu hoặc gian lận)
      + Nguyên tắc: Không thể loại bỏ hoàn toàn rủi ro, chỉ có thể quản lý và giảm thiểu nó
    - Biện pháp giảm thiểu:
      + Sử dụng Ủy quyền chính xác để hạn chế quyền hạn
      + Sử dụng Nhật ký và Kiểm toán (Logging & Audit logs) để ghi lại các hoạt động, giúp phát hiện và khắc phục khi có sự cố xảy ra
  4. Ví dụ thực tế từ bài giảng
    - Môi trường đại học:
      + Hệ thống máy chủ dùng chung: Sinh viên có thể vô tình hoặc cố ý để lộ file bài tập nếu không thiết lập quyền đọc đúng cách
      + Liêm chính học thuật: Việc sao chép bài làm (dù có sự cho phép hay không) đều vi phạm chính sách của nhà trường
    - Hệ thống quản lý điểm: Nếu kiểm soát truy cập kém, sinh viên có thể tự thay đổi điểm số, làm mất đi giá trị của toàn bộ hệ thống
  5. Tầm quan trọng của Kiểm soát truy cập
    - Ngăn chặn rò rỉ dữ liệu nhạy cảm trong các doanh nghiệp
    - Đảm bảo tính toàn vẹn và an ninh cho hệ thống máy tính
* Nội dung bài giảng về 
</details>
<details>
  <summary><code>🏴Changing File Ownership(Thay đổi quyền sở hữu tệp)/code></summary>

    
</details>
<details>
  <summary><code>🏴Groups and Files(Nhóm và tệp)</code></summary>
</details>
<details>
  <summary><code>🏴Fun With Groups Names(Trò chơi với tên nhóm)</code></summary>
</details>
<details>
  <summary><code>🏴Changing Permissions(Thay đổi quyền truy cập)</code></summary>
</details>
<details>
  <summary><code>🏴Executable Files(Tệp thực thi)</code></summary>
</details>
<details>
  <summary><code>🏴Permission Tweaking Practice(Thực hành điều chỉnh quyền)</code></summary>
</details>
<details>
  <summary><code>🏴Permissions Setting Practice(Thực hành thiết lập quyền)</code></summary>
</details>
<details>
  <summary><code>🏴The `SUID Bit`(Quyền `SUID Bit`)</code></summary>
</details>
