#Untangling Users
* Bạn có nghĩ rằng bạn, `hacker`, là "bóng ma" duy nhất trong máy không? Có RẤT NHIỀU người dùng trên một hệ thống Linux điển hình! Danh sách đầy đủ người dùng trên hệ thống Linux được chỉ định trong tệp `/etc/passwd`(được đặt tên như vậy vì lý do lịch sử --- nó thực sự không còn lưu trữ mật khẩu nữa). Đây là một ví dụ từ container dojo:
```sh
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
systemd-timesync:x:101:101:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
systemd-network:x:102:103:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:103:104:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
mysql:x:104:105:MySQL Server,,,:/nonexistent:/bin/false
messagebus:x:105:106::/nonexistent:/usr/sbin/nologin
sshd:x:106:65534::/run/sshd:/usr/sbin/nologin
hacker:x:1000:1000::/home/hacker:/bin/bash
```
* Rất nhiều người dùng ở đây, và rất nhiều thông tin! Mỗi dòng chứa, được phân tách bằng :dấu cách, tên người dùng, một `x`ký tự đại diện cho vị trí mật khẩu cũ (chúng ta sẽ đề cập đến vị trí thực tế của nó sau), ID người dùng dạng số, ID nhóm mặc định dạng số, thông tin chi tiết đầy đủ của người dùng, thư mục chính và shell mặc định.

* Chúng ta có thể thấy `hacker`người dùng ở dưới cùng. Đó là bạn! Hầu hết những người dùng còn lại đều có mặt vì lý do lịch sử, là các tài khoản dịch vụ để hỗ trợ các phần mềm đã cài đặt khác nhau, hoặc một số là tài khoản "tiện ích" (ví dụ: người `nobody`dùng này được sử dụng để đảm bảo rằng một số chương trình chạy mà không cần bất kỳ đặc quyền đặc biệt nào).

* Một người dùng quan trọng là `root`quản trị viên hệ thống. Quản trị viên hệ thống có những tác động bảo mật rõ ràng: một `hacker`người dùng bằng cách nào đó, thông qua các chức năng khác nhau của Linux, có thể trở thành `root`người dùng quản trị hệ thống và sẽ gây ra thiệt hại nghiêm trọng cho hệ thống. Mục tiêu rất thường gặp của tin tặc khi xâm nhập hệ thống là leo thang quyền truy cập `root`, và do đó, quản trị viên hệ thống `root`phải được bảo vệ bằng mọi giá!

* Trong mô-đun này, chúng ta sẽ khám phá các thủ đoạn khác nhau của người dùng, tìm hiểu các cách thức chuyển đổi người dùng sang quyền quản trị hệ thống và cùng nhau trải nghiệm những điều thú vị!

<details>
<summary><code>🏴Becoming root with su(Trở thành gốc rễ với `su`)</code><summary>

* Không chỉ tin tặc mới cần có quyền quản trị `root`. Thông thường, bạn, với tư cách là chủ sở hữu máy tính, cũng cần có `root`quyền quản trị để quản lý nó. Việc có quyền quản trị `root`là một hành động khá phổ biến mà người dùng Linux thực hiện, và có hai tiện ích dành cho mục đích này: `su`và `sudo`.

Trong thử thách này, chúng ta sẽ tìm hiểu về lệnh cũ hơn `su`( lệnh người dùng thay thế ) . Lệnh này hiện không còn được sử dụng để nâng quyền truy cập nữa, nhưng nó là một tiện ích thanh lịch từ một thời kỳ văn minh hơn, và chúng ta sẽ tìm hiểu về nó đầu tiên.`root`

