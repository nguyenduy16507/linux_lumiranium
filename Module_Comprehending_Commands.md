# Comprehending Conmands
* Module này sẽ giới thiệu cho bạn một số lệnh Linux hữu ích, sẽ rất có ích cho bạn trong suốt quá trình học tập tại đây! Danh sách này còn lâu mới đầy đủ, và chúng tôi sẽ tiếp tục mở rộng module này, nhưng chừng đó sẽ đủ để bạn bắt đầu.

Vậy thì, không để mất thêm thời gian nữa, chúng ta hãy cùng học một số lệnh!

<details>
<summary><code>🏴cat: not the pet, but the command!(Mèo không phải thú cưng mà là mệnh lệnh) </code> </summary>

* Một trong những lệnh quan trọng nhất của Linux là **cat**`.`. catLệnh này thường được sử dụng để đọc nội dung các tập tin, ví dụ như sau:
```sh
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
One of the most critical Linux commands is `cat`.
`cat` is most often used for reading out files, like so:
```
Lệnh cat này sẽ nối nhiều tập tin lại với nhau (do đó có tên gọi như vậy) nếu được cung cấp nhiều đối số. Ví dụ:
```sh
hacker@dojo:~$ cat myfile
This is my file!
hacker@dojo:~$ cat yourfile
This is your file!
hacker@dojo:~$ cat myfile yourfile
This is my file!
This is your file!
hacker@dojo:~$ cat myfile yourfile myfile
This is my file!
This is your file!
This is my file!
```
* Cuối cùng, nếu bạn không đưa ra bất kỳ đối số nào, catchương trình sẽ đọc dữ liệu từ thiết bị đầu cuối và xuất ra. Chúng ta sẽ tìm hiểu điều đó trong các thử thách sau...

Trong thử thách này, tôi sẽ sao chép cờ vào một flag tệp trong thư mục chính của bạn (nơi shell của bạn khởi chạy). Hãy đọc nó bằng lệnh cat!

* <img width="887" height="135" alt="image" src="https://github.com/user-attachments/assets/b04756fd-6303-4533-8e54-d2b01f349f61" />
</details>

<details>
<summary><code>🏴catting absolute paths(Con đường tuyệt đối của mèo)</code></summary>

* Ở cấp độ cuối cùng, bạn đã cat flag đọc cờ từ thư mục chính của mình! Tất nhiên, bạn có thể chỉ định catcác đối số của 's dưới dạng đường dẫn tuyệt đối:
```sh
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
In the last level, you did `cat flag` to read the flag out of your home directory!
You can, of course, specify `cat`'s arguments as absolute paths:
...
```
* Trong thử thách này, tôi sẽ không sao chép tệp đó vào thư mục chính của bạn, nhưng tôi sẽ làm cho nó có thể đọc được. Bạn có thể đọc nó bằng catđường dẫn tuyệt đối: /flag.

THÔNG TIN THÚ VỊ: Đây là nơi chứa/flag cờ hiệu trong pwn.college, nhưng không giống như trong thử thách này, bạn thường không thể truy cập trực tiếp vào tệp đó.

* <img width="725" height="97" alt="image" src="https://github.com/user-attachments/assets/30e6b17c-a06e-41d3-8a77-f99856fb8db2" />
</details>

<details>
<summary><code>🏴more catting practice(Luyện tập cat)</code></summary>

* Bạn có thể chỉ định đủ loại đường dẫn làm đối số cho các lệnh, và chúng ta sẽ thực hành thêm một số ví dụ với cat. Ở cấp độ này, tôi sẽ đặt cờ trong một thư mục nào đó khá phức tạp, và tôi sẽ không cho phép bạn thay đổi thư mục bằng cd, vì vậy bạn sẽ không thể cat flagsử dụng lệnh đó. Bạn phải lấy cờ bằng đường dẫn tuyệt đối, bất kể nó nằm ở đâu.
* <img width="888" height="287" alt="image" src="https://github.com/user-attachments/assets/5d02ed9b-2b8a-4dee-bffc-367f0476773b" />
</details>

