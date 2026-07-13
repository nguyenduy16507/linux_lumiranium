# Shell Variables
Giao diện dòng lệnh Linux thực chất là một ngôn ngữ lập trình phức tạp mà bạn có thể dùng để viết các chương 
trình thực sự! Vì giao diện dòng lệnh thường được gọi là "shell", nên các chương trình được viết bằng ngôn ngữ 
này được gọi là "shell script". Khi sử dụng dòng lệnh, về cơ bản bạn đang viết một shell script từng dòng một!

Giống như hầu hết các ngôn ngữ lập trình, shell hỗ trợ biến. Mô-đun này sẽ giúp bạn làm quen với việc thiết 
lập, in và sử dụng các biến này!

<details>
  <summary><code>📒Resources(Tài liệu)</code></summary>
* Dự án tìa liệu Linux có chứa 1 phần về cách biến shell https://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-5.html
  
</details>
<details>
  <summary><code>🏴Printing Variables(In các biến) </code></summary>

  * Chúng ta hãy bắt đầu bằng việc in các biến ra. /challenge/runChương trình sẽ không, và không thể, cung cấp cho bạn cờ (flag), nhưng không sao, vì cờ đã được lưu vào biến có tên là "FLAG"! Chỉ cần yêu cầu trình thông dịch lệnh (shell) in nó ra!

  * Bạn có thể thực hiện việc này bằng nhiều cách, nhưng chúng ta sẽ bắt đầu với lệnh này echo. Lệnh này chỉ đơn giản là in ra thông tin. Ví dụ:
```sh
hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
```
* Bạn cũng có thể in ra các biến echobằng cách thêm dấu chấm vào trước tên biến $. Ví dụ, có một biến, PWD, luôn chứa thư mục làm việc hiện tại của shell hiện tại. Bạn in nó ra như sau:
```sh
hacker@dojo:~$ echo $PWD
/home/hacker
```
* Giờ đến lượt bạn. Hãy yêu cầu trình thông dịch lệnh in ra FLAGbiến và giải bài toán này!

* <img width="345" height="27" alt="image" src="https://github.com/user-attachments/assets/4e7d405f-2084-43e2-b3b8-3386578d4865" />

</details>
<details>
  <summary><code>🏴Setting Variables(Thiết lập biến)</code></summary>

  Dĩ nhiên, ngoài việc đọc các giá trị được lưu trữ trong biến, bạn cũng có thể ghi giá trị vào biến. Điều này được thực hiện, giống như nhiều ngôn ngữ khác, bằng cách sử dụng ` =.`. Để gán VARgiá trị cho biến 1337, bạn sẽ sử dụng:
```sh
hacker@dojo:~$ VAR=1337
```
* Lưu ý rằng không có khoảng trắng xung quanh dấu =! Nếu bạn đặt khoảng trắng (ví dụ: VAR = 1337), trình thông dịch lệnh sẽ không nhận ra phép gán biến và thay vào đó sẽ cố gắng chạy VARlệnh (lệnh này không tồn tại).

* Cũng cần lưu ý rằng điều này sử dụng `<variable>` VARchứ không phải $VAR `<variable>`: `<variable>` $chỉ được thêm vào trước để truy cập các biến. Trong thuật ngữ shell, việc thêm `<variable>` này kích hoạt $cái gọi là mở rộng biến , và đáng ngạc nhiên là đây lại là nguồn gốc của nhiều lỗ hổng tiềm tàng (nếu bạn quan tâm đến điều đó, hãy xem Art of the Shell dojo khi bạn đã quen thuộc với dòng lệnh!).

* Sau khi thiết lập các biến, bạn có thể truy cập chúng bằng các kỹ thuật đã học trước đó, chẳng hạn như:
```sh
hacker@dojo:~$ echo $VAR
1337
```
* Để hoàn thành cấp độ này, bạn phải đặt PWNbiến thành giá trị COLLEGE. Hãy cẩn thận: cả tên và giá trị của biến đều phân biệt chữ hoa chữ thường! PWNkhông giống với pwnvà COLLEGEkhông giống với College.
* <img width="393" height="92" alt="image" src="https://github.com/user-attachments/assets/9de02fba-575e-47ba-8243-49e2206267ed" />


</details>
<details>
  <summary><code>🏴Multi-word Variables(Biến đa từ)</code></summary>
</details>
<details>
  <summary><code>🏴Exporting Variables(Xuất biến)</code></summary>
</details>
<details>
  <summary><code>🏴</code>Printing Exported Variables(In các biến đã xuất)</summary>
</details>
<details>
  <summary><code>🏴Storing Command Output(Lưu trữ kết quả đầu ra của lệnh)</code></summary>
</details>
<details>
  <summary><code>🏴Reading Input(Đọc dữ liệu đầu vào)</code></summary>
</details>
<details>
  <summary><code>🏴Reading Files(Đọc tệp)</code></summary>
</details>
