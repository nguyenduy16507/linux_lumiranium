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
    - `Xác thực (Authentication)`: Trả lời câu hỏi `"Bạn là ai?"`
       +  Xác định danh tính người dùng thông qua các phương thức như tên đăng nhập/mật khẩu hoặc mã khóa SSH
    - `Ủy quyền (Authorization)`: Trả lời câu hỏi `"Bạn có thể làm gì trên hệ thống?"`
       + Xác định các hành động cụ thể mà một danh tính đã xác thực được phép thực hiện
       +  `Ví dụ`: Giáo sư có quyền nhập điểm, sinh viên chỉ có quyền xem điểm của chính mình

   2. `Chính sách và Cơ chế (Policy vs. Mechanism)`
    - `Chính sách (Policy)`: Là các tuyên bố về quyền hạn, quy tắc ai được phép làm gì
       + Ví dụ: "Sinh viên không được phép đọc file bài tập của sinh viên khác"
    - `Cơ chế (Mechanism)`: Là công cụ hoặc phương thức kỹ thuật để thực thi chính sách đó
       + Ví dụ: Quyền truy cập file (file permissions) trên máy tính hoặc ổ khóa trên cửa vật lý
  3. `Quản lý rủi ro và Niềm tin (Risk & Trust)`
    - `Niềm tin (Trust)`: Hệ thống cần xác định ai được tin tưởng để thực hiện các nhiệm vụ cụ thể
    - `Rủi ro (Risk)`: Xác suất xảy ra một sự cố xấu (như rò rỉ dữ liệu hoặc gian lận)
      + `Nguyên tắc`: Không thể loại bỏ hoàn toàn rủi ro, chỉ có thể quản lý và giảm thiểu nó
    - `Biện pháp giảm thiểu`:
      + Sử dụng `Ủy quyền` chính xác để hạn chế quyền hạn
      + Sử dụng `Nhật ký và Kiểm toán (Logging & Audit logs)` để ghi lại các hoạt động, giúp phát hiện và khắc phục khi có sự cố xảy ra
  4. `Ví dụ thực tế từ bài giảng`
    - `Môi trường đại học`:
      + `Hệ thống máy chủ dùng chung`: Sinh viên có thể vô tình hoặc cố ý để lộ file bài tập nếu không thiết lập quyền đọc đúng cách
      + `Liêm chính học thuật`: Việc sao chép bài làm (dù có sự cho phép hay không) đều vi phạm chính sách của nhà trường
    - `Hệ thống quản lý điểm`: Nếu kiểm soát truy cập kém, sinh viên có thể tự thay đổi điểm số, làm mất đi giá trị của toàn bộ hệ thống
  5. `Tầm quan trọng của Kiểm soát truy cập`
    - Ngăn chặn rò rỉ dữ liệu nhạy cảm trong các doanh nghiệp
    - Đảm bảo tính toàn vẹn và an ninh cho hệ thống máy tính
* Nội dung bài giảng về **Triển khai kiểm soát truy cập**:
  Phần này tập trung vào cách biến Ma trận kiểm soát Truy cập(Access Control Matrix) lý thuyết thành các cơ chế thực tế trong hệ điều hành.
  1.`Vấn đề quy mô`:Một ma trận lưu trữ mọi chủ thể(hàng) và mọi đối tượng(cột) là quá lớn và tốn kém không gian .Do đó, hệ thống chia nhỏ ma trận này theo 2 hướng:
   - `Danh sách Kiểm soát Truy cập (Access Control Lists - ACL)`:
     + `Cách thức`: Lưu trữ theo từng cột của ma trận cùng với đối tượng (ví dụ: đính kèm trực tiếp vào            file)
     + `Đặc điểm`: Cần xác thực chủ thể (người dùng) rất mạnh để tránh giả mạo danh tính
     + `Ưu điểm`: Dễ dàng thu hồi quyền truy cập đối với một file cụ thể (revocation) và kiểm tra nhanh xem          "Ai có quyền trên file này?"
   - `Danh sách Năng lực (Capability Lists)`:
     + `Cách thức`: Lưu trữ theo từng hàng của ma trận cùng với chủ thể (giống như mỗi người dùng giữ một           bộ"chìa khóa" hoặc "vé")
     + `Đặc điểm`: Không thể làm giả (unforgeable), thường sử dụng kỹ thuật mã hóa để bảo vệ
     + `Ưu điểm`: Phù hợp cho các chủ thể động, tồn tại ngắn hạn; dễ dàng thu hồi tất cả quyền của một              người dùng và trả lời câu hỏi "Người này có thể làm gì trên hệ thống?"
       
  2.` Nguyên tắc Đặc quyền tối thiểu (Least Privilege)`:Hệ thống nên được thiết kế để một chủ thể chỉ có đúng những quyền cần thiết để hoàn thành công việc, giúp hạn chế rủi ro khi bị tấn công.