<details> 
<summary><code>🏴grepping for a needle in a haystack(Mò kim đáy bể như mò kim đáy bể)</code></summary>
* Đôi khi, các tập tin bạn cần cattìm lại quá lớn. May mắn thay, chúng ta có greplệnh để tìm kiếm nội dung cần thiết! Chúng ta sẽ cùng tìm hiểu lệnh này trong bài tập này.

* Có nhiều cách để làm điều đó grep, và chúng ta sẽ tìm hiểu một cách ở đây:
```sh
hacker@dojo:~$ grep SEARCH_STRING /path/to/file
```
* Khi được gọi như thế này, grepchương trình sẽ tìm kiếm trong tệp các dòng văn bản có chứa SEARCH_STRINGvà in chúng ra bảng điều khiển.

* Trong thử thách này, tôi đã đưa một trăm nghìn dòng văn bản vào tập /challenge/data.txttin. grep Nó dành cho lá cờ!

GỢI Ý: Lá cờ luôn bắt đầu bằng dòng chữ pwn.college.( Mò kim trong đống rơm )

* <img width="880" height="119" alt="image" src="https://github.com/user-attachments/assets/467ca220-e953-485d-adf2-75e21019ecc2" />

</details>

<details>
<summary><code>🏴comparing files(So sánh các tệp)</code></summary>
* Khi tìm kiếm sự khác biệt giữa các tệp tin tương tự, việc nhìn bằng mắt thường có thể không phải là phương pháp hiệu quả nhất! Đây là lúc diff lệnh này trở nên vô cùng hữu ích.

* **diff** Công cụ này so sánh hai tệp tin từng dòng một và cho bạn thấy chính xác những điểm khác biệt giữa chúng. Ví dụ:
```sh
hacker@dojo:~$ cat file1
hello
world
hacker@dojo:~$ cat file2
hello
universe
hacker@dojo:~$ diff file1 file2
2c2
< world
---
> universe
```
* Kết quả đầu ra cho chúng ta biết rằng dòng 2 đã thay đổi ( 2c2), với worldtrong tệp đầu tiên ( <) được thay thế bằng universetrong tệp thứ hai ( >).

* Đôi khi, khi thêm các dòng mới, bạn sẽ thấy điều gì đó như sau:
```sh
hacker@dojo:~$ cat old
pwn
hacker@dojo:~$ cat new
pwn
college
hacker@dojo:~$ diff old new
1a2
> college
```
* Điều này cho chúng ta biết rằng sau dòng 1 trong tệp đầu tiên, tệp thứ hai có thêm một dòng nữa ( 1a2có nghĩa là "sau dòng 1 của tệp 1, hãy thêm dòng 2 của tệp 2").

* Giờ đến lượt thử thách của bạn! Có hai tập tin trong thư mục /challenge:

  * /challenge/decoys_only.txt Chứa 100 lá cờ giả
  * /challenge/decoys_and_real.txt Bao gồm tất cả 100 lá cờ giả cộng với một lá cờ thật.
* Hãy sử dụng diffcông cụ này để tìm ra điểm khác biệt giữa các tập tin và lấy cờ (flag) của bạn!
* <img width="819" height="54" alt="image" src="https://github.com/user-attachments/assets/143f8bed-8803-44d0-b4eb-b501e884d5a4" />
* <img width="826" height="32" alt="image" src="https://github.com/user-attachments/assets/3d9418d9-c681-49a9-b238-bce008d4a15e" />
* <img width="849" height="135" alt="image" src="https://github.com/user-attachments/assets/946180d6-c4a0-4fd8-9d50-a00cdf1f78c1" />

</details>

<details>
<summary><code>🏴listing files(liệt kê các tệp)</code></summary>
  
