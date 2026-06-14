# Practicing Piping

* Có thể bạn đã nhận thấy rằng một số lệnh xuất dữ liệu ra thiết bị đầu cuối khi bạn chạy chúng. Cho đến nay, điều này đã in ra cho bạn nhiều cờ (flags), nhưng giống như nhiều thứ khác, công nghệ còn sâu sắc hơn thế. Các cơ chế đằng sau việc xử lý đầu vào và đầu ra trên dòng lệnh góp phần tạo nên sức mạnh của dòng lệnh.

* Module này sẽ dạy bạn về chuyển hướng đầu vào và đầu ra . Nói một cách đơn giản, mọi tiến trình trong Linux đều có ba kênh giao tiếp tiêu chuẩn ban đầu:

* Đầu vào chuẩn là kênh mà qua đó tiến trình nhận đầu vào. Ví dụ, trình thông dịch lệnh (shell) của bạn sử dụng đầu vào chuẩn để đọc các lệnh mà bạn nhập vào.
Đầu ra chuẩn là kênh mà qua đó các tiến trình xuất ra dữ liệu thông thường, chẳng hạn như cờ khi nó được in ra cho bạn trong các thử thách trước hoặc đầu ra của các tiện ích như ls.
Lỗi chuẩn (Standard Error ) là kênh mà qua đó các tiến trình xuất ra thông tin chi tiết về lỗi. Ví dụ, nếu bạn gõ sai một lệnh, shell sẽ xuất ra, thông qua lỗi chuẩn, rằng lệnh này không tồn tại.
Vì ba kênh này được sử dụng rất thường xuyên trong Linux, chúng được biết đến với các tên viết tắt: stdin, stdout, stderr. Mô-đun này sẽ hướng dẫn bạn cách chuyển hướng, kết nối chuỗi, chặn và can thiệp vào các kênh này. Chúc may mắn!

<details>
  <summary><code>🏴Redirecting output(Chuyển hướng đầu ra)</code></summary>

 * Trước tiên, hãy xem xét việc chuyển hướng đầu ra chuẩn (stdout) sang tệp. Bạn có thể thực hiện điều này bằng >ký tự như sau:
```sh
hacker@dojo:~$ echo hi > asdf
```
* Thao tác này sẽ chuyển hướng đầu ra của echo hi(sẽ là hi) đến tệp asdf. Sau đó, bạn có thể sử dụng một chương trình như catđể xuất tệp này:
```sh
hacker@dojo:~$ cat asdf
hi
```
* Trong thử thách này, bạn phải sử dụng phương pháp chuyển hướng đầu ra này để ghi từ PWN(viết hoa toàn bộ) vào tên tệp COLLEGE(viết hoa toàn bộ).
* <img width="416" height="86" alt="image" src="https://github.com/user-attachments/assets/faaa0e29-d18c-44e8-b056-61595dc1647d" />

</details>

<details>
  
  <summary><code>🏴Redirecting  more output(Chuyển hướng thêm đầu ra)</code></summary>

* Ngoài việc chuyển hướng đầu ra của lệnh echo, tất nhiên bạn cũng có thể chuyển hướng đầu ra của bất kỳ lệnh nào khác. Ở cấp độ này, lệnh /challenge/runsẽ một lần nữa cung cấp cho bạn một cờ, nhưng chỉ khi bạn chuyển hướng đầu ra của nó đến tệp myflag. Cờ của bạn, tất nhiên, sẽ được lưu trong myflagtệp đó!

* Bạn sẽ nhận thấy rằng nó /challenge/runvẫn sẽ in ra thiết bị đầu cuối của bạn một cách bình thường, mặc dù bạn đã chuyển hướng stdout. Đó là bởi vì nó truyền đạt các hướng dẫn và phản hồi của nó qua lỗi chuẩn, và chỉ in cờ qua đầu ra chuẩn!

* <img width="525" height="239" alt="image" src="https://github.com/user-attachments/assets/f0d62070-bf1d-491f-9d6c-e137e0c0bbaf" />

</details>