* Nội dung bài giảng về **Kiểm soát Truy cập POSIX(POSIX Access Control)**:
  Đây là cách hệ thống Unix-like(như Linux) thực thi mô hình ACL một cách gọn nhẹ và hiệu quả bằng cách sử dụng các bit quyền hạn.
  - `Hệ thống 12 bit quyền hạn`: Để tiết kiệm không gian, POSIX mã hóa quyền truy cập vào 12 bit cho mỗi         file, chia làm 4 nhóm (mỗi nhóm 3 bit):
    
      1.`Nhóm bit đặc biệt`: SetUID, SetGID và Sticky bit
    
      2.`Quyền của Chủ sở hữu (Owner)`: Read (r), Write (w), Execute (x)
    
      3.`Quyền của Nhóm (Group)`: r, w, x
    
      4.`Quyền của Người dùng khác (Others/All)`: r, w, x
    
  - `Cơ chế SetUID (Set User ID) - Cực kỳ quan trọng`:
     + `Ký hiệu`: Xuất hiện chữ s ở phần quyền thực thi của chủ sở hữu (ví dụ: -rwsr-xr-x)
     + `Hoạt động`: Khi chạy một chương trình có bit SetUID, tiến trình sẽ chạy với quyền của chủ sở hữu           file chứ không phải người dùng gọi lệnh
     + `Ví dụ`: Lệnh chsh (thay đổi shell) có SetUID root để nó có thể ghi vào file /etc/passwd (vốn chỉ           root mới có quyền ghi) nhằm cập nhật shell cho người dùng
* `Sticky Bit`: Thường dùng cho thư mục dùng chung như /tmp. Nó cho phép mọi người tạo file nhưng ngăn cản việc xóa hoặc đổi tên file của người khác
* `Các file và lệnh hệ thống then chốt`:
  - `ls -la`: Hiển thị các bit quyền hạn và danh tính chủ sở hữu/nhóm
  - `/etc/passwd`: Lưu thông tin người dùng, UID, thư mục nhà và shell

  - `/etc/shadow`: Lưu mật khẩu đã mã hóa, chỉ root mới có quyền đọc
  - `ps`: Xem danh tính (UID) của các tiến trình đang chạy
**Lưu ý**:Có thể kiểm tra xem 1 file có bộ bit `SetUID` hay không bằng lệnh `ls -la`

VD: Thay vì thấy chữ x(execute) ở phần quyền của chủ sở hữu, bạn sẽ thấy chứ `s` - vd: `rwsr-xr-x`, chữ `s` này có nghĩa là file đó vừa có quyền thực thi, vừa được thiết lập cơ chế `SetUID`
**Tóm lại**: Triển khai (Implementing) là khung lý thuyết về cách tổ chức quyền (ACL vs Capabilities), còn POSIX là một ví dụ cụ thể về cách dùng ACL 12-bit để vận hành một hệ điều hành thực tế.
</details>
<details>
  <summary><code>🏴Changing File Ownership(Thay đổi quyền sở hữu tệp)</code></summary>

* Điều đầu tiên và quan trọng nhất: quyền sở hữu tập tin. Mỗi tập tin trong Linux đều thuộc sở hữu của một người dùng trên hệ thống. Thông thường, trong cuộc sống hàng ngày, người dùng đó chính là người dùng mà bạn đăng nhập mỗi ngày.

* Trên một hệ thống dùng chung (như trong phòng máy tính), có thể có nhiều người dùng với các tài khoản khác nhau, mỗi người đều có các tệp riêng trong thư mục cá nhân của mình. Nhưng ngay cả trên một hệ thống không dùng chung (như máy tính cá nhân của bạn), Linux vẫn có nhiều tài khoản người dùng "dịch vụ" cho các tác vụ khác nhau.

* Hai tài khoản người dùng quan trọng nhất là:

1. Tài khoản người dùng của bạn! Trên pwn.college, đây là tài `hacker`khoản người dùng, bất kể tên người dùng của bạn là gì.
2. `root`Đây là tài khoản quản trị và trong hầu hết các tình huống bảo mật, đây là mục tiêu tối thượng. Nếu bạn chiếm được quyền kiểm soát `root`người dùng này, bạn gần như chắc chắn đã đạt được mục tiêu tấn công của mình!
Vậy thì sao? Chà, hóa ra cách chúng tôi ngăn bạn làm điều đó `cat /flag` là bằng cách giao `/flag`quyền sở hữu cho rootngười dùng, cấu hình quyền truy cập sao cho không người dùng nào khác có thể đọc được (bạn sẽ học cách làm điều đó sau), và cấu hình thử thách thực tế để chạy với tư cách `root`người dùng đó (bạn cũng sẽ học cách làm điều này sau). Kết quả là khi bạn thực hiện `cat /flag`, bạn sẽ nhận được:
```sh
hacker@dojo:~$ ls -l /flag
-r-------- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$ cat /flag
cat: /flag: Permission denied
hacker@dojo:~$
```
* Ở đây, bạn có thể thấy rằng cờ này thuộc sở hữu của `root`người dùng (dòng đầu tiên `root`) và `root`nhóm ( `root`dòng thứ hai). Khi chúng ta cố gắng đọc nó với tư cách `hacker`người dùng, chúng ta bị từ chối. Tuy nhiên, nếu chúng ta là `root`(một giấc mơ của hacker!), chúng ta sẽ không gặp vấn đề gì khi đọc tệp này:
```sh
root@dojo:~# cat /flag
pwn.college{demo_flag}
root@dojo:~#
```
* Điều thú vị là chúng ta có thể thay đổi quyền sở hữu của các tập tin! Việc này được thực hiện thông qua lệnh chown( thay đổi chủ sở hữu ):
```sh
chown [username] [file]
```
* Thông thường, chownchỉ người dùng mới có thể gọi hàm này root. Giả sử chúng ta rootlại là (điều này không bao giờ lỗi thời!), và xem một ví dụ sử dụng điển hình của hàm chown:
```SH
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chown hacker college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 hacker root    0 May 22 13:42 college_file
drwxr-xr-x 2 root   root 4096 May 22 13:42 pwn_directory
root@dojo:~#
```
* `college_file`Quyền sở hữu đã được chuyển cho `hacker`người dùng, và giờ `hacker`người dùng có thể làm bất cứ điều gì `root`với nó trước đây! Nếu đây là `/flag`tập tin, điều đó có nghĩa là `hacker`người dùng có thể đọc được nó!

* Ở cấp độ này, chúng ta sẽ thực hành thay đổi chủ sở hữu của `/flag`tập tin thành `hacker`người dùng, và sau đó đọc cờ. Chỉ riêng cho thử thách này, tôi đã thiết kế sao cho bạn có thể sử dụng lệnh `chown` thoải mái với tư cách `hacker`người dùng (thông thường, điều này yêu cầu bạn phải có quyền `root``sudo`). Hãy sử dụng quyền lực này một cách khôn ngoan và thoải mái sử dụng lệnh `chown`!
**Chú ý**: Lệnh `chown` dùng để `thay đổi chủ sở hữu(User)` và `nhóm sở hữu(Group)` của file hoặc thư mục. Vì việc thay đổi chủ sở hữu ảnh hưởng khá nghiêm trọng đến bảo mật, lệnh này thường yêu cầu quyền quản trị cao nhất(`sudo`)
   * `Cú pháp cơ bản` : `sudo chown [Tên_User]/:[Tên_Group] đường_dẫn/đến/file_hoặc_thư_mục`
     - `[Tên_User]` nếu muốn đổi chủ sở hữu
     - ` :[Tên_Group]` nếu muốn đổi nhóm sở hữu
     - ` [Tên_User]:[Tên_Group]` nếu muốn đổi cả chủ sở hữu và nhóm sở hữu 
   * Khi bạn có một thư mục chứa hàng trăm file/thư mục con bên trong và muốn đổi chủ sở hữu cho toàn bộ thì thêm tham số `-R`
   * Dùng lệnh `ls -l` để kiểm tra kết quả sau khi chạy lệnh đổi 
</details>
<details>
  <summary><code>🏴Groups and Files(Nhóm và tệp)</code></summary>

* Chia sẻ là thể hiện sự quan tâm, và chia sẻ là một phần không thể thiếu trong thiết kế của Linux. Các tập tin đều có người dùng sở hữu và nhóm sở hữu . Một nhóm có thể có nhiều người dùng, và một người dùng có thể là thành viên của nhiều nhóm.