* Cho đến nay, chúng tôi đã hướng dẫn bạn cách tương tác với các tập tin. Nhưng các thư mục có thể chứa rất nhiều tập tin (và các thư mục khác) bên trong, và chúng tôi không phải lúc nào cũng có mặt để hướng dẫn bạn về tên của chúng. Bạn cần học cách liệt kê nội dung của chúng bằng lệnh **ls** !

* **ls** Lệnh này sẽ liệt kê các tệp trong tất cả các thư mục được cung cấp làm đối số, và trong thư mục hiện tại nếu không có đối số nào được cung cấp. Lưu ý:
```sh
hacker@dojo:~$ ls /challenge
run
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$
```
* Trong thử thách này, chúng tôi đã đặt tên /challenge/runngẫu nhiên cho các tệp! Hãy liệt kê các tệp /challenge để tìm chúng.
* 
* <img width="832" height="197" alt="image" src="https://github.com/user-attachments/assets/c52c788d-1764-4542-816c-af929e796424" />

</details>

<details>
<summary><code>🏴touching files(Tạo tệp)</code></summary>
 
* Tất nhiên, bạn cũng có thể tạo tệp! Có nhiều cách để làm điều này, nhưng ở đây chúng ta sẽ xem xét một lệnh đơn giản. Bạn có thể tạo một tệp mới, trống bằng cách sử dụng lệnh touch:
```sh
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ touch pwnfile
hacker@dojo:/tmp$ ls
pwnfile
hacker@dojo:/tmp$
```
 
* Đơn giản vậy thôi! Ở màn chơi này, hãy tạo hai tập tin: /tmp/pwnvà /tmp/college, rồi chạy/challenge/runđể nhận cờ!
* <img width="699" height="131" alt="image" src="https://github.com/user-attachments/assets/c6ea0e33-d62b-423e-b2fa-e0e216dd6e4a" />

</details>

<details>
 <summary><code>🏴removing files(Xóa tệp)</code></summary>
 
* Các tập tin nằm rải rác khắp nơi. Giống như vỏ kẹo, cuối cùng sẽ có quá nhiều tập tin. Trong cấp độ này, chúng ta sẽ học cách dọn dẹp!

* Trong Linux, bạn xóa tập tin bằng rmlệnh như sau:
```sh
hacker@dojo:~$ touch PWN
hacker@dojo:~$ touch COLLEGE
hacker@dojo:~$ ls
COLLEGE     PWN
hacker@dojo:~$ rm PWN
hacker@dojo:~$ ls
COLLEGE
hacker@dojo:~$
```
* Hãy cùng luyện tập. Thử thách này sẽ tạo một delete_me ldtệp trong thư mục chính của bạn! Hãy xóa nó, sau đó chạy lệnh /challenge/check, lệnh này sẽ đảm bảo bạn đã xóa tệp và sẽ cung cấp cho bạn cờ!
* <img width="711" height="210" alt="image" src="https://github.com/user-attachments/assets/3fc98bf5-0a3c-4dc9-85dc-5da01c830aed" />

</details>

<details>
 <summary><code>🏴moving files(Di chuyển tệp)</code></summary>

* Bạn cũng có thể di chuyển các tập tin bằng mvlệnh này. Cách sử dụng rất đơn giản:
```sh
hacker@dojo:~$ ls
my-file
hacker@dojo:~$ cat my-file
PWN!
hacker@dojo:~$ mv my-file your-file
hacker@dojo:~$ ls
your-file
hacker@dojo:~$ cat your-file
PWN!
hacker@dojo:~$
```
* Thử thách này yêu cầu bạn di chuyển /flagtập tin vào /tmp/hack-the-planet(hãy làm đi)! Khi hoàn thành, hãy chạy lệnh /challenge/check, lệnh này sẽ kiểm tra mọi thứ và trả về cờ cho bạn.
* <img width="816" height="204" alt="image" src="https://github.com/user-attachments/assets/7caacd36-b610-4e49-929c-f57c3622f2b3" />

</details>

