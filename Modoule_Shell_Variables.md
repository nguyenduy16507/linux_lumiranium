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

*  Ở cấp độ này, bạn sẽ học về cách trích dẫn. Khoảng trắng có ý nghĩa đặc biệt trong shell, và có những chỗ bạn không thể sử dụng chúng một cách tùy tiện. Hãy nhớ lại thiết lập biến của chúng ta:
```sh
hacker@dojo:~$ VAR=1337
```
* Thao tác đó sẽ gán VARgiá trị cho biến 1337, nhưng nếu bạn muốn gán giá trị cho biến khác thì sao 1337 SAUCE? Bạn có thể thử cách sau:
```sh
hacker@dojo:~$ VAR=1337 SAUCE
```
* Điều này nghe có vẻ hợp lý, nhưng nó không hoạt động, vì những lý do tương tự như việc cần phải không có khoảng trắng xung quanh dấu chấm =. Khi shell thấy một khoảng trắng, nó sẽ kết thúc việc gán biến và hiểu từ tiếp theo ( SAUCEtrong trường hợp này là ) là một lệnh. Để đặt VARthành 1337 SAUCE, bạn cần đặt nó trong dấu ngoặc kép :
```sh
hacker@dojo:~$ VAR="1337 SAUCE"
```
* Ở đây, trình thông dịch lệnh đọc 1337 SAUCEmột mã thông báo duy nhất và vui vẻ gán giá trị đó thành VAR. Ở cấp độ này, bạn cần gán biến PWNthành COLLEGE YEAH. Chúc may mắn!
* <img width="393" height="41" alt="image" src="https://github.com/user-attachments/assets/fc496871-b29e-4402-b3c1-1a7d840108e9" />

</details>
<details>
  <summary><code>🏴Exporting Variables(Xuất biến)</code></summary>

* Theo mặc định, các biến mà bạn thiết lập trong một phiên shell chỉ có hiệu lực cục bộ trong tiến trình shell đó. Điều này có nghĩa là các lệnh khác mà bạn chạy sẽ không kế thừa chúng. Bạn có thể thử nghiệm điều này bằng cách đơn giản là gọi một tiến trình shell khác trong shell của chính bạn, như sau:
```sh
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ echo "VAR is: $VAR"
VAR is: 1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is:
```
* Trong kết quả hiển thị ở trên, $dấu nhắc là dấu nhắc của sh, một triển khai shell tối thiểu được gọi như một tiến trình con của tiến trình shell chính. Và nó không nhận `VAR` biến!

Điều này hoàn toàn hợp lý. Các biến shell của bạn có thể chứa dữ liệu nhạy cảm hoặc kỳ lạ, và bạn không muốn chúng bị rò rỉ sang các chương trình khác mà bạn chạy trừ khi được phép. Làm thế nào để đánh dấu điều đó? Bạn xuất các biến của mình. Khi bạn xuất các biến, chúng được truyền vào các biến môi trường của các tiến trình con. Bạn sẽ gặp khái niệm biến môi trường trong các bài tập khác, nhưng bạn sẽ quan sát tác dụng của chúng ở đây. Đây là một ví dụ:
```sh
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ export VAR
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```
* Ở đây, tiến trình con đã nhận được giá trị của VAR và có thể in ra! Bạn cũng có thể kết hợp hai dòng đầu tiên đó.
```sh
hacker@dojo:~$ export VAR=1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```
* Trong thử thách này, bạn phải gọi hàm /challenge/runvới PWNbiến được xuất và gán giá trị COLLEGE, và một COLLEGEbiến khác được gán giá trị PWNnhưng không được xuất (ví dụ: không được kế thừa bởi /challenge/run). Chúc may mắn!
* <img width="416" height="222" alt="image" src="https://github.com/user-attachments/assets/47bab68a-951e-4e56-bd14-6339fc6178fb" />
->Nhờ export giúp cho phép chương trình /challenge/run được kế thừa biến PWN=COLLEGE mà ko phải là COLLEGE=PWN 
* export + biến : Cho phép chương trình kế thừa biến đó
* export biến = A : Vừa tạo biến vừa cho phép chương trình con kế thừa biến đó 
</details>
<details>
  <summary><code>🏴</code>Printing Exported Variables(In các biến đã xuất)</summary>

 * Có nhiều cách để truy cập các biến trong bash. echochỉ là một trong số đó, và chúng ta sẽ học thêm ít nhất một cách nữa trong thử thách này.

* Hãy thử `env` lệnh này: nó sẽ in ra tất cả các biến được xuất trong shell của bạn, và bạn có thể xem qua kết quả đó để tìm `FLAG`biến!
* Chỉ cần dùng lệnh `env` sẽ in ra các biến được xuất trong shell 
</details>
<details>
  <summary><code>🏴Storing Command Output(Lưu trữ kết quả đầu ra của lệnh)</code></summary>