<details>
  <summary><code>🏴Appending output(Thêm đầu ra)</code></summary>

  * Một trường hợp sử dụng phổ biến của việc chuyển hướng đầu ra là lưu lại một số kết quả lệnh để phân tích sau này. Thông thường, bạn muốn thực hiện việc này một cách tổng hợp : chạy một loạt lệnh, lưu lại kết quả đầu ra của chúng và grepxử lý sau. Trong trường hợp này, bạn có thể muốn tất cả đầu ra đó tiếp tục được ghi thêm vào cùng một tệp, nhưng >sẽ tạo một tệp đầu ra mới mỗi lần, xóa nội dung cũ.

Bạn có thể chuyển hướng đầu vào ở chế độ thêm>> bằng cách sử dụng thay vì >, như sau:
```sh
hacker@dojo:~$ echo pwn > outfile
hacker@dojo:~$ echo college >> outfile
hacker@dojo:~$ cat outfile
pwn
college
hacker@dojo:$
```
* Để thực hành, hãy chạy /challenge/runvới chế độ chuyển hướng thêm (append-mode) đầu ra vào tệp /home/hacker/the-flag. Thao tác này sẽ ghi nửa đầu của cờ vào tệp, và nửa sau vào stdoutnếu stdoutđược chuyển hướng đến tệp. Nếu bạn chuyển hướng đúng cách ở chế độ thêm, nửa sau sẽ được nối vào nửa đầu, nhưng nếu bạn chuyển hướng ở chế độ cắt bớt (truncation mode >), nửa sau sẽ ghi đè lên nửa đầu và bạn sẽ không nhận được cờ!

   Hãy làm ngay đi!

  * <img width="687" height="287" alt="image" src="https://github.com/user-attachments/assets/870afd10-fd21-4f77-9aa1-773d1effb1ea" />
  * <img width="465" height="172" alt="image" src="https://github.com/user-attachments/assets/c065ff13-20ee-47c0-82c9-6432579df709" />


</details>

<details>
  <summary><code>🏴Redirecting errors(lỗi chuyển hướng)</code></summary>

  * Giống như đầu ra chuẩn, bạn cũng có thể chuyển hướng kênh lỗi của các lệnh. Ở đây, chúng ta sẽ tìm hiểu về số hiệu mô tả tệp (File Descriptor numbers ). Mô tả tệp (FD) là một số mô tả kênh giao tiếp trong Linux. Bạn đã sử dụng chúng rồi, ngay cả khi bạn không nhận ra điều đó. Chúng ta đã quen thuộc với ba loại:

  FD 0: Đầu vào chuẩn
  FD 1: Đầu ra chuẩn
  FD 2: Sai số chuẩn
* Khi bạn chuyển hướng giao tiếp tiến trình, bạn thực hiện điều đó bằng số FD, mặc dù một số số FD được ngầm định. Ví dụ, lệnh `a` >không có số ngụ ý `a` 1>, lệnh này chuyển hướng FD 1 (Đầu ra Chuẩn). Do đó, hai lệnh sau đây là tương đương:
```sh
hacker@dojo:~$ echo hi > asdf
hacker@dojo:~$ echo hi 1> asdf
```
Việc chuyển hướng lỗi khá dễ dàng từ đây. Nếu bạn có một lệnh có thể tạo ra dữ liệu thông qua lỗi chuẩn (chẳng hạn như /challenge/run), bạn có thể làm như sau:
```sh
hacker@dojo:~$ /challenge/run 2> errors.log
```
Thao tác này sẽ chuyển hướng lỗi chuẩn (FD 2) đến errors.logtệp. Hơn nữa, bạn có thể chuyển hướng nhiều mô tả tệp cùng một lúc! Ví dụ:
```sh 
hacker@dojo:~$ some_command > output.log 2> errors.log
```
Lệnh đó sẽ chuyển hướng đầu ra đến output.logvà lỗi đến errors.log.

Hãy cùng thực hành nào! Trong thử thách này, bạn cần chuyển hướng đầu ra của /challenge/run, như trước đây, sang myflag, và "lỗi" (trong trường hợp này là các hướng dẫn) sang instructions. Bạn sẽ nhận thấy rằng không có gì được in ra terminal, vì bạn đã chuyển hướng mọi thứ! Bạn có thể tìm thấy hướng dẫn/phản hồi trong instructionsvà cờ myflagtrong khi bạn thực hiện thành công!

