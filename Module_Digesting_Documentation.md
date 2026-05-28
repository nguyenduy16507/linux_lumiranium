 **Digesting Documentation(Nghiên cứu,tiếp thu,tiêu hóa tài liệu)**
 * Module này sẽ dạy bạn một trong những kỹ năng Linux quan trọng nhất: tìm kiếm trợ giúp về cách sử dụng các chương trình. Kỹ năng này sẽ rất hữu ích cho bạn trong suốt quá trình học tập. Cùng tìm hiểu chi tiết bên dưới!

<details>
<summary><code>📒Resources(tài nguyên)</code></summary> 
  
* [/ https://man7.org/linux/man-pages] or (https://man7.org/linux/man-pages/)
  
</details>
<details>
<summary><code>🏴Learning From Documentation(Học hỏi từ tài liệu)</code></summary>

* Nhu cầu điển hình của bạn đối với tài liệu hướng dẫn là để tìm hiểu cách sử dụng tất cả các chương trình phức tạp này, và một trường hợp cụ thể là tìm hiểu các tham số cần chỉ định trên dòng lệnh. Mô-đun này chủ yếu sẽ đi sâu vào khái niệm đó, như một cách để tìm hiểu cách sử dụng các chương trình nói chung. Trong phần còn lại của mô-đun, bạn sẽ tìm hiểu nhiều cách khác nhau để yêu cầu trợ giúp từ môi trường về các chương trình, nhưng trước tiên, chúng ta sẽ tìm hiểu khái niệm đọc tài liệu hướng dẫn.

* Việc sử dụng chương trình đúng cách phụ thuộc phần lớn vào việc chỉ định chính xác các tham số cho chương trình. Hãy nhớ lại ví -adụ ls -atrong hidden filesbài tập của mô- đun Lệnh cơ bản : đó -alà một tham số cho biết lscần liệt kê cả các tệp ẩn và tệp không ẩn. Vì chúng ta muốn liệt kê các tệp ẩn, nên việc gọi hàm lsvới -atham số là cách sử dụng đúng trong trường hợp của chúng ta.

* Chương trình cho thử thách này là /challenge/challenge, và bạn cần gọi nó đúng cách để nhận được cờ. Giả sử đây là tài liệu hướng dẫn của nó:

* Chào mừng bạn đến với tài liệu hướng dẫn của chương trình /challenge/challenge! Để chạy chương trình này đúng cách, bạn cần truyền tham số cho nó --giveflag. Chúc may mắn! Với những thông tin đó, hãy đi lấy lá cờ!



* <img width="828" height="119" alt="image" src="https://github.com/user-attachments/assets/418e71f7-076e-49db-922b-d373a1aacec5" />

</details>

<details>
<summary><code>🏴Learning Complex Usage(Học cách sử dụng phức tạp)</code></summary> 

*Mặc dù việc sử dụng hầu hết các lệnh khá đơn giản, nhưng việc sử dụng một số lệnh lại có thể khá phức tạp. Ví dụ, các đối số của các lệnh như sed`and` awk, mà chúng ta chắc chắn sẽ không đề cập đến ngay bây giờ, lại là toàn bộ các chương trình trong một ngôn ngữ lập trình chuyên biệt! Nằm đâu đó giữa ` cdand` và `and` awklà các lệnh nhận đối số cho chính đối số của chúng...

* Nghe có vẻ điên rồ, nhưng bạn đã từng gặp điều này ở findcấp độ trong các Lệnh Cơ bản . Lệnh findnày có một -nameđối số, và -namebản thân đối số đó lại nhận một đối số khác chỉ định tên cần tìm kiếm. Nhiều lệnh khác cũng tương tự.

* Đây là tài liệu hướng dẫn cho cấp độ này /challenge/challenge:

  * Chào mừng đến với tài liệu hướng dẫn của chương trình /challenge/challenge! Chương trình này cho phép bạn in các tệp tùy ý ra thiết bị đầu cuối khi được cung cấp --printfileđối số. Đối số của --printfileđối số là đường dẫn của tệp        cần đọc. Ví dụ, lệnh /challenge/challenge --printfile /challenge/DESCRIPTION.md sẽ in ra mô tả của cấp độ!

 Với những tài liệu đó, hãy đi lấy lá cờ!

* <img width="863" height="102" alt="image" src="https://github.com/user-attachments/assets/22f58417-6779-4ec5-be13-cc6c563c61c1" />
  
</details>

<details>
<summary><code>🏴Reading Manuals(Đọc sách hướng dẫn)</code></summary>

* Cấp độ này giới thiệu manlệnh. manlà viết tắt của manual, và sẽ hiển thị (nếu có) hướng dẫn sử dụng của lệnh bạn truyền vào làm đối số. Ví dụ, giả sử chúng ta muốn tìm hiểu về lệnh yes( vâng , đây là một lệnh có thật):
```sh
hacker@dojo:~$ man yes
```
* Thao tác này sẽ hiển thị trang hướng dẫn sử dụng cho yes, trang này sẽ trông giống như thế này:
```sh
YES(1)                           User Commands                          YES(1)

NAME
       yes - output a string repeatedly until killed

SYNOPSIS
       yes [STRING]...
       yes OPTION

DESCRIPTION
       Repeatedly output a line with all specified STRING(s), or 'y'.

       --help display this help and exit

       --version
              output version information and exit

AUTHOR
       Written by David MacKenzie.

REPORTING BUGS
       GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
       Report any translation bugs to <https://translationproject.org/team/>

COPYRIGHT
       Copyright  ©  2020  Free Software Foundation, Inc.  License GPLv3+: GNU
       GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
       This is free software: you are free  to  change  and  redistribute  it.
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       Full documentation <https://www.gnu.org/software/coreutils/yes>
       or available locally via: info '(coreutils) yes invocation'

GNU coreutils 8.32               February 2022                          YES(1)
```
Các phần quan trọng là:
```sh
NAME(1)                           CATEGORY                          NAME(1)

NAME
	This gives the name (and short description) of the command or
	concept discussed by the page.

SYNOPSIS
	This gives a short usage synopsis. These synopses have a standard
	format. Typically, each line is a different valid invocation of the
	command, and the lines can be read as:

	COMMAND [OPTIONAL_ARGUMENT] SINGLE_MANDATORY_ARGUMENT
	COMMAND [OPTIONAL_ARGUMENT] MULTIPLE_ARGUMENTS...

DESCRIPTION
	Details of the command or concept, with detailed descriptions
	of the various options.

SEE ALSO
	Other man pages or online resources that might be useful.

COLLECTION                        DATE                          NAME(1)
```
  * Bạn có thể cuộn trang hướng dẫn bằng các phím mũi tên và PgUp/PgDn. Khi đọc xong trang hướng dẫn, bạn có thể nhấn qđể thoát.

* Các trang hướng dẫn (manpage) được lưu trữ trong một cơ sở dữ liệu tập trung. Nếu bạn tò mò, cơ sở dữ liệu này nằm trong /usr/share/manthư mục đó, nhưng bạn không cần phải tương tác trực tiếp với nó: bạn chỉ cần truy vấn nó bằng manlệnh. Các đối số của manlệnh không phải là đường dẫn tệp, mà chỉ là tên của các mục nhập (ví dụ: bạn chạy lệnh man yesđể tra cứu yestrang hướng dẫn, thay vì man /usr/bin/yeslệnh , lệnh này sẽ là đường dẫn thực tế đến yeschương trình nhưng sẽ dẫn đến manviệc hiển thị thông tin không chính xác).

* Thử thách ở cấp độ này có một tùy chọn bí mật mà khi bạn sử dụng, sẽ khiến thử thách in ra lá cờ. Bạn phải tìm hiểu tùy chọn này thông qua trang hướng dẫn sử dụng (man page) cho challenge!
 * <img width="1345" height="585" alt="image" src="https://github.com/user-attachments/assets/aa990012-4e05-4efc-b5b3-c0ae3ea9642e" />
 * <img width="994" height="105" alt="image" src="https://github.com/user-attachments/assets/3f72b0cb-a1c3-4e38-a1fa-500244126b94" />

</details>

<details>
<summary><code>🏴Searching Manuals(Tìm kiếm tài liệu hướng dẫn)</code></summary>
* Bạn có thể cuộn trang hướng dẫn sử dụng bằng các phím mũi tên (và PgUp/PgDn) và tìm kiếm bằng /. Sau khi tìm kiếm, bạn có thể nhấn nđể chuyển đến kết quả tiếp theo và Nđể quay lại kết quả trước đó. Thay vì /, bạn có thể sử dụng ?để tìm kiếm ngược lại!

* Hãy tìm tùy chọn cung cấp cờ bằng cách đọc trang hướng dẫn sử dụng challenge(man page).

* <img width="977" height="155" alt="image" src="https://github.com/user-attachments/assets/9aec7a1e-2843-4e49-992e-37c144b1fd7f" />

  
</details>

<details>
<summary><code>🏴Searching For Manuals(Tìm kiếm tài liệu hướng dẫn)</code></summary> 

* Cấp độ này khá hóc búa: nó giấu trang hướng dẫn sử dụng (manpage) cho thử thách bằng cách ngẫu nhiên hóa tên của nó. May mắn thay, tất cả các trang hướng dẫn sử dụng đều được tập hợp trong một cơ sở dữ liệu có thể tìm kiếm, vì vậy bạn sẽ có thể tìm kiếm trong cơ sở dữ liệu trang hướng dẫn sử dụng để tìm ra trang hướng dẫn sử dụng ẩn của thử thách! Để tìm ra cách tìm kiếm trang hướng dẫn sử dụng phù hợp, hãy đọc mantrang hướng dẫn sử dụng bằng cách thực hiện: man man!

* GỢI Ý 1: man man hướng dẫn bạn cách sử dụng nâng cao manlệnh này, và bạn phải sử dụng kiến ​​thức này để tìm ra cách tìm trang hướng dẫn ẩn (manpage) sẽ cho bạn biết cách sử dụng lệnh đó./challenge/challenge

* GỢI Ý 2: Mặc dù trang hướng dẫn được đặt tên ngẫu nhiên, bạn vẫn thực sự sử dụng nó /challenge/challengeđể lấy cờ!
* <img width="1286" height="626" alt="image" src="https://github.com/user-attachments/assets/e20c05ec-3940-4d00-99f6-c332a77a8cde" />
* <img width="1363" height="607" alt="image" src="https://github.com/user-attachments/assets/88146bd5-2043-49e4-abb9-9ca81979b68a" />
* <img width="1208" height="314" alt="image" src="https://github.com/user-attachments/assets/dec1edef-1c33-40b2-b9a7-888bc33af626" />

</details>

<details>
<summary><code>🏴Helpful Programs(Các chương trình hữu ích)</code></summary>

* Một số chương trình không có trang hướng dẫn sử dụng (man page), nhưng có thể cho bạn biết cách chạy chúng nếu được gọi kèm theo một đối số đặc biệt. Thông thường, đối số này là --help, nhưng đôi khi nó có thể là -hhoặc, trong những trường hợp hiếm hoi, -?, help, hoặc các giá trị khác thường như /?(mặc dù giá trị sau thường gặp hơn trên Windows).

* Ở cấp độ này, bạn sẽ thực hành đọc tài liệu của một chương trình --help. Hãy thử xem!
* <img width="1050" height="391" alt="image" src="https://github.com/user-attachments/assets/d55b15e5-b0dc-42bd-9143-2557648c82e6" />

</details>

<details>
<summary><code>🏴Help For builtins(Trợ giúp về các hàm tích hợp sẵn)</code></summary> 
  
* Một số lệnh, thay vì là các chương trình có trang hướng dẫn sử dụng và tùy chọn trợ giúp, được tích hợp sẵn vào chính shell. Chúng được gọi là các lệnh tích hợp (builtins) . Các lệnh tích hợp được gọi giống như các lệnh thông thường, nhưng shell xử lý chúng nội bộ thay vì khởi chạy các chương trình khác. Bạn có thể lấy danh sách các lệnh tích hợp của shell bằng cách chạy lệnh ` builtins` help , như sau:
```sh
hacker@dojo:~$ help
Bạn có thể nhận được trợ giúp về một vấn đề cụ thể bằng cách truyền nó cho hàm helptích hợp sẵn. Hãy cùng xem một hàm tích hợp sẵn mà chúng ta đã sử dụng trước đó, cd!

hacker@dojo:~$ help cd
cd: cd [-L|[-P [-e]] [-@]] [dir]
    Change the shell working directory.
    
    Change the current directory to DIR.  The default DIR is the value of the
    HOME shell variable.
...
```
* Thông tin hữu ích đấy! Trong thử thách này, chúng ta sẽ thực hành sử dụng lệnh helpđể tra cứu trợ giúp cho các lệnh tích hợp sẵn. challengeLệnh trong thử thách này là một lệnh tích hợp sẵn của shell, chứ không phải là một chương trình. Giống như trước đây, bạn cần tra cứu trợ giúp của nó để tìm ra giá trị bí mật cần truyền cho lệnh đó!

*<img width="854" height="380" alt="image" src="https://github.com/user-attachments/assets/d94b25f1-3c81-4a4f-be12-61c4b68d360c" />

  
</details>
