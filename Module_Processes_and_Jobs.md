# Processses and jobs (Quy trình và công việc)
* Máy tính thực thi phần mềm để hoàn thành công việc. Trong điện toán hiện đại, phần mềm này được chia thành hai loại: nhân hệ điều hành (mà chúng ta sẽ tìm hiểu kỹ hơn ở phần sau ) và các tiến trình , mà chúng ta sẽ thảo luận ở đây. Khi Linux khởi động, nó khởi chạy một tiến trình `init` (viết tắt của initializer), tiến trình này đến lượt nó sẽ khởi chạy một loạt các tiến trình khác, các tiến trình này lại khởi chạy thêm nhiều tiến trình nữa cho đến khi cuối cùng bạn nhìn thấy giao diện dòng lệnh, mà giao diện này cũng là một tiến trình! Tất nhiên, giao diện dòng lệnh sẽ khởi chạy các tiến trình để đáp ứng các lệnh bạn nhập vào.

* Trong mô-đun này, chúng ta sẽ học cách quan sát và tương tác với các quy trình theo nhiều cách thú vị!
<details>
<summary><code>🏴Listing Processes(Quy trình liêm yết)</code></summary>

* Đầu tiên, chúng ta sẽ học cách liệt kê các tiến trình đang chạy bằng pslệnh `ls`. Tùy thuộc vào người bạn hỏi, ` psls` có thể viết tắt cho "process snapshot" (ảnh chụp nhanh tiến trình) hoặc "process status" (trạng thái tiến trình), và nó dùng để liệt kê các tiến trình. Theo mặc định, ` psls` chỉ liệt kê các tiến trình đang chạy trong cửa sổ terminal của bạn, điều này thực sự không hữu ích lắm:
```sh
hacker@dojo:~$ ps
    PID TTY          TIME CMD
    329 pts/0    00:00:00 bash
    349 pts/0    00:00:00 ps
hacker@dojo:~$
```
* Trong ví dụ trên, chúng ta có shell ( `bash`) và `ps`chính tiến trình, và đó là tất cả những gì đang chạy trên thiết bị đầu cuối cụ thể đó. Chúng ta cũng thấy rằng mỗi tiến trình đều có một mã định danh số ( ID tiến trình , hay PID), là một số duy nhất xác định mọi tiến trình đang chạy trong môi trường Linux. Chúng ta cũng thấy thiết bị đầu cuối mà các lệnh đang chạy (trong trường hợp này, được ký hiệu là `pts/0`), và tổng lượng thời gian CPU mà tiến trình đã sử dụng cho đến nay (vì các tiến trình này rất ít đòi hỏi, chúng thậm chí chưa tiêu tốn đến 1 giây!).

* Trong hầu hết các trường hợp, đây là tất cả những gì bạn sẽ thấy với giá trị mặc định `ps`. Để làm cho nó hữu ích, chúng ta cần truyền thêm một vài tham số.

Vì `ps`đây là một tiện ích rất cũ, cách sử dụng của nó hơi rắc rối. Có hai cách để chỉ định các tham số.

Cú pháp "chuẩn": với cú pháp này, bạn có thể sử dụng `-e`để liệt kê "mọi" tiến trình và `-f`để xuất ra định dạng "đầy đủ", bao gồm cả các đối số. Chúng có thể được kết hợp thành một đối số duy nhất `-ef`.
 - `ps -ef` : liệt kê tiến trình và xuất đầy đủ 

Cú pháp "BSD": Trong cú pháp này, bạn có thể sử dụng `a`để liệt kê các tiến trình cho tất cả người dùng, `x`để liệt kê các tiến trình không chạy trong cửa sổ terminal, và `u `để hiển thị kết quả "dễ đọc cho người dùng". Chúng có thể được kết hợp thành một đối số duy nhất `aux`.
 - `ps aux` : liệt kê toàn bộ các tiến trình đang chạy trên hệ thống(Tất cả người dùng,chủ sở hữu-tgian bắt đầu,tiến trình ẩn)

Hai phương pháp này, `ps -ef`và `ps aux`, cho ra kết quả hơi khác nhau nhưng vẫn có thể nhận dạng được lẫn nhau.

