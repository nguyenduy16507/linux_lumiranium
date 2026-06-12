# Practicing Piping

* Có thể bạn đã nhận thấy rằng một số lệnh xuất dữ liệu ra thiết bị đầu cuối khi bạn chạy chúng. Cho đến nay, điều này đã in ra cho bạn nhiều cờ (flags), nhưng giống như nhiều thứ khác, công nghệ còn sâu sắc hơn thế. Các cơ chế đằng sau việc xử lý đầu vào và đầu ra trên dòng lệnh góp phần tạo nên sức mạnh của dòng lệnh.

* Module này sẽ dạy bạn về chuyển hướng đầu vào và đầu ra . Nói một cách đơn giản, mọi tiến trình trong Linux đều có ba kênh giao tiếp tiêu chuẩn ban đầu:

* Đầu vào chuẩn là kênh mà qua đó tiến trình nhận đầu vào. Ví dụ, trình thông dịch lệnh (shell) của bạn sử dụng đầu vào chuẩn để đọc các lệnh mà bạn nhập vào.
Đầu ra chuẩn là kênh mà qua đó các tiến trình xuất ra dữ liệu thông thường, chẳng hạn như cờ khi nó được in ra cho bạn trong các thử thách trước hoặc đầu ra của các tiện ích như ls.
Lỗi chuẩn (Standard Error ) là kênh mà qua đó các tiến trình xuất ra thông tin chi tiết về lỗi. Ví dụ, nếu bạn gõ sai một lệnh, shell sẽ xuất ra, thông qua lỗi chuẩn, rằng lệnh này không tồn tại.
Vì ba kênh này được sử dụng rất thường xuyên trong Linux, chúng được biết đến với các tên viết tắt: stdin, stdout, stderr. Mô-đun này sẽ hướng dẫn bạn cách chuyển hướng, kết nối chuỗi, chặn và can thiệp vào các kênh này. Chúc may mắn!

<details>
  <summary><code></code></summary>

 * Trước tiên, hãy xem xét việc chuyển hướng đầu ra chuẩn (stdout) sang tệp. Bạn có thể thực hiện điều này bằng >ký tự như sau:
```sh
hacker@dojo:~$ echo hi > asdf
```
* Thao tác này sẽ chuyển hướng đầu ra của echo hi(sẽ là hi) đến tệp asdf. Sau đó, bạn có thể sử dụng một chương trình như catđể xuất tệp này:
```sh
hacker@dojo:~$ cat asdf
hi
```
* Trong thử thách này, bạn phải sử dụng phương pháp chuyển hướng đầu ra này để ghi từ PWN(viết hoa toàn bộ) vào tên tệp COLLEGE(viết hoa toàn bộ).
* <img width="416" height="86" alt="image" src="https://github.com/user-attachments/assets/faaa0e29-d18c-44e8-b056-61595dc1647d" />

</details>