* Khi ta đã chuyển hướng xong thì mở instructions sẽ ra các hướng dẫn, thông báo còn mở myflag thì ra cờ.
  * <img width="1186" height="523" alt="image" src="https://github.com/user-attachments/assets/ca4d7a94-eeb7-45f3-90bf-19654a3ea607" />
  * <img width="841" height="121" alt="image" src="https://github.com/user-attachments/assets/cee9ad0f-0d61-4ee9-b15f-07e0ebebcc8c" />


</details>

<details>
  <summary><code>🏴Redirevting input(Chuyển hướng đầu vào)</code></summary>

  * Tương tự như việc bạn có thể chuyển hướng đầu ra từ các chương trình, bạn cũng có thể chuyển hướng đầu vào đến các chương trình! Điều này được thực hiện bằng cách sử dụng <, như sau:
```sh
hacker@dojo:~$ echo yo > message
hacker@dojo:~$ cat message
yo
hacker@dojo:~$ rev < message
oy
```
* Bạn có thể làm được nhiều điều thú vị với các chương trình khác nhau bằng cách sử dụng chuyển hướng đầu vào! Ở cấp độ này, chúng ta sẽ thực hành sử dụng /challenge/run, điều này yêu cầu bạn chuyển hướng PWNtệp đến nó và tệp đó PWNchứa giá trị COLLEGE! Để ghi giá trị đó vào PWNtệp, hãy nhớ lại thử thách trước đó về chuyển hướng đầu ra từ echo!

  * <img width="460" height="116" alt="image" src="https://github.com/user-attachments/assets/03de1f4d-ebe3-4b07-9a44-d19048fda90c" />


</details>

<details>
  <summary><code>🏴Grepping stored results(Tìm kiếm kết quả lưu trữ)</code></summary>

  * Bạn đã biết cách chạy các lệnh, cách chuyển hướng đầu ra của chúng (ví dụ: >), và cách tìm kiếm trong tệp kết quả (ví dụ: grep). Hãy cùng kết hợp những điều này lại!

   1.Để chuẩn bị cho các cấp độ phức tạp hơn, chúng tôi muốn bạn:

   2.Chuyển hướng đầu ra của `/challenge/run` thành `/tmp/data.txt`.
Điều này sẽ tạo ra một trăm nghìn dòng văn bản, trong đó có một dòng là quốc kỳ, ở định dạng /tmp/data.txt.
   3.`grep`Vì lá cờ đó!
  * <img width="430" height="28" alt="image" src="https://github.com/user-attachments/assets/7d6abea3-4f4a-463f-8f00-a9c3b34f206e" />

</details>

<details>
  <summary><code>🏴Grepping live output(Tìm kiếm đầu ra trực tiếp)</code></summary>

  * Hóa ra bạn có thể "loại bỏ bước trung gian" và tránh việc phải lưu kết quả vào tệp, như bạn đã làm ở cấp độ trước. Bạn có thể làm điều này bằng cách sử dụng toán |tử (pipe). Đầu ra chuẩn từ lệnh bên trái dấu pipe sẽ được kết nối với ( được chuyển tiếp vào ) đầu vào chuẩn của lệnh bên phải dấu pipe. Ví dụ:
```sh
hacker@dojo:~$ echo no-no | grep yes
hacker@dojo:~$ echo yes-yes | grep yes
yes-yes
hacker@dojo:~$ echo yes-yes | grep no
hacker@dojo:~$ echo no-no | grep no
no-no
```
* Giờ hãy tự mình thử xem! /challenge/runNó sẽ xuất ra một trăm nghìn dòng văn bản, bao gồm cả cờ. (Phần cuối cùng greplà thông tin về cờ)

  * <img width="723" height="273" alt="image" src="https://github.com/user-attachments/assets/65378a51-2b6f-4b70-a661-d27142a0749d" />

</details>

<details>
  <summary><code>🏴Grepping errors(Lỗi Grepping)</code></summary>

  * Bạn biết cách chuyển hướng lỗi vào một tệp và bạn cũng biết cách chuyển đầu ra đến một chương trình khác, chẳng hạn như grep. Nhưng nếu bạn muốn greptruyền trực tiếp các lỗi thì sao?

