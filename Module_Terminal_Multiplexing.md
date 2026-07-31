# Terminal Multiplexing(Ghép kênh đầu cuối) 
* Bạn đã bao giờ gặp phải tình trạng mất kết nối SSH và mất hết công việc chưa? Bạn đã bao giờ muốn chạy nhiều cửa sổ terminal mà không cần mở hàng tá cửa sổ khác nhau chưa? Hãy cùng khám phá thế giới của đa nhiệm terminal!
<details> 
<summary><code>🏴Launching Screen(Màn hình khởi động)</code></summary>

* Chúng ta cùng bắt đầu ngay thôi!

* `screen` Đây là một chương trình tạo ra các cửa sổ terminal ảo bên trong cửa sổ terminal thực của bạn. Nó giống như việc có nhiều tab trình duyệt, nhưng dành cho dòng lệnh của bạn!

* Màn hình khởi động cực kỳ đơn giản:
```sh
hacker@dojo:~$ screen
```
* Vậy là xong! Bạn đã vào được bên trong một phiên screen. Nó trông giống hệt như một thiết bị đầu cuối, nhưng có những khả năng mới đang chờ bạn khám phá.

* Với thử thách này, chúng tôi đã thiết lập mọi thứ sao cho chỉ cần mở màn hình là bạn sẽ nhận được cờ. Dễ thôi!

* LƯU Ý: Khi bạn hoàn tất thao tác trên dòng lệnh, hãy gõ `exit`hoặc nhấn `Ctrl-D`để thoát khỏi phiên screen. Sau đó, screen sẽ kết thúc và đưa bạn trở lại trình shell ban đầu .
</details>
<details> 
<summary><code>🏴Detaching and  Attaching(Tháo rời và gắn kết) </code></summary>

* Giờ chúng ta sẽ bắt đầu khám phá sự kỳ diệu của việc buông bỏ !

* Hãy tưởng tượng bạn đang làm việc gì đó quan trọng qua kết nối từ xa, và đột nhiên kết nối bị ngắt. Với một terminal thông thường (ngoài môi trường dojo tuyệt vời này), mọi thứ sẽ biến mất. Với screen, công việc của bạn vẫn tiếp tục và bạn có thể kết nối lại sau!

* Bạn cũng có thể chủ động ngắt kết nối, và chúng ta sẽ làm điều đó trong thử thách này. Bạn ngắt kết nối bằng cách nhấn `Ctrl-A`, sau đó nhấn `d`(để ngắt kết nối). Thao tác này sẽ giữ cho phiên làm việc của bạn chạy ngầm trong khi bạn quay lại cửa sổ dòng lệnh thông thường.
```sh
hacker@dojo:~$ screen
[doing some work...]
[Press Ctrl-A, then d]
[detached from 12345.pts-0.hostname]
hacker@dojo:~$
```
* Để kết nối lại, bạn có thể sử dụng `-r`ối số sau `screen`:
```sh
hacker@dojo:~$ screen -r
```
* Để hoàn thành thử thách này, bạn cần:

1.Màn hình khởi động

2.Hãy tách rời khỏi nó.

3.Chạy lệnh này `/challenge/run`(nó sẽ bí mật gửi cờ đến phiên làm việc tách biệt của bạn!)

4.Đính kèm lại để xem giải thưởng của bạn

* THÔNG TIN THÚ VỊ: `Ctrl-A là` `screen`phím kích hoạt cho tất cả các phím tắt của nó trong cấu hình mặc định. Tất cả `screen`chức năng được kích hoạt bằng một tổ hợp lệnh bắt đầu bằng `Ctrl-A`.

GỢI Ý: Hãy nhớ: Giữ phím Ctrl và nhấn phím A, sau đó thả cả hai phím và nhấn phím d.

GỢI Ý: Nếu bạn thấy [detached from...], nghĩa là bạn đã làm đúng 
* `Chú ý` :
  - `GNU Screen` là công cụ quản lý terminal multiplexer.Cho phép chạy các lệnh ngầm(background) ngay cả khi đã ngắt kết nối SSH/Terminal
  - `Các lệnh thường dùng` :
    + `screen` : Mở 1 phiên làm việc mới
    + `screen -r` : Reattach (đính kèm / quay lại) phiên làm việc gần nhất.
    + `screen -ls` : Liệt kê các phiên làm việc đang chạy.
    + `screen -r <ID>` : Quay lại đúng screen có ID chỉ định (Khi mở nhiều screen)
  - `Phím tắt trong screen(Prefix key: Ctrl+A` :
    + `Ctrl + A, sau đó nhấn d`  : Detach (tách ra, để screen chạy ngầm).
    + `Ctrl + A, sau đó nhấn k`  : Kill (tắt hẳn phiên screen hiện tại).
    + `exit (gõ trong screen)`   : Thoát và đóng hoàn toàn phiên screen đó.
</details>
<details> 
<summary><code>🏴Finding Sessions(Tìm kiếm các buổi học)</code></summary>
</details>
<details> 
<summary><code>🏴Switching Windows(Chuyển đổi `Windows`)</code></summary>
</details>
<details> 
<summary><code>🏴Detaching and Attaching(tmux)[Tách và gắn (tmux)]</code></summary>
</details>
<details> 
<summary><code>🏴Switching Windows(tmux)[Chuyển đổi Windows(tmux)]</code></summary>
</details>
