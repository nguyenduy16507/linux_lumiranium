# Hello Hacker

* Module này sẽ dạy cho bạn những điều RẤT cơ bản về việc tương tác với dòng lệnh! Dòng lệnh cho phép bạn thực thi các lệnh. Khi bạn khởi chạy một terminal, nó sẽ thực thi một "shell" dòng lệnh, trông sẽ giống như thế này:
  ```Sh
  hacker@dojo:~$
  ```

* Đây được gọi là "dấu nhắc" (prompt), và nó đang nhắc bạn nhập vào một lệnh. Hãy cùng xem xét những gì đang diễn ra ở đây:
  * Phần `hacker` trong dấu nhắc là tên người dùng (username) của người dùng hiện tại. Trong môi trường DOJO của pwn.college, tên này là "hacker".
  * Trong ví dụ trên, phần `dojo` của dấu nhắc là tên máy chủ (hostname) của cỗ máy mà shell đang chạy trên đó (ví dụ, lời nhắc nhở này có thể hữu ích nếu bạn là một quản trị viên hệ thống phải làm việc với nhiều máy tính hàng ngày). Trong ví dụ trên, tên máy chủ là dojo, nhưng trong pwn.college, nó sẽ được bắt nguồn từ tên của thử thách (challenge) mà bạn đang giải quyết.
  * Ký tự `$` ở cuối dấu nhắc biểu thị rằng `hacker` không phải là một người dùng quản trị (administrative user). Trong các module sau này ở pwn.college, khi bạn học cách sử dụng các kỹ thuật khai thác (exploits) để trở thành người dùng quản trị, bạn sẽ thấy dấu nhắc biểu thị điều đó bằng cách in ra ký tự `#` thay vì `$`, và lúc đó bạn sẽ biết rằng mình đã chiến thắng!
* Dù sao đi nữa, dấu nhắc đang chờ lệnh của bạn. Hãy chuyển sang thử thách đầu tiên để học cách thực sự thực thi các lệnh!
<details>
<summary>🎦<code>The Command Line(Dòng lệnh)</code> </summary>

*Hello Students
Các bạn có thể đã từng nhìn thấy :
```sh
#echo Hello Hacker!
Hello hacker!
```
Nhưng điều gì thực sự xảy ra đằng sau ?

* **Command line ?** (Dòng lệnh)

Dòng lệnh (Còn được gọi là "Shell") là một giao diện mạnh mẽ với 1 máy tính. Ý tưởng cơ bản :
1.Bạn gõ 1 lệnh
2.Hệ thống thực thi nó và xuất ra các kết quả 

Thông thường, một lệnh sẽ chứa 1 chương trình và các tham số cho chương trình đó, được phân tách bằng khoảng trắng.

```sh
yans@asdf ~ cat flag
pwn_college{1337}
yans@asdf ~ $ █
```

Điều gì đã xảy ra?
1.Tôi đã bảo Shell chạy chương trình `cat` với đối số `flag`.
2.Shell đã tìm thấy tệp chương trình `cat` và khởi chạy nó thành 1 tiến trình `cat` với 1 đối số `flag`.
3.`cat` là 1 chương trình xuất ra các tệp. Nó đọc đối số `flag` và biết phải xuất ra tệp `flag`, tệp này chứa"pwn-college{1337}".
4.
* ** Command Parameters / Arguments**(Các tham số lệnh/các đối số)

Các tham số lệnh cũng được gọi là các "đối số".Một vài ví dụ:

Lệnh `echo` nhận nhiều đối số và chỉ đơn giản là in chúng ngược lại ra_terminal!_
```sh
yans@asdf:~$ echo Hello Hackers!
Hello HackerS!
yans@asdf:~$
```

Một đối số làm thay đổi chức năng của các lệnh. Những đối số này(thường) được đặt trước bằng 1 ký tự '-'(dấu gạch ngang). Ví dụ, đối số '-n' cho lệnh `echo` khiến lệnh echo không bắt đầu 1 dòng mới trước khi kết thúc.

```sh
yans@asdf:~$ echo -n Hello Hackers!
Hello Hackers!yans@asdf:~$
```
Các đối số dài hơn (thường) được đặt trước bằng `--`(hai dấu gạch ngang). Ví dụ,lệnh `date` hiển thị thời gian hiện tại, nhưng lại có các chế đô hoạt động khác (trong truồng hợp này, chuyển đổi múi giờ sang UTC):