* Toán tử này >chuyển hướng một bộ mô tả tệp nhất định đến một tệp, và bạn đã sử dụng nó 2>để chuyển hướng fd 2, tức là lỗi chuẩn. Toán tử này chỉ| chuyển hướng đầu ra chuẩn đến một chương trình khác, và không có dạng nào của toán tử này! Nó chỉ có thể chuyển hướng đầu ra chuẩn (bộ mô tả tệp 1).2|

 May mắn thay, ở đâu có vỏ sò, ở đó có cách!

* Shell có một >&toán tử, dùng để chuyển hướng một mô tả tệp đến một mô tả tệp khác . Điều này có nghĩa là chúng ta có thể thực hiện quy trình hai bước để grepxử lý lỗi: đầu tiên, chúng ta chuyển hướng lỗi chuẩn đến đầu ra chuẩn ( 2>& 1) và sau đó chuyển hướng stderr và stdout đã được kết hợp như bình thường ( |)!

* Hãy thử ngay! Giống như màn chơi trước, màn chơi này sẽ làm bạn choáng ngợp với lượng dữ liệu đầu ra, nhưng lần này là về sai số chuẩn. grepHãy vượt qua nó để tìm ra lá cờ!

  * <img width="721" height="288" alt="image" src="https://github.com/user-attachments/assets/afd224e6-e368-48de-99b4-4d7e938c7a69" />

</details>

<details>
  <summary><code>🏴Filtering wiht grep -v(Lọc dữ liệu bằng lệnh `grep-v`)</code></summary>

  * Lệnh này grepcó một tùy chọn rất hữu ích: -v(đảo ngược kết quả khớp). Trong khi chế độ bình thường grephiển thị các dòng KHỚP với một mẫu, grep -vchế độ này hiển thị các dòng KHÔNG khớp với mẫu:
```sh
hacker@dojo:~$ cat data.txt
hello hackers!
hello world!
hacker@dojo:~$ cat data.txt | grep -v world
hello hackers!
hacker@dojo:~$
```
* Đôi khi, cách duy nhất để lọc chỉ dữ liệu bạn muốn là lọc bỏ dữ liệu bạn không muốn. Trong thử thách này, chương /challenge/runtrình sẽ xuất cờ ra stdout, nhưng nó cũng sẽ xuất ra hơn 1000 cờ giả (có chứa từ khóa DECOYnào đó trong cờ) lẫn với cờ thật. Bạn cần lọc bỏ các cờ giả trong khi vẫn giữ lại cờ thật!

* Sử dụng công cụ này grep -vđể lọc bỏ tất cả các dòng chứa từ "DECOY" và hiển thị lá cờ thật!

  * <img width="416" height="31" alt="image" src="https://github.com/user-attachments/assets/5c00be5e-1901-4ab5-ba24-416c6020ca3d" />

</details>

<details>
  <summary><code>🏴Filtering with sed(Lọc dữ liệu bằng lệnh sed)</code></summary>

  * `grep` Không phải chỉ có cách này mới dùng để so khớp mẫu. Đôi khi dữ liệu thật và dữ liệu rác được trộn lẫn trong cùng một dòng, và chúng ta muốn lọc bỏ dữ liệu rác. Để làm điều đó, chúng ta có `sed`. `sed`cung cấp một cách dễ dàng để thay thế các mẫu trong văn bản bằng một từ khác. Cú pháp để so khớp và thay thế rất đơn giản:
```sh
sed "s/oldword/newword/g"
```
`s/`- thay thế
`oldword`- từ cần thay thế
`newword`- sự thay thế cho oldword
`/g`- toàn cầu (tìm kiếm tất cả các lần xuất hiện của mẫu)

Trong thử thách này, `/challenge/run`hệ thống sẽ in ra lá cờ, nhưng giữa mỗi ký tự sẽ có chuỗi "FAKEFLAG". Nhiệm vụ của bạn là lọc bỏ dữ liệu rác khỏi lá cờ. Chúc may mắn!

  * <img width="635" height="232" alt="image" src="https://github.com/user-attachments/assets/4396637b-cd34-46cd-b4cf-14e016ed0e22" />

</details>