* Bạn có thể kiểm tra xem mình thuộc nhóm nào bằng `id`lệnh:
```sh
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@dojo:~$
```
* Ở đây, `hacker`người dùng chỉ thuộc `hacker`nhóm. Trường hợp sử dụng phổ biến nhất của nhóm là để kiểm soát quyền truy cập vào các tài nguyên hệ thống khác nhau. Ví dụ, "Chế độ đặc quyền" trong pwn.college cấp cho bạn quyền truy cập root để gỡ lỗi tốt hơn, v.v. Điều này được xử lý bằng cách cấp cho bạn một nhóm bổ sung khi bạn khởi chạy ở Chế độ đặc quyền:
```sh
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker),27(sudo)
hacker@dojo:~$
```
* Một người dùng chính điển hình của máy tính để bàn Linux thường có rất nhiều nhóm. Ví dụ, đây là màn hình nền của Zardus:
```sh
zardus@yourcomputer:~$ id
uid=1000(zardus) gid=1000(zardus) groups=1000(zardus),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),100(users),106(netdev),114(bluetooth),117(lpadmin),120(scanner),995(docker)
zardus@yourcomputer:~$
```
* Tất cả các nhóm này cho phép Zardus đọc đĩa CD và đĩa mềm (ai còn dùng đến chúng nữa?), quản trị hệ thống, phát nhạc, vẽ lên màn hình video, sử dụng Bluetooth, v.v. Thông thường, việc kiểm soát truy cập này được thực hiện thông qua quyền sở hữu nhóm trên hệ thống tập tin! Ví dụ, việc xuất đồ họa có thể được thực hiện thông qua `/dev/fb0`tập tin đặc biệt:
```sh
zardus@yourcomputer:~$ ls -l /dev/fb0
crw-rw---- 1 root video 29, 0 Jun 30 23:42 /dev/fb0
zardus@yourcomputer:~$
```
* Tệp này là một tệp thiết bị đặc biệt (loại ccó nghĩa là nó là "thiết bị ký tự"), và việc tương tác với nó sẽ dẫn đến những thay đổi trong đầu ra hiển thị (thay vì thay đổi dung lượng lưu trữ trên đĩa, như đối với một tệp thông thường!). Tài khoản người dùng của Zardus trên máy tính của anh ấy có thể tương tác với nó vì tệp này có quyền sở hữu nhóm là `video`, và Zardus là thành viên của `video`nhóm đó.