```sh
  yans@asdf:~$ date
  Sun Aug 25 09:53:32 PM MST 2024
  yans@asdf:~$ date --utc
  Mon Aug 26 04:53:34 AM UTC 2024
  yans@asdf:~$
```
</details>

<details>
  <summary>🏴 <code>Intro to Commands(Giới thiệu về các lệnh)</code></summary>

  * Trong thử thách này, bạn sẽ gọi (invoke) lệnh đầu tiên của mình! Khi bạn gõ một lệnh và nhấn phím enter, lệnh sẽ được gọi, giống như thế này:
    ```sh
    hacker@dojo:~$ whoami
    hacker
    hacker@dojo:~$
    ```

  * Ở đây, người dùng đã thực thi lệnh `whoami`, lệnh này chỉ đơn giản là in ra tên người dùng (hacker) trên terminal. Khi lệnh kết thúc, shell lại một lần nữa hiển thị dấu nhắc, sẵn sàng cho lệnh tiếp theo.
  
  * Trong cấp độ (level) này, hãy gọi lệnh `hello` để lấy cờ (flag)! Hãy ghi nhớ: các lệnh trong Linux có phân biệt chữ hoa chữ thường (case sensitive): `hello` thì khác với `HELLO`.

  <img width="512" height="158" alt="image" src="https://github.com/user-attachments/assets/3c4a31f1-f90d-4b3b-b102-14132b977ae1" />



</details>

<details>
  <summary>🏴 <code>In tro Arguments</code></summary>

  * Hãy thử một thứ gì đó phức tạp hơn: một lệnh đi kèm với các __đối số__ (arguments), đây là cách chúng ta gọi phần dữ liệu bổ sung được truyền vào cho lệnh. Khi bạn gõ một dòng văn bản và nhấn phím enter, shell thực sự phân tích cú pháp (parses) đầu vào của bạn thành một lệnh và các đối số của nó. Từ đầu tiên là lệnh, và các từ tiếp theo sau đó là các đối số. Hãy quan sát:

    ```sh
    hacker@dojo:~$ echo Hello
    Hello
    hacker@dojo:~$
    ```

  * Trong trường hợp này, lệnh là `echo`, và đối số là `Hello`. `echo` là một lệnh đơn giản chuyên "vang lại" (in lại) tất cả các đối số của nó ra ngoài terminal, giống như bạn thấy trong phiên làm việc ở trên.

  * Hãy cùng xem xét `echo` với nhiều đối số:
    ```sh
    hacker@dojo:~$ echo Hello Hacker!
    Hello Hacker!
    hacker@dojo:~$
    ```
    
  * Trong trường hợp này, lệnh là `echo`, và `Hello` cùng với `Hacker!` là hai đối số truyền cho `echo`. Thật đơn giản!
  
  * Trong thử thách này, để lấy được cờ (flag), bạn phải chạy lệnh `hello` (KHÔNG PHẢI lệnh `echo`) với một đối số duy nhất là `hackers`. Hãy thử ngay bây giờ!

  * <img width="540" height="142" alt="image" src="https://github.com/user-attachments/assets/610a4a86-5238-4cb6-a357-19295f1cb576" />

  
</details>

<details>
  <summary>🏴 <code>Command History</code></summary>

  * Bạn sẽ phải gõ rất nhiều lệnh, và việc gõ mọi thứ từ đầu có thể gây phiền toái. Thật may mắn, shell có lưu lại lịch sử (history) của mọi lệnh mà bạn gọi.
  
  * Bạn có thể cuộn qua những lệnh đã được lưu đó bằng các phím mũi tên lên/xuống, và chúng ta sẽ thực hành điều đó trong thử thách này. Thử thách này sẽ chèn (inject) cờ (flag) vào trong lịch sử của bạn. Hãy mở một terminal lên, nhấn mũi tên lên, và lấy nó! Trong các thử thách khác, lịch sử sẽ chứa nhật ký (log) của các lệnh mà bạn đã chạy, vì vậy nếu bạn cần chạy lại một lệnh tương tự, bạn có thể sử dụng các phím mũi tên để cuộn qua và tìm nó!
  * <img width="944" height="152" alt="image" src="https://github.com/user-attachments/assets/250b64a7-22d1-46cd-b7de-98e76794bbd0" />

</details>
