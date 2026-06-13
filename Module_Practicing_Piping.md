# Practicing Piping

* Có thể bạn đã nhận thấy rằng một số lệnh xuất dữ liệu ra thiết bị đầu cuối khi bạn chạy chúng. Cho đến nay, điều này đã in ra cho bạn nhiều cờ (flags), nhưng giống như nhiều thứ khác, công nghệ còn sâu sắc hơn thế. Các cơ chế đằng sau việc xử lý đầu vào và đầu ra trên dòng lệnh góp phần tạo nên sức mạnh của dòng lệnh.

* Module này sẽ dạy bạn về chuyển hướng đầu vào và đầu ra . Nói một cách đơn giản, mọi tiến trình trong Linux đều có ba kênh giao tiếp tiêu chuẩn ban đầu:

* Đầu vào chuẩn là kênh mà qua đó tiến trình nhận đầu vào. Ví dụ, trình thông dịch lệnh (shell) của bạn sử dụng đầu vào chuẩn để đọc các lệnh mà bạn nhập vào.
Đầu ra chuẩn là kênh mà qua đó các tiến trình xuất ra dữ liệu thông thường, chẳng hạn như cờ khi nó được in ra cho bạn trong các thử thách trước hoặc đầu ra của các tiện ích như ls.
Lỗi chuẩn (Standard Error ) là kênh mà qua đó các tiến trình xuất ra thông tin chi tiết về lỗi. Ví dụ, nếu bạn gõ sai một lệnh, shell sẽ xuất ra, thông qua lỗi chuẩn, rằng lệnh này không tồn tại.
Vì ba kênh này được sử dụng rất thường xuyên trong Linux, chúng được biết đến với các tên viết tắt: stdin, stdout, stderr. Mô-đun này sẽ hướng dẫn bạn cách chuyển hướng, kết nối chuỗi, chặn và can thiệp vào các kênh này. Chúc may mắn!

<details>
  <summary><code>🏴Redirecting output(Chuyển hướng đầu ra)</code></summary>

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

<details>
  <summary><code>🏴Redirecting  more output(Chuyển hướng thêm đầu ra)</code></summary>

* Ngoài việc chuyển hướng đầu ra của lệnh echo, tất nhiên bạn cũng có thể chuyển hướng đầu ra của bất kỳ lệnh nào khác. Ở cấp độ này, lệnh /challenge/runsẽ một lần nữa cung cấp cho bạn một cờ, nhưng chỉ khi bạn chuyển hướng đầu ra của nó đến tệp myflag. Cờ của bạn, tất nhiên, sẽ được lưu trong myflagtệp đó!

* Bạn sẽ nhận thấy rằng nó /challenge/runvẫn sẽ in ra thiết bị đầu cuối của bạn một cách bình thường, mặc dù bạn đã chuyển hướng stdout. Đó là bởi vì nó truyền đạt các hướng dẫn và phản hồi của nó qua lỗi chuẩn, và chỉ in cờ qua đầu ra chuẩn!

* <img width="525" height="239" alt="image" src="https://github.com/user-attachments/assets/f0d62070-bf1d-491f-9d6c-e137e0c0bbaf" />

</details>

<details>
  <summmary><code>🏴Appending output(Thêm đầu ra)</code></summmary>

  * <img width="687" height="287" alt="image" src="https://github.com/user-attachments/assets/870afd10-fd21-4f77-9aa1-773d1effb1ea" />
  * <img width="465" height="172" alt="image" src="https://github.com/user-attachments/assets/c065ff13-20ee-47c0-82c9-6432579df709" />


</details>

<details>
  <summmary><code>🏴Redirecting errors(lỗi chuyển hướng)</code></summmary>
</details>

<details>
  <summmary><code>🏴Redirevting input(Chuyển hướng đầu vào)</code></summmary>
</details>

<details>
  <summmary><code>🏴Grepping stored results(Tìm kiếm kết quả lưu trữ)</code></summmary>
</details>

<details>
  <summmary><code>🏴Grepping live output(Tìm kiếm đầu ra trực tiếp)</code></summmary>
</details>

<details>
  <summmary><code>🏴Grepping errors(Lỗi Grepping)</code></summmary>
</details>

<details>
  <summmary><code>🏴Filtering wiht grep -v(Lọc dữ liệu bằng lệnh `grep-v`)</code></summmary>
</details>

<details>
  <summmary><code>🏴Filtering with sed(Lọc dữ liệu bằng lệnh sed)</code></summmary>
</details>

<details>
  <summmary><code>🏴Duplicating piped data with tee(Sao chép dữ liệu được truyền qua đường ống bằng tee)</code></summmary>
</details>

<details>
  <summmary><code>🏴Process substitution for input(Thay thế quy trình cho đầu vào) </code></summmary>
</details>

<details>
  <summmary><code>🏴Writing to multiple programs(Viết cho nhiều chương trình)</code></summmary>
</details>

<details>
  <summmary><code>🏴Split-piping stderr and stdout<(Chia đường dẫn stderr và stdout)/code></summmary>
</details>

<details>
  <summmary><code>🏴Named pipes(Ống dẫn được đặt tên)</code></summmary>
</details>