Tuy nhiên, tập tin trong phòng tập võ lại không may mắn như vậy `/flag`! Hãy xem xét những điều sau:
`
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@dojo:~$ ls -l /flag
-r--r----- 1 root root ... /flag
hacker@dojo:~$ cat /flag
cat: /flag: Permission denied
hacker@dojo:~$
Ở đây, tập tin cờ thuộc sở hữu của rootngười dùng và rootnhóm, và hackerngười dùng này không phải là người dùng cũng không phảiroot là thành viên của rootnhóm, vì vậy không thể truy cập tập tin. May mắn thay, quyền sở hữu nhóm có thể được thay đổi bằng lệnh chgrp( change group )! Trừ khi bạn là chủ sở hữu của tập tin và là thành viên trong nhóm mới, việc này thường yêu cầu quyền truy cập, vì vậy hãy kiểm tra bằng lệnh sau `:rootroot`
```sh
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chgrp hacker college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 root root   4096 May 22 13:42 pwn_directory
root@dojo:~#
```
* Ở cấp độ này, tôi đã cho phép bất kỳ nhóm nào sở hữu cờ đều có thể đọc được, nhưng hiện tại nhóm đó là `root`. May mắn thay, tôi cũng đã cho phép bạn thực thi lệnh này `chgrp`với tư cách `hacker`người dùng! Hãy thay đổi quyền sở hữu nhóm của tệp cờ và đọc cờ!  
</details>
<details>
  <summary><code>🏴Fun With Groups Names(Trò chơi với tên nhóm)</code></summary>

* Ở các cấp độ trước, bạn có thể nhận thấy rằng `hacker`người dùng của bạn là thành viên của `hacker`nhóm này, và người dùng kia `zardus`cũng là thành viên của `zardus`nhóm khác. Có một quy ước trong Linux rằng mỗi người dùng có nhóm riêng, nhưng điều này không nhất thiết phải đúng. Ví dụ, nhiều phòng máy tính sẽ đưa tất cả người dùng của họ vào một `user`nhóm chung duy nhất.

* Vấn đề là, `hacker`trước đây bạn đã sử dụng lệnh đó cho nhóm, nhưng ở cấp độ này, cách đó sẽ không hiệu quả. Tôi vẫn cho phép bạn sử dụng lệnh đó `chgrp`, nhưng tôi đã chọn ngẫu nhiên tên nhóm mà người dùng của bạn thuộc về. Bạn sẽ cần sử dụng idlệnh để tìm ra tên nhóm đó, rồi chgrptiến đến chiến thắng!
*<img width="296" height="79" alt="image" src="https://github.com/user-attachments/assets/b574ce67-db7c-408d-9327-e37433c86b56" />

   - Đấu tiên ta chạy lệnh `ls -l /flag` để kiểm tra ta thấy chủ sở hữu và nhóm sở hữu có quyền đọc file `/flag` mà user `hacker` không phải là root nên ko có quyền mở file này. Nên ta phải chuyển đổi nhóm sở hữu của /flag sang nhóm ngẫu nhiên mà user `hacker` đang thuộc về thì lúc này user `hacker` đã trở thành thiền viên của nhóm sở hữu file đó. Từ đó user `hacker` có thể mở được file `/flag`
</details>
<details>
  <summary><code>🏴Changing Permissions(Thay đổi quyền truy cập)</code></summary>

* Vậy là giờ chúng ta đã hiểu rõ về quyền sở hữu. Hãy cùng bàn về khía cạnh khác: quyền truy cập tệp. Nhớ lại ví dụ của chúng ta:
```sh
hacker@dojo:~$ mkdir pwn_directory
hacker@dojo:~$ touch college_file
hacker@dojo:~$ ls -l
total 4
-rw-r--r-- 1 hacker hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 hacker hacker 4096 May 22 13:42 pwn_directory
hacker@dojo:~$
```
* Xin nhắc lại, ký tự đầu tiên là loại tệp. Chín ký tự tiếp theo là quyền truy cập thực tế của tệp hoặc thư mục, được chia thành 3 ký tự biểu thị quyền cho người dùng sở hữu (giờ thì bạn đã hiểu rồi!), 3 ký tự biểu thị quyền cho nhóm sở hữu (giờ bạn cũng đã hiểu rồi!), và 3 ký tự biểu thị quyền mà tất cả những người dùng và nhóm khác (ví dụ: người dùng khác) có đối với tệp.

Mỗi ký tự trong ba ký tự đó đại diện cho quyền hạn thuộc một loại khác nhau:
```sh
r - user/group/other can read the file (or list the directory)-`Có thể đọc tệp`(hoặc liệt kê thư mục)
w - user/group/other can modify the files (or create/delete files in the directory)-`Có thể chỉnh sửa` tệp(hoặc tạo/xóa thư mục)
x - user/group/other can execute the file as a program (or can enter the directory, e.g., using `cd`)-`Có thể thực thi tệp tin` như 1 chương trình (hoặc có thể vào thư mục,vd: như lệnh`cd`)
- - nothing
```
Như `college_file`rên, mục `rw-r--r--`quyền được giải mã thành:
```sh
`r`: Người dùng sở hữu tập tin (user hacker) có thể đọc tập tin đó.
`w`: Người dùng sở hữu tập tin (user hacker) có thể ghi vào tập tin đó.
`-`: Người dùng sở hữu tập tin (người dùng hacker) không thể thực thi nó.
`r`: Người dùng trong nhóm sở hữu tệp (nhóm hacker) có thể đọc tệp đó.
`-`: Người dùng trong nhóm sở hữu tệp (nhóm hacker) không thể ghi vào tệp đó.
`-`: Người dùng trong nhóm sở hữu tệp (nhóm hacker) không thể thực thi tệp đó.
`r`: Tất cả người dùng khác đều có thể đọc được.
`-`: tất cả người dùng khác không thể ghi vào đó
`-`: Những người dùng khác không thể thực thi lệnh này.
```sh
Bây giờ, hãy cùng xem các quyền mặc định của `/flag`:
```sh
hacker@dojo:~$ ls -l /flag
-r-------- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$
```
* Ở đây,chỉ có một bit được thiết lập: `r`quyền đọc cho người dùng sở hữu (trong trường hợp này là `root`). Các thành viên của nhóm sở hữu ( `root`nhóm ) và tất cả người dùng khác không có quyền truy cập vào tệp.

Có thể bạn đang thắc mắc về cách thức `chgrp`hoạt động của các cấp độ quyền truy cập, nếu không có quyền truy cập nhóm vào tệp tin. Vâng, đối với các cấp độ đó, tôi đã thiết lập quyền truy cập theo cách khác:
```sh
hacker@dojo:~$ ls -l /flag
-r--r----- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$
```
* Nhóm đó có quyền truy cập! Đó là lý do tại sao `chgrp`việc sao chép tập tin cho phép bạn đọc được tập tin.

* Tóm lại! Giống như quyền sở hữu, quyền truy cập tệp cũng có thể được thay đổi. Việc này được thực hiện bằng lệnh `chmod`( chmod ). Cách sử dụng cơ bản của chmod là:
```sh
chmod [OPTIONS] MODE FILE
```
* Bạn có thể chỉ định `MODE`theo hai cách: sửa đổi chế độ quyền hiện có hoặc tạo một chế độ hoàn toàn mới để ghi đè lên chế độ cũ.

* Ở cấp độ này, chúng ta sẽ tìm hiểu về cách thứ nhất: sửa đổi một chế độ hiện có. `chmod`Cho phép bạn điều chỉnh quyền hạn với định dạng chế độ là `WHO+/- WHAT`, trong đó `WHO`là người dùng/nhóm/khác và `WHAT`là đọc/ghi/thực thi. Ví dụ, để thêm quyền đọc cho người dùng sở hữu , bạn sẽ chỉ định chế độ là `u+r`. `w`Quyền ghi và `x`thực thi cho gnhóm và `o`các chế độ khác (hoặc atất cả các chế độ) được chỉ định theo cùng một cách. Thêm ví dụ:
```sh
`u+r`Như đã nêu ở trên, thao tác này bổ sung quyền đọc cho quyền hạn của người dùng.
`g+w`xThêm quyền ghi và thực thi vào quyền hạn của nhóm.
`o-w` Loại bỏ quyền ghi cho người dùng khác.
`a-rwx`Xóa bỏ tất cả quyền hạn cho người dùng, nhóm và toàn thế giới.
```
Vì thế:
```sh
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chmod go-rwx *
root@dojo:~# ls -l
total 4
-rw------- 1 hacker root    0 May 22 13:42 college_file
drwx------ 2 root   root 4096 May 22 13:42 pwn_directory
root@dojo:~#
```
* Trong thử thách này, bạn phải thay đổi quyền truy cập của `/flag`tập tin để có thể đọc được nó! Thông thường, bạn cần phải là chủ sở hữu của tập tin để thay đổi quyền truy cập, nhưng tôi đã làm cho `chmod`lệnh này trở nên vô cùng mạnh mẽ ở cấp độ này, và bạn có thể làm `chmod`bất cứ điều gì bạn muốn ngay cả khi bạn chỉ là `hacker`người dùng. Đây là một quyền lực tối thượng. `/flag`Tập tin thuộc sở hữu của `root`, và bạn không thể thay đổi điều đó, nhưng bạn có thể làm cho nó có thể đọc được. Hãy bắt tay vào giải quyết thử thách này!
* Lệnh `chmod` được dùng để thiết lập hoặc thay đổi quyền truy cập của 1 tệp tin(file) hoặc thư mục(folder). Lệnh này giúp kiểm soát xem ai được phép đọc, sửa hay thực thi dữ liệu đó.
* VD:- Với chủ sở hữu `chmod u+r` : thêm quyền đọc cho chủ sở hữu
     - Với nhóm sở hữu `chmod g+r` : thêm quyền đọc cho nhóm sở hữu
     - Với những ng dùng khác trong hệ thống `chmod o+r` : Thêm quyền đọc cho mọi ng dùng
     - Với cả 3 nhóm trên `chmod a+r` : cấp quyền đọc cho tất cả mọi người
</details>
<details>
  <summary><code>🏴Executable Files(Tệp thực thi)</code></summary>

 * Cho đến nay, bạn chủ yếu làm việc với quyền đọc . Điều này hợp lý, vì bạn đã cấp `/flag`quyền đọc cho tệp. Ở cấp độ này, chúng ta sẽ tìm hiểu về quyền thực thi.

* Khi bạn gọi một chương trình, chẳng hạn như `/challenge/run`, Linux sẽ chỉ thực sự thực thi nó nếu bạn có quyền truy cập thực thi vào tệp chương trình đó. Hãy xem xét:
```sh
hacker@dojo:~$ ls -l /challenge/run
-rwxr-xr-x 1 root root    0 May 22 13:42 /challenge/run
hacker@dojo:~$ /challenge/run
Successfully ran the challenge!
hacker@dojo:~$
```
* Trong trường hợp này, `/challenge/run`chương trình chạy vì người dùng có quyền thực thi hacker. Vì tệp tin thuộc sở hữu của `root`người dùng và `root`nhóm, nên cần phải thiết lập quyền thực thi `other`. Nếu chúng ta xóa các quyền này, quá trình thực thi sẽ thất bại!
```sh
hacker@dojo:~$ chmod o-x /challenge/run
hacker@dojo:~$ ls -l /challenge/run
-rwxr-xr-- 1 root root    0 May 22 13:42 /challenge/run
hacker@dojo:~$ /challenge/run
bash: /challenge/run: Permission denied
hacker@dojo:~$
```
* Trong thử thách này, `/challenge/run`chương trình sẽ cung cấp cho bạn lá cờ, nhưng trước tiên bạn phải làm cho nó có thể thực thi được! Hãy nhớ mật khẩu của bạn `chmod`và chương trình sẽ `/challenge/run`cho bạn biết lá cờ!
* <img width="293" height="92" alt="image" src="https://github.com/user-attachments/assets/bb01a38b-96eb-4f14-ba3c-047a1107254c" />
- Ở thử thách này ban đầu ta phải chạy lệnh `ls -l /challenge/run` để check xem các quyền hạn của ng dùng root sau đó ta sử dụng lệnh `chmod u+x` để cấp cho chủ sở hữu quyền thực thi chạy lệnh `/challenge/run` sau khi có quyền thực thi thì ta chạy lệnh này để lấy flag.
* Lưu ý của bài này chủ sở hữu là của chính root nên ta thêm quyền thực thi cho `u` còn với những bài khác tùy vào bài mà ta lựa chọn sử dụng `u`,`g`,`o`,hay `a`.

</details>
<details>
  <summary><code>🏴Permission Tweaking Practice(Thực hành điều chỉnh quyền)</code></summary>

* Bạn nghĩ mình có thể làm được không chmod? Cùng luyện tập nào!

* Thử thách này yêu cầu bạn thay đổi quyền truy cập của `/challenge/pwn` tập tin theo những cách cụ thể một vài lần liên tiếp. Nếu bạn thay đổi quyền truy cập sai, trò chơi sẽ thiết lập lại và bạn có thể thử lại. Nếu bạn thay đổi quyền truy cập đúng tám lần liên tiếp, thử thách sẽ cho phép bạn `chmod /flag` tự mình đọc được tập tin đó :-) Khởi chạy `/challenge/run` để bắt đầu!
* chạy `/challenge/run` để bắt đầu sau đó dựa vào dữ kiệu của bài để viết tiếp.
  - VD: Từ `rw-r--r--` -> `rwxr--rwx` Ta sẽ chạy câu lệnh :  `chmod u+x,o+wx /challenge/pwn`
</details>
<details>
  <summary><code>🏴Permissions Setting Practice(Thực hành thiết lập quyền)</code></summary>

* Ngoài việc thêm và xóa quyền, như ở cấp độ trước, `chmod`bạn cũng có thể thiết lập toàn bộ quyền, ghi đè lên các quyền cũ. Điều này được thực hiện bằng cách sử dụng `=`thay vì `-`hoặc `+`. Ví dụ:
```sh
`u=rw`: Thiết lập quyền đọc và ghi cho người dùng, đồng thời xóa quyền thực thi.
`o=x`: Chỉ thiết lập quyền thực thi cho tất cả người dùng, xóa quyền đọc và ghi.
`a=rwx`: Thiết lập quyền đọc, ghi và thực thi cho người dùng, nhóm và toàn bộ cộng đồng!
```
* Nhưng nếu bạn muốn thay đổi quyền người dùng theo cách khác với quyền nhóm thì sao? Ví dụ, bạn muốn thiết lập quyền `rw`cho người dùng sở hữu, nhưng chỉ `r`cho nhóm sở hữu? Bạn có thể đạt được điều này bằng cách kết hợp nhiều chế độ `chmod`với `,`!
```sh
`chmod u=rw,g=r /challenge/pwn` Sẽ thiết lập quyền truy cập cho người dùng là đọc và ghi, và quyền truy cập cho nhóm là chỉ đọc.
`chmod a=r,u=rw /challenge/pwn` Sẽ thiết lập quyền đọc cho toàn bộ `u`,`g`,`o `và cập nhận thêm cho `u` quyền ghi.
```
* Ngoài ra, bạn có thể xóa sạch quyền truy cập bằng lệnh -:
```sh
`chmod u=rw,g=r,o=- /challenge/pwn`Sẽ thiết lập quyền đọc và ghi cho `u`, quyền đọc cho `g`, xóa sạch mọi quyền của `o`
```
* Hãy nhớ rằng, dấu `-`phẩy xuất hiện sau đó `=`nằm trong ngữ cảnh khác so với khi nó xuất hiện ngay sau dấu phẩy `u`hoặc `g`( `o`trong trường hợp đó, nó sẽ khiến một số phần cụ thể bị loại bỏ, chứ không phải toàn bộ).

* Cấp độ này mở rộng cấp độ trước bằng cách yêu cầu những thay đổi quyền hạn triệt để hơn, điều mà bạn sẽ cần `=`và cần `,`sử dụng chuỗi lệnh để đạt được. Chúc may mắn!
* Lưu ý khi xóa 1 hay 2 quyền của đối tượng sở hữu ta dùng lệnh có chứa dấu `-` ở phía sau đối tượng đó, còn muốn xóa toàn bộ ta có thể dùng dấu `=-` ở sau đối tượng đó.
</details>
<details>
  <summary><code>🏴The `SUID Bit`(Quyền `SUID Bit`)</code></summary>

* Như bạn đã tìm hiểu trong mô-đun trước, có nhiều trường hợp `root`người dùng không phải là người dùng thông thường cần quyền truy cập nâng cao để thực hiện một số tác vụ hệ thống nhất định. Quản trị viên hệ thống không thể có mặt để cung cấp mật khẩu mỗi khi người dùng muốn thực hiện một tác vụ mà chỉ `root`người dùng có quyền /sudo mới có thể làm được. Thay vào đó, bit quyền "Đặt ID người dùng" (SUID) cho phép người dùng chạy một chương trình với tư cách là chủ sở hữu của tệp chương trình đó.

* Đây thực chất chính là cơ chế được sử dụng để cho phép các chương trình thử thách bạn chạy đọc cờ hoặc, bên ngoài pwn.college, để kích hoạt các công cụ quản trị hệ thống như `su`, `sudo`, v.v. Quyền truy cập của một tập tin có SUID trông như thế này:
```sh
hacker@dojo:~$ ls -l /usr/bin/sudo
-rwsr-xr-x 1 root root 232416 Dec 1 11:45 /usr/bin/sudo
hacker@dojo:~$
```
* Phần `s`thay thế cho bit thực thi có nghĩa là chương trình có thể thực thi bằng SUID . Điều này có nghĩa là, bất kể người dùng nào chạy chương trình (miễn là họ có quyền thực thi), chương trình sẽ được thực thi với tư cách người dùng sở hữu (trong trường hợp này là `root`người dùng ).

* Với tư cách là chủ sở hữu của một tập tin, bạn có thể thiết lập bit SUID của tập tin đó bằng cách sử dụng lệnh chmod:
```sh
chmod u+s [program]
```
* Nhưng hãy cẩn thận! Việc cấp bit SUID cho một tệp thực thi thuộc sở hữu của người dùng `root`có thể tạo ra một lỗ hổng cho kẻ tấn công để chiếm quyền kiểm soát `root`. Bạn sẽ tìm hiểu thêm về điều này trong mô-đun Lạm dụng Chương trình .

* Bây giờ, chúng ta sẽ cho phép bạn thêm bit SUID vào `/challenge/getroot`chương trình để tạo ra một `root`shell cho phép bạn `cat`tự thiết lập cờ!M
* <img width="357" height="70" alt="image" src="https://github.com/user-attachments/assets/a0f71b36-cc03-4e35-884e-cc725b8a1cc9" />
* Lưu ý :
   - Cú pháp để bật SUID : Để gán bit SUID cho một file( với điều kiện bạn là chủ sở hữu file hoặc là        `root` ), ta dùng lệnh `chmod u+s <Tên File>`
   - Khi bit được bật, chữ `x` ở phần `user` sẽ chuyển thành chữ `s` VD:`rwx`-> `rws`

</details>