<details>
<summary><code>🏴copying files(Sao chép tệp)</code></summary>

* Nhưng nếu bạn muốn giữ lại tệp gốc thì sao? Bạn có thể làm điều đó bằng cplệnh này. Cách sử dụng tương tự như với lệnh kia mv, nhưng nó sẽ giữ lại tệp nguồn.

* Thử thách này yêu cầu bạn sao chép /flagtệp vào /tmp/hack-the-planet(hãy làm đi)! Khi hoàn thành, hãy chạy lệnh /challenge/check, lệnh này sẽ kiểm tra mọi thứ và trả về cờ cho bạn.
* <img width="828" height="169" alt="image" src="https://github.com/user-attachments/assets/5a31ddf3-457b-455f-bdc1-ae11585cb24c" />

</details>

<details>
<summary><code>🏴hidden files(Tệp ẩn)</summary>

* Điều thú vị là, theo mặc định, lệnh lsnày không liệt kê tất cả các tập tin. Linux có một quy ước rằng các tập tin bắt đầu bằng dấu phẩy .sẽ không hiển thị theo mặc định trong lệnh này lsvà trong một vài ngữ cảnh khác. Để xem chúng bằng lệnh này ls, bạn cần gọi lệnh ls với -a cờ , như sau:
  
```sh
hacker@dojo:~$ touch pwn
hacker@dojo:~$ touch .college
hacker@dojo:~$ ls
pwn
hacker@dojo:~$ ls -a
.college	pwn
hacker@dojo:~$
```

* Giờ đến lượt bạn! Hãy đi tìm lá cờ, nó được giấu dưới dạng một tệp có tiền tố dấu chấm trong thư mục /.

* <img width="706" height="196" alt="image" src="https://github.com/user-attachments/assets/fab8e87a-e275-4ca9-9d74-b1b0a65d0eef" />

</details>

<details>
 <summary><code>🏴An Epic Filesystem Quest(Cuộc phiêu lưu sử thi trong hệ thống tệp tin)</code></summary>

* Với kiến ​​thức của bạn về cd, ls, và cat, chúng ta sẵn sàng chơi một trò chơi nhỏ!
* Chúng ta sẽ bắt đầu bằng /. Thông thường:
```sh
hacker@dojo:~$ cd /
hacker@dojo:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  dev        flag  lib   lib64  media   opt  root  sbin  sys  usr
```
* Nhiều nội dung thật đấy! Rồi một ngày nào đó, bạn sẽ quen thuộc với chúng, nhưng ngay bây giờ, bạn có thể đã nhận ra flag catcác tệp và challengethư mục rồi.
* Trong thử thách này, tôi đã giấu lá cờ ! Ở đây, bạn sẽ sử dụng lsvà catđể lần theo dấu vết của tôi và tìm ra nó! Đây là cách thực hiện:

   0.Manh mối đầu tiên nằm ở đây /. Hãy đi đến đó.
   1.Hãy tìm kiếm bằng lệnh `ls` .Sẽ có một thư mục tên là HINT hoặc CLUE hoặc một cái tên tương tự!
   2.cat Hãy đọc gợi ý từ tập tin đó!
   3.Tùy thuộc vào gợi ý, hãy chuyển sang thư mục tiếp theo (hoặc không!).
   4.Hãy lần theo các manh mối để tìm thấy lá cờ!
   Chúc may mắn!
  * <img width="873" height="920" alt="image" src="https://github.com/user-attachments/assets/dfbae53f-2454-42ac-ac82-82eee6088c76" />
  * <img width="868" height="922" alt="image" src="https://github.com/user-attachments/assets/5ecd5953-9f06-4943-894c-f0c2e3cfc410" />
  * <img width="887" height="922" alt="image" src="https://github.com/user-attachments/assets/b8f46aee-14d0-4149-a655-55a4f274991a" />
  * <img width="882" height="237" alt="image" src="https://github.com/user-attachments/assets/99a3373b-c989-4d55-9b9f-add461019b0f" />