`su`là một tệp nhị phân setuid:
```sh
hacker@dojo:~$ ls -l /usr/bin/su
-rwsr-xr-x 1 root root 232416 Dec 1 11:45 /usr/bin/su
hacker@dojo:~$
```
* Vì bit SUID được thiết lập, `su`nó chạy với quyền `root`. Khi chạy với quyền `root`, nó có thể khởi động một `root`shell! Tất nhiên, surất thận trọng: trước khi cho phép người dùng nâng quyền lên `root`, nó kiểm tra để đảm bảo rằng người dùng biết `root`mật khẩu:
```sh
hacker@dojo:~$ su
Password: 
su: Authentication failure
hacker@dojo:~$
```
* Việc kiểm tra `root`mật khẩu chính là điều khiến phương pháp cũ trở nên lỗi thời `su`. Các hệ thống hiện đại rất hiếm khi sử dụng `root`mật khẩu, và các cơ chế khác nhau (mà chúng ta sẽ tìm hiểu sau) được dùng để cấp quyền quản trị.

* Nhưng thử thách NÀY (và chỉ thử thách này) mới có `root`mật khẩu. Mật khẩu đó là `hack-the-planet`, và bạn phải cung cấp nó cho `su`để trở thành `root`! Hãy làm điều đó và đọc lá cờ!
* <img width="326" height="75" alt="image" src="https://github.com/user-attachments/assets/74e134fe-79c9-4814-bb88-e48973cc2dad" />
 - Dấu nhác đổi lệnh từ `hacker@...:$`(Dấu $ thể hện người dùng thường) thành `root@...:#`(Dấu # thể hiện quyền root)
</details>
<details>
<summary><code>🏴Other users with su(Những người dùng khác có `su`)</code><summary>

* Nếu không có đối số nào, lệnh sunày sẽ khởi động một rootshell (sau khi xác thực bằng rootmật khẩu của người dùng kia). Tuy nhiên, bạn cũng có thể cung cấp tên người dùng làm đối số để chuyển sang người dùng đó thay vì người dùng mặc định root. Ví dụ:
```sh
hacker@dojo:~$ su some-user
Password:
some-user@dojo:~$
```
* Tuyệt vời! Ở màn này, bạn phải chuyển sang zardusngười dùng và sau đó chạy lệnh /challenge/run. Mật khẩu của Zardus là dont-hack-me. Chúc may mắn!
* <img width="292" height="56" alt="image" src="https://github.com/user-attachments/assets/72a15561-bb4e-4b17-866b-66addf2bd8d2" />
 - Nếu muốn chuyển sang người dùng nào đó thì ta lấy tên ng dùng đó làm đối số của `su`
</details>
<details>
<summary><code>🏴Cracking passwords(Phá mật khẩu)</code><summary>

* Khi bạn nhập mật khẩu cho `su`, hệ thống sẽ so sánh mật khẩu đó với mật khẩu đã lưu trữ cho người dùng đó. Trước đây, các mật khẩu này được lưu trữ trong `/etc/passwd`, nhưng vì `/etc/passwd`là một tệp có thể đọc được trên toàn hệ thống, điều này không tốt cho mật khẩu, nên chúng đã được chuyển sang `/etc/shadow`. Đây là ví dụ `/etc/shadow`từ cấp độ trước:
```sh
root:$6$s74oZg/4.RnUvwo2$hRmCHZ9rxX56BbjnXcxa0MdOsW2moiW8qcAl/Aoc7NEuXl2DmJXPi3gLp7hmyloQvRhjXJ.wjqJ7PprVKLDtg/:19921:0:99999:7:::
daemon:*:19873:0:99999:7:::
bin:*:19873:0:99999:7:::
sys:*:19873:0:99999:7:::
sync:*:19873:0:99999:7:::
games:*:19873:0:99999:7:::
man:*:19873:0:99999:7:::
lp:*:19873:0:99999:7:::
mail:*:19873:0:99999:7:::
news:*:19873:0:99999:7:::
uucp:*:19873:0:99999:7:::
proxy:*:19873:0:99999:7:::
www-data:*:19873:0:99999:7:::
backup:*:19873:0:99999:7:::
list:*:19873:0:99999:7:::
irc:*:19873:0:99999:7:::
gnats:*:19873:0:99999:7:::
nobody:*:19873:0:99999:7:::
_apt:*:19873:0:99999:7:::
systemd-timesync:*:19901:0:99999:7:::
systemd-network:*:19901:0:99999:7:::
systemd-resolve:*:19901:0:99999:7:::
mysql:!:19901:0:99999:7:::
messagebus:*:19901:0:99999:7:::
sshd:*:19901:0:99999:7:::
hacker::19916:0:99999:7:::
zardus:$6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1.:19921:0:99999:7:::
```
* Được phân tách bằng :dấu ngoặc kép, trường đầu tiên của mỗi dòng là tên người dùng và trường thứ hai là mật khẩu. Giá trị *hoặc !về mặt chức năng có nghĩa là đăng nhập bằng mật khẩu cho tài khoản đã bị vô hiệu hóa, trường trống có nghĩa là không có mật khẩu (một lỗi cấu hình không hiếm gặp cho phép đăng nhập không cần mật khẩu `su`trong một số cấu hình), và chuỗi dài như "Zardus'" `$6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1`.là kết quả của việc mã hóa một chiều (băm) mật khẩu của Zardus từ cấp độ cuối cùng (trong trường hợp này là `dont-hack-me`). Các trường khác trong tệp này có ý nghĩa khác, và bạn có thể đọc thêm về chúng tại đây `https://www.cyberciti.biz/faq/understanding-etcshadow-file/` .

* Khi bạn nhập mật khẩu vào hệ thống su, nó sẽ mã hóa một chiều (tạo hàm băm) mật khẩu đó và so sánh kết quả với giá trị đã lưu trữ. Nếu kết quả trùng khớp, suhệ thống sẽ cấp cho bạn quyền truy cập vào người dùng!

* Nhưng nếu bạn không biết mật khẩu thì sao? Nếu bạn có giá trị băm của mật khẩu, bạn có thể bẻ khóa nó! Mặc dù /etc/shadowtheo mặc định, chỉ có thể đọc được bằng root, nhưng rò rỉ dữ liệu vẫn có thể xảy ra! Ví dụ, các bản sao lưu thường được lưu trữ mà không được mã hóa và bảo vệ không đầy đủ trên các máy chủ tệp, và điều này đã dẫn đến vô số vụ rò rỉ dữ liệu.

Nếu tin tặc có được mật khẩu bị rò rỉ /etc/shadow, chúng có thể bắt đầu bẻ khóa mật khẩu và gây ra thiệt hại nghiêm trọng. Việc bẻ khóa có thể được thực hiện bởi John the Ripper , như sau:
```sh
hacker@dojo:~$ john ./my-leaked-shadow-file
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Will run 32 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
password1337      (zardus)
1g 0:00:00:22 3/3 0.04528g/s 10509p/s 10509c/s 10509C/s lykys..lank
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@dojo:~$
```
Tại đây, John the Ripper đã giải mã được mật khẩu bị rò rỉ của Zardus để tìm ra giá trị thực của nó password1337. Tội nghiệp Zardus!

Màn chơi này mô phỏng câu chuyện đó, cung cấp cho bạn một thông tin rò rỉ /etc/shadow(trong /challenge/shadow-leak). Hãy giải mã nó (việc này có thể mất vài phút), suđể đến zardus, và chạy /challenge/runđến lấy lá cờ!
</details>
<details>
<summary><code>🏴Using sudo(Sử dụng sudo)</code><summary>

* Ngày xưa, một hệ thống Linux điển hình có rootmật khẩu mà quản trị viên sẽ sử dụng suđể đăng nhập root(sau khi đăng nhập vào tài khoản của họ bằng mật khẩu tài khoản thông thường). Nhưng rootmật khẩu rất khó bảo trì, chúng (hoặc mã băm của chúng!) có thể bị rò rỉ, và chúng không phù hợp với môi trường lớn hơn (ví dụ: nhiều máy chủ). Để giải quyết vấn đề này, trong những thập kỷ gần đây, thế giới đã chuyển từ quản trị thông qua lệnh ` sudo` susang quản trị thông qua lệnh `sudo` sudo( Thông tin thú vị : `sudo` sudoban đầu viết tắt của "su peruser do " , nhưng đã đổi thành su"do", và vì su`sudo` viết tắt của "substitute user", nên ý nghĩa hiện tại của `sudo` sudolà "substitute user, do").

* Không giống như su, mặc định khởi chạy shell với tư cách người dùng được chỉ định, sudomặc định chạy lệnh với tư cách root:
```sh
hacker@dojo:~$ whoami
hacker
hacker@dojo:~$ sudo whoami
root
hacker@dojo:~$
```
* Hoặc, điều quan trọng hơn liên quan đến việc nhận cờ:
```sh
hacker@dojo:~$ grep hacker /etc/shadow
grep: /etc/shadow: Permission denied
hacker@dojo:~$ sudo grep hacker /etc/shadow
hacker:$6$Xro.e7qB3Q2Jl2sA$j6xffIgWn9xIxWUeFzvwPf.nOH2NTWNJCU5XVkPuONjIC7jL467SR4bXjpVJx4b/bkbl7kyhNquWtkNlulFoy.:19921:0:99999:7:::
hacker@dojo:~$
```
* Không giống như su, vốn dựa vào xác thực bằng mật khẩu, sudokiểm tra các chính sách để xác định xem người dùng có được phép chạy các lệnh với quyền hay không root. Các chính sách này được định nghĩa trong /etc/sudoers, và mặc dù phần lớn nằm ngoài phạm vi bài viết này, nhưng có rất nhiều tài liệu để tìm hiểu về vấn đề này!

* Vì vậy, thế giới đã chuyển sang sudovà (về mặt quản trị hệ thống) đã bỏ lại suphía sau. Trên thực tế, ngay cả Chế độ Đặc quyền của pwn.college cũng hoạt động bằng cách cho phép bạn sudotruy cập để nâng cao đặc quyền!

* Ở cấp độ này, chúng tôi sẽ cấp cho bạn sudoquyền truy cập, và bạn sẽ sử dụng nó để đọc lá cờ. Thật dễ dàng!

* LƯU Ý: Sau cấp độ này, chúng ta sẽ kích hoạt Chế độ Đặc quyền! Trong không gian làm việc, hãy nhấp vào biểu tượng khóa đóng để bắt đầu lại thử thách ở Chế độ Đặc quyền và nhấp vào biểu tượng khóa mở để trở lại chế độ bình thường. Tên máy chủ của dấu nhắc lệnh sẽ kết thúc ~practicebằng khi Chế độ Đặc quyền được kích hoạt. Chế độ Đặc quyền cho phép bạn sudotruy cập đầy đủ để phân tích và gỡ lỗi, nhưng nó cung cấp một cờ giữ chỗ không thể gửi đi.
* Lệnh sudo (Superuser Do): Cho phép người dùng thường thực thi một lệnh cụ thể dưới quyền root mà không cần biết mật khẩu của root (thường chỉ cần nhập mật khẩu của chính tài khoản cá nhân nếu được yêu cầu).
* Ý nghĩa và chức năng chính:
 - `Nâng quyền` : Thực thi 1 lệnh duy nhất cần quyền quản trị mà không cần đăng nhập hẳn vào tài khoản `root`
 - Bảo mật : Theo dõi lịch sử thao tác của người dùng bằng cách ghi lại toàn bộ các lệnh đã sử dụng kèm theo `sudo` và nhật ký hệ thống.
 - Ủy quyền(Sudoers):Cho phép người quản trị cấp quyền thực hiện một hoặc một vài lệnh cụ thể cho các user thường thông qua tệp cấu hình (thường là `/etc/sudoers`) mà không cần chia sẻ mật khẩu root - tránh bị lộ mật khẩu
</details>