Hãy thử ở võ đường xem sao:
```sh
hacker@dojo:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
hacker         1       0  0 05:34 ?        00:00:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7       1  0 05:34 ?        00:00:00 /bin/sleep 6h
hacker       102       1  1 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server --auth=none -
hacker       138     102 11 05:34 ?        00:00:07 /usr/lib/code-server/lib/node /usr/lib/code-server/out/node/entr
hacker       287     138  0 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       318     138  6 05:34 ?        00:00:03 /usr/lib/code-server/lib/node --dns-result-order=ipv4first /usr/
hacker       554     138  3 05:35 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       571     554  0 05:35 pts/0    00:00:00 /usr/bin/bash --init-file /usr/lib/code-server/lib/vscode/out/vs
hacker       695     571  0 05:35 pts/0    00:00:00 ps -ef
hacker@dojo:~$
```
* Bạn có thể thấy ở đây có các tiến trình đang chạy để khởi tạo môi trường thử thách ( `docker-init`), thời gian chờ trước khi thử thách tự động kết thúc để bảo toàn tài nguyên tính toán ( `sleep 6h`thời gian chờ sau 6 giờ), môi trường VSCode (một số `code-server`tiến trình hỗ trợ), trình shell ( `bash`), và `ps -ef`lệnh của tôi. Về cơ bản, nó giống với `ps aux`:
```sh
hacker@dojo:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
hacker         1  0.0  0.0   1128     4 ?        Ss   05:34   0:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7  0.0  0.0   2736   580 ?        S    05:34   0:00 /bin/sleep 6h
hacker       102  0.4  0.0 723944 64660 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       138  3.3  0.0 968792 106272 ?       Sl   05:34   0:07 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       287  0.0  0.0 717648 53136 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       318  3.3  0.0 977472 98256 ?        Sl   05:34   0:06 /usr/lib/code-server/lib/node --dns-result-order=
hacker       554  0.4  0.0 650560 55360 ?        Rl   05:35   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       571  0.0  0.0   4600  4032 pts/0    Ss   05:35   0:00 /usr/bin/bash --init-file /usr/lib/code-server/li
hacker      1172  0.0  0.0   5892  2924 pts/0    R+   05:38   0:00 ps aux
hacker@dojo:~$
```
* Có rất nhiều điểm chung giữa `ps -ef`và `ps aux`: cả hai đều hiển thị người dùng ( `USER`cột ), PID, TTY, thời gian bắt đầu của tiến trình ( `STIME`/ `START`), tổng thời gian CPU đã sử dụng ( `TIME`) và lệnh ( `CMD/ COMMAND`). `ps -ef`Ngoài ra, còn xuất ra ID tiến trình cha ( `PPID`), là PID của tiến trình đã khởi chạy tiến trình đang xét, trong khi `ps aux`xuất ra phần trăm tổng CPU và bộ nhớ hệ thống mà tiến trình đang sử dụng. Thêm vào đó, còn rất nhiều thứ khác mà chúng ta sẽ không đề cập đến ngay bây giờ.

Thôi được rồi! Cùng luyện tập nào. Ở màn này, mình lại đổi tên `/challenge/run`file thành một tên ngẫu nhiên, và lần này mình làm cho bạn không thể tìm thấy thư mục `ls`đó `/challenge`! Nhưng mình cũng đã khởi chạy nó rồi, nên bạn có thể tìm thấy nó trong danh sách các tiến trình đang chạy, tìm ra tên file và khởi chạy lại trực tiếp để lấy flag! Chúc may mắn!

LƯU Ý: Cả hai `ps -ef`tùy chọn đều `ps aux`cắt ngắn danh sách lệnh cho phù hợp với chiều rộng của cửa sổ terminal (đó là lý do tại sao các ví dụ trên được sắp xếp gọn gàng ở phía bên phải màn hình). Nếu bạn không thể đọc toàn bộ đường dẫn đến tiến trình, bạn có thể cần phóng to cửa sổ terminal (hoặc chuyển hướng đầu ra đến nơi khác để tránh hiện tượng cắt ngắn này!). Ngoài ra, bạn có thể truyền tùy `w`chọn hai lần (ví dụ: `ps -efww`hoặc `ps auxww`) để tắt tính năng cắt ngắn
* <img width="431" height="170" alt="image" src="https://github.com/user-attachments/assets/797f84f1-43ea-47ec-8835-208cfa27121b" />
 - Ở bài này lá cờ được để trong file mà file này đang được chạy ngầm , ta phải dùng `ps aux` để hiển thị lên file này và chạy nó để lấy lá cờ


</details>
<details>
<summary><code>🏴Killing Processes(Các quy trình tiêu diệt)</code></summary>

* Bạn đã khởi chạy các tiến trình, bạn đã xem các tiến trình, giờ bạn sẽ học cách kết thúc các tiến trình! Trong Linux, điều này được thực hiện bằng `kill`lệnh có tên gọi khá mạnh mẽ là `sump`. Với các tùy chọn mặc định (mà chúng ta sẽ chỉ đề cập đến trong cấp độ này), `kill`lệnh `sump` sẽ kết thúc một tiến trình theo cách cho phép nó có cơ hội hoàn tất các công việc của mình trước khi chấm dứt sự tồn tại.