<details>
  <summary><code>🏴Duplicating piped data with tee(Sao chép dữ liệu được truyền qua đường ống bằng tee) </code></summary>

  * Khi bạn truyền dữ liệu từ lệnh này sang lệnh khác, tất nhiên bạn sẽ không còn thấy dữ liệu đó trên màn hình nữa. Điều này không phải lúc nào cũng mong muốn: ví dụ, bạn có thể muốn xem dữ liệu khi nó được truyền giữa các lệnh để gỡ lỗi các kết quả không mong muốn (ví dụ: "tại sao lệnh thứ hai lại không hoạt động???").

* May mắn thay, có một giải pháp! teeLệnh này, được đặt tên theo "bộ chia chữ T" trong đường ống nước , sao chép dữ liệu chảy qua các đường ống của bạn vào bất kỳ số lượng tệp nào được cung cấp trên dòng lệnh. Ví dụ:
```sh
hacker@dojo:~$ echo hi | tee pwn college
hi
hacker@dojo:~$ cat pwn
hi
hacker@dojo:~$ cat college
hi
hacker@dojo:~$
```
* Như bạn thấy, bằng cách cung cấp hai tệp cho hàm tee, chúng ta đã có được ba bản sao của dữ liệu được truyền vào: một bản đến stdout, một bản đến pwntệp và một bản đến collegetệp. Bạn có thể hình dung cách bạn có thể sử dụng điều này để gỡ lỗi những sự cố xảy ra:
```sh
hacker@dojo:~$ command_1 | command_2
Command 2 failed!
hacker@dojo:~$ command_1 | tee cmd1_output | command_2
Command 2 failed!
hacker@dojo:~$ cat cmd1_output
Command 1 failed: must pass --succeed!
hacker@dojo:~$ command_1 --succeed | command_2
Commands succeeded!
```
* Giờ đến lượt bạn thử! Quá trình này /challenge/pwnphải được chuyển tiếp vào /challenge/college, nhưng bạn cần chặn dữ liệu để xem pwncần gì từ bạn!

  * <img width="572" height="112" alt="image" src="https://github.com/user-attachments/assets/bc4f5d2d-71f6-459c-8656-ff50e8b1bafb" />
* <img width="673" height="79" alt="image" src="https://github.com/user-attachments/assets/82136bda-3dc9-4954-bc8b-73b44f2ff43f" />

</details>

<details>
  <summary><code>🏴Process substitution for input(Thay thế quy trình cho đầu vào) </code></summary>

  * Đôi khi bạn cần so sánh kết quả của hai lệnh thay vì hai tệp. Bạn có thể nghĩ đến việc lưu mỗi kết quả vào một tệp trước:
```sh
hacker@dojo:~$ command1 > file1
hacker@dojo:~$ command2 > file2
hacker@dojo:~$ diff file1 file2
```
* Nhưng có một cách thanh lịch hơn! Linux tuân theo triết lý `"mọi thứ đều là một tập tin"` . Nghĩa là, hệ thống cố gắng cung cấp quyền truy cập giống như tập tin cho hầu hết các tài nguyên, bao gồm cả đầu vào và đầu ra của các chương trình đang chạy! Shell cũng tuân theo triết lý này, cho phép bạn, ví dụ, sử dụng bất kỳ tiện ích nào nhận đối số tập tin trên dòng lệnh và kết nối nó với đầu ra của các chương trình, như bạn đã học ở các cấp độ trước.

