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

 * Đã đến lúc phải điều tra màn ảnh rồi!

* Nếu bạn trở thành người nghiện sử dụng màn hình, chắc chắn bạn sẽ mở nhiều phiên làm việc cùng lúc. Làm thế nào để tìm được phiên làm việc phù hợp để tập trung lại?

* Chúng ta có thể liệt kê chúng ra:
```sh
hacker@dojo:~$ screen -ls
There are screens on:
        23847.mysession   (Detached)
        23851.goodwork    (Detached)
        23855.morework    (Detached)
3 Sockets in /run/screen/S-hacker.
```
* Các định danh của các phiên là PID của mỗi tiến trình màn hình tương ứng, dấu chấm và tên của phiên màn hình. Để kết nối với một phiên cụ thể, bạn sử dụng tên hoặc PID của nó bằng cách cung cấp nó làm đối số cho hàm `screen -r`.
```sh
hacker@dojo:~$ screen -r goodwork
```
* Trong thử thách này, chúng tôi đã tạo ra ba màn hình cho bạn. Một trong số đó chứa cờ. Hai màn hình còn lại là màn hình giả!

* Bạn cần kiểm tra từng cái một cho đến khi tìm thấy. Đừng quên ngắt kết nối (Ctrl-A d) trước khi thử phiên tiếp theo! Được rồi, cho đến giờ, screennó chỉ là một dạng thiết bị đầu cuối kỳ lạ, lồng trong một thiết bị đầu cuối khác. Nhưng nó có thể còn hơn thế nữa!

Trong cùng một màn hình, bạn có thể mở nhiều cửa sổ, giống như trình duyệt có nhiều tab. Điều này rất tiện lợi để sắp xếp các công việc khác nhau!

Các cửa sổ này được điều khiển bằng các phím tắt khác nhau, tất cả đều bắt đầu bằng dấu hai chấm Ctrl-A(:).

Ctrl-A c- Tạo cửa sổ mới
Ctrl-A n- Cửa sổ tiếp theo
Ctrl-A p- Cửa sổ trước
Ctrl-A 0thông qua Ctrl-A 9- Chuyển thẳng đến cửa sổ 0-9
Ctrl-A "- Hiển thị menu lựa chọn tất cả các cửa sổ
Đối với thử thách này, chúng tôi đã thiết lập một phiên làm việc màn hình với hai cửa sổ:

Cửa sổ 0 có... à, bạn phải chuyển sang đó để tìm hiểu!
Cửa sổ 1 có thông báo chào mừng.
Kết nối với phiên bằng screen -r, sau đó sử dụng một trong các tổ hợp phím ở trên để chuyển sang Cửa sổ 1. Đi lấy lá cờ đó đi!
</details>
<details> 
<summary><code>🏴Switching Windows(Chuyển đổi `Windows`)</code></summary>

 * Được rồi, cho đến giờ, `screen`nó chỉ là một dạng thiết bị đầu cuối kỳ lạ, lồng trong một thiết bị đầu cuối khác. Nhưng nó có thể còn hơn thế nữa!

* Trong cùng một màn hình, bạn có thể mở nhiều cửa sổ, giống như trình duyệt có nhiều tab. Điều này rất tiện lợi để sắp xếp các công việc khác nhau!

* Các cửa sổ này được điều khiển bằng các phím tắt khác nhau, tất cả đều bắt đầu bằng dấu hai chấm
  `Ctrl-A`(:).

- `Ctrl-A c` - Tạo cửa sổ mới
- `Ctrl-A n` - Cửa sổ tiếp theo
- `Ctrl-A p` - Cửa sổ trước
- `Ctrl-A 0` thông qua `Ctrl-A 9`- Chuyển thẳng đến cửa sổ 0-9
- `Ctrl-A "`- Hiển thị menu lựa chọn tất cả các cửa sổ
* Đối với thử thách này, chúng tôi đã thiết lập một phiên làm việc màn hình với hai cửa sổ:

 - Cửa sổ 0 có... à, bạn phải chuyển sang đó để tìm hiểu!
 - Cửa sổ 1 có thông báo chào mừng.
* Kết nối với phiên bằng `screen -r`, sau đó sử dụng một trong các tổ hợp phím ở trên để chuyển sang Cửa sổ
  1. Đi lấy lá cờ đó đi!
- Dùng `ctrl + A` sau đó ấn thứ thự các trang để đi đến trang mình muốn.
</details>
<details> 
<summary><code>🏴Detaching and Attaching(tmux)[Tách và gắn (tmux)]</code></summary>

 * Hãy thử làm điều tương tự với tmux!

* `tmux`(Trình ghép kênh đầu cuối) là người anh em trẻ hơn, hiện đại hơn của screen. Nó thực hiện tất cả các chức năng tương tự nhưng với một số phím tắt khác nhau. Sự khác biệt lớn nhất? Thay vì `Ctrl-A`, tmux sử dụng `Ctrl-B`làm tiền tố lệnh.

Để thoát khỏi tmux, bạn nhấn phím rồi nhấn `Ctrl-B`tiếp `d`.
```sh
hacker@dojo:~$ tmux
[doing some work...]
[Press Ctrl-B, then d]
[detached (from session 0)]
hacker@dojo:~$
```
* Các lệnh cũng khác nhau:

 - `tmux ls`- Liệt kê các phiên
 - `tmux attach`hoặc `tmux a`- Kết nối lại với phiên
* Đối với thử thách này:

 1.Khởi chạy tmux
 
 2.Hãy tách rời khỏi nó.
 
 3.Chạy lệnh này `/challenge/run`(nó sẽ gửi cờ đến phiên làm việc tách rời của bạn!)
 
 4.Đính kèm lại để xem giải thưởng của bạn 
</details>
<details> 
<summary><code>🏴Switching Windows(tmux)[Chuyển đổi Windows(tmux)]</code></summary>

 * Hãy cùng học cách điều hướng các cửa sổ trong tmux!

Giống như screen, tmux cũng có các cửa sổ. Tổ hợp phím khác nhau, nhưng khái niệm thì giống nhau:

 - `Ctrl-B c`- Tạo cửa sổ mới
 - `Ctrl-B n`- Cửa sổ tiếp theo
 - `Ctrl-B p`- Cửa sổ trước
 - `Ctrl-B 0`thông qua `Ctrl-B 9`- Chuyển đến cửa sổ 0-9
 - `Ctrl-B w`- Xem một cửa sổ đẹp
Tmux hiển thị các cửa sổ của bạn ở phía dưới trong thanh trạng thái, trông giống như sau:
```sh
[0] 0:bash* 1:bash
```
* Mục này `*`hiển thị cửa sổ hiện tại của bạn, và mỗi mục cũng hiển thị tiến trình mà cửa sổ đó được tạo ra để chạy.

Chúng tôi đã tạo một phiên tmux với hai cửa sổ:

  Cửa sổ 0 có cờ!
  
  Cửa sổ số 1 hân hạnh chào đón bạn. 
  
Đi lấy lá cờ đó đi! 
</details>