* Trong quá trình làm việc với shell, bạn thường muốn lưu trữ kết quả của một số lệnh vào một biến. May mắn thay, shell giúp việc này trở nên khá dễ dàng bằng cách sử dụng một thứ gọi là Thay thế lệnh ! Hãy xem:
```sh
hacker@dojo:~$ FLAG=$(cat /flag)
hacker@dojo:~$ echo "$FLAG"
pwn.college{blahblahblah}
hacker@dojo:~$
```
* Tuyệt vời! Giờ thì bạn hãy thực hành. Đọc trực tiếp kết quả của /challenge/runlệnh vào một biến có tên là PWN, và biến đó sẽ chứa cờ!

* Thông tin thú vị: Bạn cũng có thể sử dụng dấu ngoặc kép ngược thay vì dấu hai chấm ( $():) trong ví dụ trên. Đây là định dạng cũ hơn và có một số nhược điểm (ví dụ, hãy tưởng tượng nếu bạn muốn lồng các phép thay thế lệnh. Bạn sẽ làm thế nào với dấu ngoặc kép ngược? Quan điểm chính thức của pwn.college là bạn nên sử dụng thay vì ) .FLAG=`cat /flag`FLAG=$(cat /flag)$(cat $(find / -name flag))$(blah)`blah`
* <img width="435" height="79" alt="image" src="https://github.com/user-attachments/assets/03bf0fde-0f77-46d3-bf06-97b0b2a39e15" />

</details>
<details>
  <summary><code>🏴Reading Input(Đọc dữ liệu đầu vào)</code></summary>

 * Chúng ta sẽ bắt đầu bằng việc đọc dữ liệu nhập từ người dùng (bạn). Việc đó được thực hiện bằng cách sử dụng readhàm tích hợp có tên gọi rất phù hợp, hàm này sẽ đọc dữ liệu nhập vào một biến!

* Dưới đây là một ví dụ sử dụng -pđối số, cho phép bạn chỉ định lời nhắc (nếu không, bạn sẽ khó phân biệt đầu vào và đầu ra trong ví dụ bên dưới khi đọc bài này):
```sh
hacker@dojo:~$ read -p "INPUT: " MY_VARIABLE
INPUT: Hello!
hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
You entered: Hello!
```
* Hãy nhớ rằng, readnó đọc dữ liệu từ đầu vào chuẩn của bạn! Ví dụ đầu tiên Hello!ở trên là dữ liệu đầu vào chứ không phải đầu ra . Chúng ta hãy cố gắng làm rõ điều đó hơn. Ở đây, chúng ta đã chú thích ở đầu mỗi dòng để cho biết dòng đó đại diện cho dữ liệu INPUTtừ người dùng hay OUTPUTđến người dùng:
```sh
 INPUT: hacker@dojo:~$ echo $MY_VARIABLE
OUTPUT:
 INPUT: hacker@dojo:~$ read MY_VARIABLE
 INPUT: Hello!
 INPUT: hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
OUTPUT: You entered: Hello!
```
* Trong thử thách này, nhiệm vụ của bạn là sử dụng lệnh read để thiết lập PWN biến thành giá trị COLLEGE. Chúc may mắn!
* <img width="378" height="52" alt="image" src="https://github.com/user-attachments/assets/a5e398f3-281c-4fe3-bc95-f06790ff99dd" />

</details>
<details>
  <summary><code>🏴Reading Files(Đọc tệp)</code></summary>

 * Thông thường, khi người dùng shell muốn đọc một tệp vào một biến môi trường, họ sẽ làm điều gì đó tương tự như sau:
```sh
hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ VAR=$(cat some_file)
hacker@dojo:~$ echo $VAR
test
```
* Cách này có hiệu quả, nhưng nó thể hiện điều mà những hacker khó tính gọi là "Sử dụng Cat một cách vô ích" . Nghĩa là, chạy cả một chương trình khác chỉ để đọc tập tin là một sự lãng phí. Hóa ra bạn chỉ cần sử dụng sức mạnh của shell!

* Trước đây, bạn readđã nhập dữ liệu vào một biến. Bạn cũng đã từng chuyển hướng các tệp tin vào đầu vào lệnh! Kết hợp chúng lại, bạn có thể đọc các tệp tin bằng shell.
```sh
hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ read VAR < some_file
hacker@dojo:~$ echo $VAR
test
```
* Chuyện gì đã xảy ra ở đó? Ví dụ này chuyển hướng some_filevào đầu vào chuẩn của read, và vì vậy khi readđọc vào VAR, nó sẽ đọc từ tệp! Bây giờ, hãy sử dụng điều đó để đọc /challenge/read_mevào PWNbiến môi trường, và chúng tôi sẽ cung cấp cho bạn cờ! Cờ /challenge/read_mesẽ liên tục thay đổi, vì vậy bạn cần đọc nó trực tiếp vào PWNbiến bằng một lệnh duy nhất!
* <img width="379" height="42" alt="image" src="https://github.com/user-attachments/assets/d4462cae-03e9-4286-8a5c-626c8eee962a" />

</details>
