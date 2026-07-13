# Shell Variables
Giao diện dòng lệnh Linux thực chất là một ngôn ngữ lập trình phức tạp mà bạn có thể dùng để viết các chương 
trình thực sự! Vì giao diện dòng lệnh thường được gọi là "shell", nên các chương trình được viết bằng ngôn ngữ 
này được gọi là "shell script". Khi sử dụng dòng lệnh, về cơ bản bạn đang viết một shell script từng dòng một!

Giống như hầu hết các ngôn ngữ lập trình, shell hỗ trợ biến. Mô-đun này sẽ giúp bạn làm quen với việc thiết \
lập, in và sử dụng các biến này!
<details>
  <summary><code>🏴Printing Variables(In các biến) </code></summary>

  * Chúng ta hãy bắt đầu bằng việc in các biến ra. /challenge/runChương trình sẽ không, và không thể, cung cấp cho bạn cờ (flag), nhưng không sao, vì cờ đã được lưu vào biến có tên là "FLAG"! Chỉ cần yêu cầu trình thông dịch lệnh (shell) in nó ra!

Bạn có thể thực hiện việc này bằng nhiều cách, nhưng chúng ta sẽ bắt đầu với lệnh này echo. Lệnh này chỉ đơn giản là in ra thông tin. Ví dụ:

hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
Bạn cũng có thể in ra các biến echobằng cách thêm dấu chấm vào trước tên biến $. Ví dụ, có một biến, PWD, luôn chứa thư mục làm việc hiện tại của shell hiện tại. Bạn in nó ra như sau:

hacker@dojo:~$ echo $PWD
/home/hacker
Giờ đến lượt bạn. Hãy yêu cầu trình thông dịch lệnh in ra FLAGbiến và giải bài toán này!


</details>
<details>
  <summary><code>🏴Setting Variables(Thiết lập biến)</code></summary>
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