</details>

<details>
 <summary><code>🏴making directories(tạo thư mục)</code></summary>

* Chúng ta có thể tạo tập tin. Còn thư mục thì sao? Bạn tạo thư mục bằng lệnh . Sau đó ,mkdir bạn có thể đặt tập tin vào đó!

Đồng hồ:
```sh
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ mkdir my_directory
hacker@dojo:/tmp$ ls
my_directory
hacker@dojo:/tmp$ cd my_directory
hacker@dojo:/tmp/my_directory$ touch my_file
hacker@dojo:/tmp/my_directory$ ls
my_file
hacker@dojo:/tmp/my_directory$ ls /tmp/my_directory/my_file
/tmp/my_directory/my_file
hacker@dojo:/tmp/my_directory$
```
* Bây giờ, hãy tạo một /tmp/pwnthư mục và tạo một collegetệp trong đó! Sau đó chạy lệnh này /challenge/run, lệnh này sẽ kiểm tra giải pháp của bạn và cung cấp cho bạn cờ!
* <img width="685" height="369" alt="image" src="https://github.com/user-attachments/assets/079f6ad3-964d-455e-b5b1-252b9970a846" />

</details>

<details>
<summary><code>🏴finding files(tìm kiếm tệp)</code></summary>
 
* Vậy là chúng ta đã biết cách liệt kê, đọc và tạo tập tin. Nhưng làm thế nào để tìm chúng? Chúng ta sử dụng findlệnh!

* Lệnh này findcó thể nhận các đối số tùy chọn mô tả tiêu chí tìm kiếm và vị trí tìm kiếm. Nếu bạn không chỉ định tiêu chí tìm kiếm, findnó sẽ khớp với mọi tệp. Nếu bạn không chỉ định vị trí tìm kiếm, findnó sẽ sử dụng thư mục làm việc hiện tại ( .). Ví dụ:
```sh
hacker@dojo:~$ mkdir my_directory
hacker@dojo:~$ mkdir my_directory/my_subdirectory
hacker@dojo:~$ touch my_directory/my_file
hacker@dojo:~$ touch my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find
.
./my_directory
./my_directory/my_subdirectory
./my_directory/my_subdirectory/my_subfile
./my_directory/my_file
hacker@dojo:~$
```
* Và khi chỉ định vị trí tìm kiếm:
``` sh
hacker@dojo:~$ find my_directory/my_subdirectory
my_directory/my_subdirectory
my_directory/my_subdirectory/my_subfile
hacker@dojo:~$
```
* Và dĩ nhiên, chúng ta có thể chỉ định các tiêu chí! Ví dụ, ở đây, chúng ta lọc theo tên:
```sh
hacker@dojo:~$ find -name my_subfile
./my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find -name my_subdirectory
./my_directory/my_subdirectory
hacker@dojo:~$
```
* Bạn có thể tìm kiếm toàn bộ hệ thống tập tin nếu muốn!
```sh
hacker@dojo:~$ find / -name hacker
/home/hacker
hacker@dojo:~$
```
* Giờ đến lượt bạn. Tôi đã giấu lá cờ trong một thư mục ngẫu nhiên trên hệ thống tập tin. Nó vẫn có tên là flag. Hãy tìm nó đi!

* Một vài lưu ý. Thứ nhất, có những tập tin khác cùng tên flagtrên hệ thống tập tin. Đừng hoảng sợ nếu tập tin đầu tiên bạn thử không chứa cờ cần tìm. Thứ hai, có rất nhiều vị trí trên hệ thống tập tin mà người dùng thông thường không thể truy cập. Những vị trí này sẽ gây findra lỗi, nhưng bạn có thể bỏ qua chúng; chúng tôi sẽ không giấu cờ ở đó! Cuối cùng, quá trình này findcó thể mất một lúc; hãy kiên nhẫn!
* <img width="839" height="774" alt="image" src="https://github.com/user-attachments/assets/d7ead042-2070-4546-87dc-c35d07f21dc6" />
* <img width="852" height="808" alt="image" src="https://github.com/user-attachments/assets/9a00fd0d-9420-4cff-8d76-4b56eec353cc" />