* Điều thú vị là, chúng ta có thể tiến xa hơn nữa và kết nối đầu vào và đầu ra của chương trình với các đối số của lệnh. Điều này được thực hiện bằng cách sử dụng `Thay thế Tiến trình` . Để đọc từ một lệnh (thay thế tiến trình đầu vào), hãy sử dụng  `<(command)`. Khi bạn viết `<(command)`, bash sẽ chạy lệnh và kết nối đầu ra của nó với một tệp tạm thời mà nó sẽ tạo ra. Tất nhiên, đây không phải là một tệp thực sự , mà là cái được gọi là đường ống có tên , vì nó có tên tệp:
```SH
hacker@dojo:~$ echo <(echo hi)
/dev/fd/63
hacker@dojo:~$
```
* Câu hỏi "Where did `/dev/fd/63`come from?" `bash`được thay thế `<(echo hi)`bằng đường dẫn của tệp ống dẫn được đặt tên được kết nối với đầu ra của lệnh! Trong khi lệnh đang chạy, việc đọc từ tệp này sẽ đọc dữ liệu từ đầu ra chuẩn của lệnh. Thông thường, điều này được thực hiện bằng cách sử dụng các lệnh nhận tệp đầu vào làm đối số:
```SH
hacker@dojo:~$ cat <(echo hi)
hi
hacker@dojo:~$
```
* Dĩ nhiên, bạn có thể chỉ định điều này nhiều lần:
```SH
hacker@dojo:~$ echo <(echo pwn) <(echo college)
/dev/fd/63 /dev/fd/64
hacker@dojo:~$ cat <(echo pwn) <(echo college)
pwn
college
hacker@dojo:~$
```
* Giờ đến phần thử thách! Hãy nhớ lại những gì bạn đã học trong `diff`thử thách `" Hiểu các lệnh"` . Trong thử thách đó, bạn đã so sánh hai tập tin. Bây giờ, bạn sẽ so sánh hai tập hợp kết quả đầu ra của lệnh: `/challenge/print_decoys`, lệnh này sẽ in ra một loạt các cờ giả, và `/challenge/print_decoys_and_flag`lệnh này sẽ in ra những cờ giả đó cộng với cờ thật.

Hãy sử dụng phương pháp thay thế tiến trình `diff` để so sánh kết quả đầu ra của hai chương trình này và tìm ra cờ của bạn!

  * <img width="670" height="40" alt="image" src="https://github.com/user-attachments/assets/d83b61e8-f02d-4c0b-9196-fe3d5d31b1eb" />

</details>

<details>
  <summary><code>🏴Writing to multiple programs(Viết cho nhiều chương trình)</code></summary>
* Giờ bạn đã biết rằng thay thế tiến trình có thể làm cho đầu ra lệnh xuất hiện dưới dạng tệp để đọc bằng `<(command)`. Nhưng bạn cũng có thể sử dụng thay thế tiến trình để ghi vào các lệnh!

Bạn có thể sao chép dữ liệu sang hai tập tin bằng lệnh `tee`:
```sh
hacker@dojo:~$ echo HACK | tee THE > PLANET
hacker@dojo:~$ cat THE
HACK
hacker@dojo:~$ cat PLANET
HACK
hacker@dojo:~$
```
Và bạn đã từng `tee`sao chép dữ liệu vào một tệp và một lệnh:
```sh
hacker@dojo:~$ echo HACK | tee THE | cat
HACK
hacker@dojo:~$ cat THE
HACK
hacker@dojo:~$
```
* Nhưng nếu phải sao chép thành hai lệnh thì sao? Như `tee`đã nêu trong trang hướng dẫn sử dụng, lệnh này được thiết kế để ghi vào tập tin và xuất ra đầu ra chuẩn:
```sh
TEE(1)                           User Commands                          TEE(1)

NAME
       tee - read from standard input and write to standard output and f
```
  * Nhưng khoan đã! Bạn vừa học được rằng bash có thể làm cho các lệnh trông giống như các tập tin bằng cách sử dụng thay thế tiến trình! Để ghi vào một lệnh (thay thế tiến trình đầu ra), hãy sử dụng `>(command)`. Nếu bạn ghi một đối số của `>(rev)`, bash sẽ chạy `rev`lệnh (lệnh này đọc dữ liệu từ đầu vào chuẩn, đảo ngược thứ tự và ghi nó vào đầu ra chuẩn!), nhưng kết nối đầu vào của nó với một tập tin đường ống tạm thời được đặt tên. Khi các lệnh ghi vào tập tin này, dữ liệu sẽ được chuyển đến đầu vào chuẩn của lệnh:
```sh
hacker@dojo:~$ echo HACK | rev
KCAH
hacker@dojo:~$ echo HACK | tee >(rev)
HACK
KCAH
```
Trên đây, chuỗi sự kiện sau đã diễn ra:

1.`bash`Khởi chạy `rev`lệnh, kết nối một đường ống có tên (có lẽ là `/dev/fd/63`) với `rev`đầu vào chuẩn của .
2.`bash`Khởi động `tee`lệnh, nối một đường ống vào đầu vào chuẩn của nó và thay thế đối số đầu tiên `tee`ằng `/dev/fd/63. tee`Thậm chí nó còn không nhìn thấy đối số `>(rev)`; trình shell đã thay thế nó trước khi khởi chạy.`tee`
3.`bash`đã sử dụng hàm `echo`tích hợp để in `HACK`vào `tee`đầu vào chuẩn của 's.
4,`tee`Đọc dữ liệu `HACK`, ghi nó vào đầu ra chuẩn, rồi ghi tiếp vào `/dev/fd/63`(được kết nối với `rev`stdin của )
5.`rev`Đọc dữ liệu HACKtừ đầu vào chuẩn, đảo ngược giá trị và ghi `KCAH`vào đầu ra chuẩn.
Giờ đến lượt bạn! Trong thử thách này, chúng ta có `/challenge/hack`, `/challenge/the`, và `/challenge/planet`. Hãy chạy /challenge/hacklệnh và sao chép đầu ra của nó làm đầu vào cho cả hai lệnh /challenge/thevà /challenge/planet! Hãy xem lại các thử thách trước đó "Sao chép dữ liệu được truyền qua đường ống bằng tee" và "Thay thế quy trình cho đầu vào" nếu bạn cần ôn lại phương pháp này.

Câu hỏi đố vui!

Người học tinh ý sẽ nhận ra rằng những điều sau đây là tương đương:
```sh
hacker@dojo:~$ echo hi | rev
ih
hacker@dojo:~$ echo hi > >(rev)
ih
hacker@dojo:~$
```
Có nhiều hơn một cách để truyền dữ liệu! Tất nhiên, cách thứ hai khó đọc hơn nhiều và cũng khó mở rộng hơn. Ví dụ:
```sh
hacker@dojo:~$ echo hi | rev | rev
hi
hacker@dojo:~$ echo hi > >(rev | rev)
hi
hacker@dojo:~$
```
* Thật là ngớ ngẩn! Bài học ở đây là, mặc dù thay thế quy trình là một công cụ mạnh mẽ trong bộ công cụ của bạn, nhưng nó là một công cụ rất chuyên biệt ; đừng sử dụng nó cho mọi thứ!

  *<img width="602" height="52" alt="image" src="https://github.com/user-attachments/assets/88da43d5-1176-47e3-9666-3833a2441651" />

</details>

<details>
  <summary><code>🏴Split-piping stderr and stdout<(Chia đường dẫn stderr và stdout)/code></summary>

  * Giờ hãy cùng tổng hợp kiến ​​thức của bạn. Bạn phải thành thạo thao tác chuyển hướng đầu ra (piping) quan trọng nhất: chuyển hướng đầu ra chuẩn (stdout) đến một chương trình và đầu ra lỗi chuẩn (stderr) đến một chương trình khác.

 * Thách thức ở đây, dĩ nhiên, là `|`toán tử liên kết đầu ra chuẩn (stdout) của lệnh bên trái với đầu vào chuẩn (stdin) của lệnh bên phải. Tất nhiên, bạn đã từng `2>&1`chuyển hướng lỗi chuẩn (stderr) vào đầu ra chuẩn và do đó, truyền lỗi chuẩn qua đường ống, nhưng điều này lại làm trộn lẫn lỗi chuẩn và đầu ra chuẩn. Làm thế nào để giữ cho chúng không bị trộn lẫn?

* Bạn cần kết hợp kiến ​​thức của mình về` >()`, `2>`, và` |`. Cách thực hiện như thế nào là một nhiệm vụ tôi sẽ để bạn tự quyết định.

Trong thử thách này, bạn có:

1.`/challenge/hack`Thao tác này tạo ra dữ liệu trên stdout và stderr.
2.`/challenge/the`Bạn phải chuyển hướng stderr`hack` của chương trình này .
3.`/challenge/planet`Bạn phải chuyển hướng đầu ra chuẩn`hack` của chương trình này .
Đi lấy lá cờ đi!

THÊM ĐIỂM THƯỞNG: Để tăng độ khó, hãy tìm một giải pháp không sử dụng dấu chấm `|`.

    * <img width="607" height="53" alt="image" src="https://github.com/user-attachments/assets/22a2644b-022e-4338-8cc7-3028c6dc1172" />

</details>

<details>
  <summary><code>🏴Named pipes(Ống dẫn được đặt tên)</code></summary>
</details>