* Giả sử bạn có một `sleep`tiến trình phiền phức ( `sleep`là một chương trình chỉ đơn giản là chạy trong khoảng thời gian được chỉ định trên dòng lệnh, trong trường hợp này là 1337 giây) mà bạn đã khởi chạy trong một cửa sổ terminal khác, như sau:
```sh
hacker@dojo:~$ sleep 1337
```
* Làm thế nào để loại bỏ nó? Bạn có thể `kill`chấm dứt nó bằng cách truyền mã định danh tiến trình (mã định `PID`danh từ `ps`) làm đối số, như sau:
```sh
hacker@dojo:~$ ps -e | grep sleep
 342 pts/0    00:00:00 sleep
hacker@dojo:~$ kill 342
hacker@dojo:~$ ps -e | grep sleep
hacker@dojo:~$
```
* Giờ là lúc kết thúc tiến trình đầu tiên của bạn! Trong thử thách này, `/challenge/run`sẽ từ chối chạy trong khi `/challenge/dont_run`đang chạy! Bạn phải tìm ra `dont_run`tiến trình và `kill`kết thúc nó. Nếu bạn thất bại, pwn.collegesẽ từ chối mọi thông tin về nhiệm vụ của bạn. Chúc may mắn.
* <img width="434" height="86" alt="image" src="https://github.com/user-attachments/assets/aeb20933-5cf8-4f9d-856b-c2503a4ed787" />
 - Ở bài này ta chạy `ps aux` để hiển thị toàn bộ đường dẫn và tham số của toàn bộ các tiến trình sau đó dùng dấu `|` để chuyển đầu ra của lệnh này cho lệnh tìm kiếm `prep dont_run`-lệnh này có tác dụng tìm kiếm và hiểu thị dòng nào chứa dont_run ra.Sau đó dùng kill để loại bỏ tiến trình ngầm này rồi chạy lệnh mới cần tìm 
* Lưu ý : File này có thê là 1 tiến trình ẩn nên phải kiểm tra kĩ bằng `ps aux`
</details>
<details>
<summary><code>🏴Interrupting Processes(Các quy trình bị dán đoạn)</code></summary>

* Bạn đã học cách kết thúc các tiến trình khác bằng `kill`lệnh, nhưng đôi khi bạn chỉ muốn loại bỏ tiến trình đang làm tắc nghẽn cửa sổ terminal! May mắn thay, terminal có phím tắt cho việc này: `Ctrl-C`(ví dụ: giữ phím `Ctrl`và nhấn `C`) sẽ gửi một "lệnh ngắt" đến bất kỳ ứng dụng nào đang chờ nhập liệu từ terminal và thông thường, điều này sẽ khiến ứng dụng thoát một cách gọn gàng.

* Hãy thử ở đây! `/challenge/run`Nó sẽ từ chối đưa cờ cho bạn cho đến khi bạn can thiệp. Chúc may mắn!

* Đối với những ai thực sự quan tâm, hãy xem bài viết này về các thiết bị đầu cuối và "mã điều khiển" (chẳng hạn như Ctrl-C).
* <img width="365" height="62" alt="image" src="https://github.com/user-attachments/assets/c0e84245-62b1-46af-b2db-9709ef1d2954" />
 - ở bài này cho ta biết `crtl + C ` có nghĩa là dừng hoàn toàn tiến trình đang chạy 

</details>
<details>
<summary><code>🏴Killing Misbehaving Proccesses(Loại bỏ các tiến trình hoạt động sai)</code></summary>

* Đôi khi, các tiến trình hoạt động không đúng cách có thể gây cản trở công việc của bạn. Có thể cần phải chấm dứt các tiến trình này...

* Trong thử thách này, có một tiến trình mồi nhử đang chiếm dụng một tài nguyên quan trọng - một đường ống được đặt tên (FIFO) mà `/tmp/flag_fifo`(giống như trong thử thách` Thực hành đường ống` FIFO) `/challenge/run`muốn ghi cờ của bạn vào đó. Bạn cần phải chặn `kill`tiến trình này.

* Quy trình làm việc chung của bạn nên như sau:

    1.Kiểm tra xem những tiến trình nào đang chạy.
    2.Tìm `/challenge/decoy`trong danh sách và xác định ID quy trình của nó.
    3.`kill`Nó.
    4.Chạy `/challenge/run`lệnh để lấy cờ mà không bị quá tải bởi các lệnh giả (bạn không cần chuyển hướng đầu ra của nó; nó sẽ tự ghi vào FIFO).