</details>

<details>
 <summary><code>🎥Symbolic Links(Liên kết tượng chưng)</code></summary>

 * **A deeper look at files(Phân tích sâu hơn về các tập tin)**

    Có nhiều loại tệp khác nhau. Bạn có thể sử dụng lệnh `ls -ld /path/to/your/file` để kiểm tra.

    ```sh
    yans@asdf ~ $ ls -ld /home/yans/flags
    drwxr-xr-x 2 yans users 4096 Aug 19 06:30 /home/yans/flags
    yans@asdf ~ $ ls -ld /home/yans/flags/TOPSECRET
    -rw-r--r-- 1 yans users 18 Aug 19 06:30 /home/yans/flags/TOPSECRET
    yans@asdf ~ $ █
    ```

    * Types:

      * `-` là một tệp thông thường (regular file)
      * `d` là một thư mục (các thư mục thực chất chỉ là các tệp đặc biệt)
      * `l` là một liên kết tượng trưng (symbolic link - một tệp con trỏ một cách trong suốt đến một tệp hoặc thư mục khác.)
      * `p` là một đường ống có tên (named pipe - còn được gọi là FIFO. Bạn sẽ trở nên rất quen thuộc với những thứ này trong module này!)
      * `c` là một tệp thiết bị ký tự (character device file - tức là, được hỗ trợ/đại diện bởi một thiết bị phần cứng tạo ra hoặc nhận các luồng dữ liệu, chẳng hạn như micrô)
      * `b` là một tệp thiết bị khối (block device file - tức là, được hỗ trợ/đại diện bởi một thiết bị phần cứng lưu trữ và tải các khối dữ liệu, chẳng hạn như ổ cứng)
      * `s` là một unix socket (về cơ bản là một kết nối mạng cục bộ được đóng gói trong một tệp)

  * **Symbolic (AKA soft) links?(Liên kết tượng trưng - hay còn gọi là liên kết mềm)**

    Một liên kết tượng trưng/mềm (symbolic/soft link) là một loại tệp đặc biệt tham chiếu đến một tệp khác.

    Chúng được tạo ra bằng lệnh `ln -s`, `-s` viết tắt của _symbolic_

    ```sh
    yans@asdf ~ $ ln -s flags/TOPSECRET link_to_the_flag
    yans@asdf ~ $ ls -l
    total 24
    drwxr-xr-x 2 yans users 4096 Aug 19 06:27 Desktop
    drwxr-xr-x 2 yans users 4096 Aug 19 06:27 Documents
    drwxr-xr-x 2 yans users 4096 Aug 19 06:27 Downloads
    drwxr-xr-x 2 yans users 4096 Aug 19 06:27 Pictures
    drwxr-xr-x 2 yans users 4096 Aug 19 06:27 code
    drwxr-xr-x 2 yans users 4096 Aug 19 06:30 flags
    lrwxrwxrwx 1 yans users   15 Aug 19 07:29 link_to_the_flag -> flags/TOPSECRET
    yans@asdf ~ $ cat ./link_to_the_flag
    pwn_college{1337}
    yans@asdf ~ $ █
    ```

    Bạn cũng có thể liên kết các thư mục:

    ```sh
    yans@asdf ~ $ ln -s flags link_to_flags_dir
    yans@asdf ~ $ ls -ld link_to_flags_dir
    lrwxrwxrwx 1 yans users 5 Aug 19 07:32 link_to_flags_dir -> flags
    yans@asdf ~ $ cat link_to_flags_dir/TOPSECRET
    pwn_college{1337}
    yans@asdf ~ $ █
    ```

  * **Symbolic link gotchas(Những cạm bẫy trong liên kết tượng trưng)** 

    Hãy cẩn thận (Beware): các liên kết tượng trưng trỏ đến các đường dẫn tương đối (relative paths) sẽ mang tính tương đối **so với thư mục chứa liên kết đó**!

    ```sh
    yans@asdf ~ $ ln -s flags/TOPSECRET link_to_the_flag
    yans@asdf ~ $ ls -l link_to_the_flag
    lrwxrwxrwx 1 yans users 15 Aug 19 07:45 link_to_the_flag -> flags/TOPSECRET
    yans@asdf ~ $ cat link_to_the_flag
    pwn_college{1337}
    yans@asdf ~ $ mv link_to_the_flag /tmp
    yans@asdf ~ $ ls -l /tmp
    total 0
    lrwxrwxrwx 1 yans users 15 Aug 19 07:45 link_to_the_flag -> flags/TOPSECRET
    yans@asdf ~ $ cat /tmp/link_to_the_flag
    cat: /tmp/link_to_the_flag: No such file or directory
    yans@asdf ~ $ █
    ```

    So với đường dẫn tuyệt đối (absolute path):

    ```sh
    yans@asdf ~ $ ln -s /home/yans/flags/TOPSECRET link_to_the_flag
    yans@asdf ~ $ ls -l link_to_the_flag
    lrwxrwxrwx 1 yans users 26 Aug 19 07:49 link_to_the_flag -> /home/yans/flags/TOPSECRET
    yans@asdf ~ $ cat link_to_the_flag
    pwn_college{1337}
    yans@asdf ~ $ mv link_to_the_flag /tmp
    yans@asdf ~ $ ls -l /tmp/link_to_the_flag
    lrwxrwxrwx 1 yans users 26 Aug 19 07:49 /tmp/link_to_the_flag -> /home/yans/flags/TOPSECRET
    yans@asdf ~ $ cat /tmp/link_to_the_flag
    pwn_college{1337}
    yans@asdf ~ $ █
    ```

    
  * **Hard Links?(Liên kết cứng)**

    Sự tồn tại của các liên kết mềm (soft links) ngụ ý sự tồn tại của một liên kết cứng (hard link).

    Các liên kết cứng (được tạo bằng lệnh ln mà không có đối số -s) tham chiếu trực tiếp đến tệp gốc bằng cách thực hiện phép thuật (magic) với những từ ngữ đáng sợ như "inode".

    ```sh
    yans@asdf ~ $ ln flags/TOPSECRET hard_link_to_flag
    yans@asdf ~ $ ls -l
    total 28
    drwxr-xr-x 2 yans users 4096 Aug 19 06:27 Desktop
    drwxr-xr-x 2 yans users 4096 Aug 19 06:27 Documents
    drwxr-xr-x 2 yans users 4096 Aug 19 06:27 Downloads
    drwxr-xr-x 2 yans users 4096 Aug 19 06:27 Pictures
    drwxr-xr-x 2 yans users 4096 Aug 19 06:27 code
    drwxr-xr-x 2 yans users 4096 Aug 19 07:33 flags
    -rw-r--r-- 2 yans users   18 Aug 19 06:30 hard_link_to_flag
    yans@asdf ~ $ cat hard_link_to_flag
    pwn_college{1337}
    yans@asdf ~ $ █
    ```

    Một liên kết cứng là một tham chiếu "hợp lệ" (valid) đến tệp gốc ngang bằng với chính bản thân tệp gốc đó. Nó là một tệp tình cờ được hỗ trợ (backed by) bởi cùng một dữ liệu giống hệt như tệp gốc.

