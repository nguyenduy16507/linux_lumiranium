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
<commary><code>🏴listing files(liệt kê các tệp)</code></commary>
  
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
  
</details>