Chúc may mắn!

* LƯU Ý: Bạn có thể thấy một vài cờ mồi xuất hiện ngay cả sau khi đã tắt tiến trình mồi. Điều này xảy ra vì các đường ống trong Linux được đệm : về mặt khái niệm, chúng có một độ dài nhất định mà dữ liệu truyền qua, và bạn có thể tắt tiến trình mồi trong khi dữ liệu vẫn đang nằm trong đường ống. Dữ liệu đó, sau khi đã vào đường ống, sẽ tiếp tục đi đến đầu kia (của bạn cat). Nếu bạn đợi một giây, bạn sẽ thấy các cờ mồi dừng lại, và sau đó bạn có thể /challenge/runvà chiến thắng!

* Đầu tiên ta dùng lệnh `ps -ef | grep decoy ` để tìm ra những tiến trình chứa /challenge/decoy sao đó `kill` nó đi rồi chạy `cat /tmp/flag_fifo` để đọc dữ liệu còn sót lại trong fifo sau đó gõ `ctrl + C` nếu lệnh bị treo,chạy `/challenge/run` sau đó đọc flag thật từ `fifo` bằng lệnh `cat /tmp/flag_fifo`.
</details>
<details>
<summary><code>🏴Suspending Processes(Tạm dừng các quy trình)</code></summary>

* Bạn đã học cách ngắt các tiến trình bằng lệnh `git log` `Ctrl-C`, nhưng có những biện pháp ít quyết liệt hơn mà bạn có thể sử dụng để khôi phục lại cửa sổ terminal! Bạn có thể tạm dừng các tiến trình vào chế độ nền bằng lệnh `git log` `Ctrl-Z`. Ở cấp độ này, chúng ta sẽ tìm hiểu cách thức hoạt động của lệnh này và ở cấp độ tiếp theo, chúng ta sẽ tìm hiểu cách tiếp tục các tiến trình đã bị tạm dừng!

* Cấp độ này `run`muốn thấy một bản sao khác của chính nó đang chạy và sử dụng cùng một cửa sổ dòng lệnh . Làm thế nào? Sử dụng cửa sổ dòng lệnh để khởi chạy nó, sau đó tạm dừng nó, rồi khởi chạy một bản sao khác trong khi bản đầu tiên đang bị tạm dừng!
* <img width="386" height="275" alt="image" src="https://github.com/user-attachments/assets/9bf92c49-5cdb-4c72-9389-d03e3cefe943" />
 - lệnh `ctrl + Z` để tạm dừng tiến trình đang chạy và có thể khỏi chạy lại sau đó khi cần ,ta cũng có thể khởi chạy 1 tiến trình khác như tiến trình đã tạm dừng.

</details>
<details>
<summary><code>🏴Resuming Processes(Tiếp tục các quy trình)</code></summary>

* Thông thường, khi bạn tạm dừng các tiến trình, bạn sẽ muốn tiếp tục chúng vào một thời điểm nào đó. Nếu không, tại sao không chấm dứt chúng? Để tiếp tục các tiến trình, trình thông dịch lệnh của bạn cung cấp lệnh `fg``receive`, một lệnh tích hợp sẵn, lấy tiến trình bị tạm dừng, tiếp tục nó và đưa nó trở lại hoạt động ở phía trước cửa sổ terminal.

* Hãy thử xem! Thử thách này `run`yêu cầu bạn tạm dừng rồi tiếp tục lại. Chúc may mắn!
* <img width="376" height="107" alt="image" src="https://github.com/user-attachments/assets/06116a7c-4a37-4915-a559-870987cd9d4e" />
 - Lệnh `fg` dùng để khởi chạy lại tiến trình mà mình đã tạm dừng trước đó . 
* Nếu như ta tạm dừng nhiều tiến trình thì phải sử dụng lệnh `jobs` để xem `id` các tiến trình và chọn tiến trình mình muốn sau đó dùng lệnh `fg %(id)`
</details>
<details>
<summary><code>🏴Backgroundung Processes(Các quy trình nên tảng)</code></summary>
</details>
<details>
<summary><code>🏴Foregrounding Processes(Các quy trình làm nổi bật)</code></summary>
</details>
<details>
<summary><code>🏴Strating Backgrounded Processes(Khởi động các quy trình nền)</code></summary>
</details>
<details>
<summary><code>🏴Processes Exit Codes(Mã thoát của quy trình)</code></summary>
</details>