</details>

<details>
 <summary><code>🏴linking files(Liên kết các tệp)</code></summary>

* Nếu bạn sử dụng Linux (hoặc máy tính) trong một thời gian đủ dài để làm việc thực sự, cuối cùng bạn sẽ gặp phải một số biến thể của tình huống sau: bạn muốn hai chương trình truy cập cùng một dữ liệu, nhưng các chương trình đó lại mong đợi dữ liệu nằm ở hai vị trí khác nhau. May mắn thay, Linux cung cấp một giải pháp cho vấn đề này: các liên kết .

* Các liên kết có hai loại: liên kết cứng và liên kết mềm (còn được gọi là liên kết tượng trưng ). Chúng ta sẽ phân biệt hai loại này bằng một ví dụ tương tự:

* Liên kết cứng là khi bạn sử dụng nhiều địa chỉ khác nhau để chỉ căn hộ của mình, tất cả đều dẫn trực tiếp đến cùng một địa điểm (ví dụ: Apt 2so với Unit 2).
* " Liên kết mềm" là khi bạn chuyển nhà và yêu cầu dịch vụ bưu chính tự động chuyển tiếp thư từ nơi ở cũ đến nơi ở mới.
* Trong hệ thống tập tin, về mặt khái niệm, một tập tin là một địa chỉ chứa nội dung của tập tin đó. Liên kết cứng là một địa chỉ thay thế dùng để lập chỉ mục dữ liệu đó — việc truy cập vào liên kết cứng và truy cập vào tập tin gốc hoàn toàn giống nhau, ở chỗ chúng ngay lập tức cung cấp dữ liệu cần thiết. Ngược lại, liên kết mềm/liên kết tượng trưng chứa tên tập tin gốc. Khi bạn truy cập vào liên kết tượng trưng, ​​Linux sẽ nhận ra đó là một liên kết tượng trưng, ​​đọc tên tập tin gốc, và sau đó (thường) tự động truy cập vào tập tin đó. Trong hầu hết các trường hợp, cả hai tình huống đều dẫn đến việc truy cập dữ liệu gốc, nhưng cơ chế thì khác nhau.

* Liên kết cứng nghe có vẻ đơn giản hơn với hầu hết mọi người (ví dụ điển hình, tôi đã giải thích nó chỉ trong một câu ở trên, so với hai câu cho liên kết mềm), nhưng chúng có nhiều nhược điểm và những vấn đề khó khăn khi triển khai, khiến cho liên kết mềm/liên kết tượng trưng trở thành lựa chọn thay thế phổ biến hơn nhiều.

* Trong thử thách này, chúng ta sẽ tìm hiểu về liên kết tượng trưng (còn được gọi là symlink ). Liên kết tượng trưng được tạo bằng ln lệnh với -s đối số, như sau:
```sh
hacker@dojo:~$ cat /tmp/myfile
This is my file!
hacker@dojo:~$ ln -s /tmp/myfile /home/hacker/ourfile
hacker@dojo:~$ cat ~/ourfile
This is my file!
hacker@dojo:~$
```
* Bạn có thể thấy rằng việc truy cập vào liên kết tượng trưng sẽ trả về nội dung của tệp gốc! Ngoài ra, bạn cũng có thể thấy cách sử dụng dấu chấm ( ln -s.). Lưu ý rằng đường dẫn tệp gốc đứng trước đường dẫn liên kết trong lệnh!

* Có thể nhận dạng liên kết tượng trưng bằng một vài phương pháp. Ví dụ, filelệnh này, nhận tên tệp và cho biết loại tệp đó là gì, sẽ nhận ra các liên kết tượng trưng:
```sh
hacker@dojo:~$ file /tmp/myfile
/tmp/myfile: ASCII text
hacker@dojo:~$ file ~/ourfile
/home/hacker/ourfile: symbolic link to /tmp/myfile
hacker@dojo:~$
```
* Được rồi, giờ đến lượt bạn thử! Ở cấp độ này, lá cờ như thường lệ nằm ở /flag, nhưng /challenge/catflag thay vào đó sẽ hiển thị /home/hacker/not-the-flag. Hãy sử dụng liên kết tượng trưng và đánh lừa nó để lấy được lá cờ!
* <img width="805" height="288" alt="image" src="https://github.com/user-attachments/assets/653084f8-2276-4d23-a943-04badef2d3d7" />

</details>
