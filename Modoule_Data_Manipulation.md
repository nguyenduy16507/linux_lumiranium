# Data Manipulation(Thao tác dữ liệu)
* Bạn đã học cách truyền dữ liệu, chỉ định đầu vào, v.v. Giờ hãy bắt đầu kết hợp mọi thứ lại với nhau! Trong mô-đun này, bạn sẽ học một số lệnh để thao tác dữ liệu, giúp bạn đạt được kết quả tuyệt vời trên giao diện dòng lệnh.
<details>
  <summary><code>📒Further Programs to Learn(Các chương trình học tập nâng cao)</code></summary>

* * Có vô số chương trình mà các lập trình viên dòng lệnh sử dụng để thao tác dữ liệu. Mỗi chương trình thực hiện những việc cụ thể khác nhau, thường tuân theo `Unix Philosophy`(Triết lý Unix) là chỉ làm 1 việc và làm thật tốt. Bạn có thể kết hợp các chương trình này thành chuỗi logic phức hợp thực sự tuyệt vời. Một số ví dụ mà bạn nên tự hoc sau khi đã sẵn sàng sau khi hoàn thành khóa học Linux Luminarium, là:
*    -`awk` : để sử lý văn bản phức tạp
*    -`cut` : để trích xuất các phần tử của đường thẳng
*    -`less` : đối với trình đọc tập tin tương tác 
*    -`more` : đọc nhiều phần của tập tin cùng một lúc
*    -`paste` : để kết hợp các tệp
*    -`sed` : để thao tác các văn bản phức tạp
*    -`sort` : để sắp xếp dữ liệu
*    -`tail` : như 1 nghịch đảo của `head`
*    -`uniq` : để lọc dữ liệu ra duy nhất trong 1 luồng dữ liệu 
</details>
<details>
  <summary><code>🏴Translating characters(Dịch kí tự)</code></summary>

*  Một trong những mục đích của việc truyền dữ liệu qua đường ống là để sửa đổi dữ liệu. Nhiều lệnh Linux sẽ giúp bạn sửa đổi dữ liệu theo những cách rất thú vị. Một trong số đó là lệnh ` trand-print`, lệnh trnày sẽ xử lý các ký tự nhận được qua đầu vào chuẩn và in chúng ra đầu ra chuẩn.

* Ở cách sử dụng cơ bản nhất, trhàm này dịch ký tự được cung cấp trong đối số đầu tiên thành ký tự được cung cấp trong đối số thứ hai:
```sh
hacker@dojo:~$ echo OWN | tr O P
PWN
hacker@dojo:~$
```
* Nó cũng có thể xử lý nhiều ký tự, trong đó các ký tự ở các vị trí khác nhau của đối số đầu tiên được thay thế bằng các ký tự tương ứng trong đối số thứ hai.
```sh
hacker@dojo:~$ echo PWM.COLLAGE | tr MA NE
PWN.COLLEGE
hacker@dojo:~$
```
* Giờ đến lượt bạn thử! Ở cấp độ này, /challenge/runchương trình sẽ in ra lá cờ nhưng sẽ đảo ngược chữ hoa chữ thường của tất cả các ký tự (ví dụ: Asẽ trở thành avà ngược lại). Bạn có thể hoàn tác thao tác này trvà lấy lại lá cờ không?
* <img width="388" height="38" alt="image" src="https://github.com/user-attachments/assets/0c847dbe-5de5-463e-8374-264ff7e8b4fe" />
* `tr` chỉ làm việc với dữ liệu từ stdin,ko đọc file trực tiếp
* `tr` rất hay đi cùng pipe(|)

</details>
<details>
  <summary><code>🏴Deleting characters(Xóa kí tự)</code></summary>

 * `tr`Cũng có thể dịch các ký tự thành rỗng (tức là xóa chúng). Điều này được thực hiện thông qua một `-d` cờ và một đối số chỉ định các ký tự cần xóa:
```sh
hacker@dojo:~$ echo PAWN | tr -d A
PWN
hacker@dojo:~$
```
* Khá đơn giản! Giờ bạn hãy thử xem. Trong kết quả của lệnh `/challenge/run` tôi sẽ chèn một số ký tự giả (cụ thể là: ^và %) vào giữa các ký tự cờ. Sử dụng `tr -d`lệnh để loại bỏ chúng!
* <img width="332" height="36" alt="image" src="https://github.com/user-attachments/assets/90012f92-ad6c-4c19-a1ee-c1fb65d96bbf" />

</details>
<details>
  <summary><code>🏴Deleting newlines(Xóa dòng mới)</code></summary>

* Một loại ký tự thường bị loại bỏ là ký tự phân cách dòng. Điều này xảy ra khi bạn có một luồng dữ liệu mà bạn muốn chuyển thành một dòng duy nhất để xử lý tiếp. Bạn có thể chỉ định ký tự xuống dòng gần giống như bất kỳ ký tự nào khác, bằng cách sử dụng mã thoát cho chúng:
```sh
hacker@dojo:~$ echo "hello_world!" | tr _ "\n"
hello
world!
hacker@dojo:~$
```
* Ở đây, dấu gạch chéo ngược ( `\`) biểu thị rằng ký tự theo sau nó là ký tự thay thế cho một ký tự khó nhập vào shell thông thường. Tất nhiên, ký tự xuống dòng rất khó nhập vì khi bạn thường nhấn `Enter`, bạn sẽ chạy chính lệnh đó. `\n`là ký tự thay thế cho ký tự xuống dòng này, và nó phải được đặt trong dấu ngoặc kép để ngăn trình thông dịch shell tự cố gắng diễn giải nó và chuyển nó cho`tr`thay vì .

* Bây giờ, hãy kết hợp điều này với thao tác xóa. Trong thử thách này, chúng ta sẽ chèn một loạt ký tự xuống dòng vào cờ. Hãy xóa chúng bằng cờ `tr`'s và ký tự xuống dòng được mã hóa!`-d`

* Thông tin thú vị! Bạn muốn thay thế ký tự dấu gạch chéo ngược ( `\\`)? Vì `\`là ký tự thoát, bạn phải thoát nó! `\\`sẽ được coi là dấu gạch chéo ngược bởi `tr`. Điều này không liên quan đến thử thách này, nhưng dù sao cũng là một thông tin thú vị!
* <img width="374" height="22" alt="image" src="https://github.com/user-attachments/assets/7f1eb2ac-4815-4988-89ce-56d2f6c08af7" />

</details>
<details>
  <summary><code>🏴Extracting the first lines with `head`(Trích xuất các dòng đầu tiên bằng `head`)</code></summary>

*  Trong quá trình làm quen với Linux, bạn sẽ gặp những tình huống cần lấy ngay những dòng đầu tiên của các chương trình rất dài dòng. Để làm điều này, bạn sẽ sử dụng lệnh `head`! `head`Lệnh này được dùng để hiển thị một vài dòng đầu tiên của đầu vào:
```sh
hacker@dojo:~$ cat /something/very/long | head
this
is
just
the
first
ten
lines
of
the
file
hacker@dojo:~$
```
* Theo mặc định, nó hiển thị 10 dòng đầu tiên, nhưng bạn có thể điều chỉnh điều này bằng `-n`tùy chọn:
```sh
hacker@dojo:~$ cat /something/very/long | head -n 2
this
is
hacker@dojo:~$
```
* Bài toán này `/challenge/pwn`xuất ra rất nhiều dữ liệu, và bạn cần sử dụng lệnh pipe `head`để lấy 7 dòng đầu tiên, sau đó chuyển tiếp chúng đến lệnh tiếp theo `/challenge/college`, lệnh này sẽ trả về cờ nếu bạn làm đúng! Giải pháp của bạn sẽ là một lệnh phức hợp dài với hai lệnh pipe kết nối ba lệnh. Chúc may mắn!
* <img width="403" height="42" alt="image" src="https://github.com/user-attachments/assets/4c67938f-31a2-45e7-a3ed-32f2f0280ad7" />

</details>
<details>
  <summary><code>🏴Extracting specific sections of text(Trích xuất các phần văn bản cụ thể)</code></summary>

* Đôi khi, bạn muốn lấy các cột dữ liệu cụ thể, chẳng hạn như cột đầu tiên, cột thứ ba hoặc cột thứ 42. Để làm điều này, bạn có `cut`lệnh.

* Ví dụ, hãy tưởng tượng bạn có tệp dữ liệu sau:
```sh
hacker@dojo:~$ cat scores.txt
hacker 78 99 67
root 92 43 89
hacker@dojo:~$
```
* Bạn có thể sử dụng `cut`để trích xuất các cột cụ thể:
```sh
hacker@dojo:~$ cut -d " " -f 1 scores.txt
hacker
root
hacker@dojo:~$ cut -d " " -f 2 scores.txt
78
92
hacker@dojo:~$ cut -d " " -f 3 scores.txt
99
43
hacker@dojo:~$
```
* Tham số này chỉ định ký tự phân cách`-d` cột (cách các cột được phân tách). Trong trường hợp này, đó là ký tự khoảng trắng. Tất nhiên, nó phải được đặt trong dấu ngoặc kép để trình thông dịch lệnh biết rằng khoảng trắng đó là một tham số chứ không phải là khoảng trắng phân tách các tham số khác! Tham số này chỉ định số thứ tự trường (cột cần trích xuất).`-f`

* Trong thử thách này, `/challenge/run`chương trình sẽ cung cấp cho bạn một loạt các dòng với các số ngẫu nhiên và các ký tự đơn (các ký tự của lá cờ) dưới dạng các cột. Sử dụng `cut`để trích xuất các ký tự của lá cờ, sau đó chuyển chúng đến `tr -d "\n"`(giống như cấp độ trước!) để ghép chúng lại với nhau thành một dòng duy nhất. Giải pháp của bạn sẽ trông giống như `/challenge/run | cut ??? | tr ???`, với đã được ???điền đầy đủ.
 + B1 : chạy /challenge/run xem có mấy cột
* <img width="411" height="34" alt="image" src="https://github.com/user-attachments/assets/08c97b4f-22cd-46d3-a44b-54e715aeb45b" />
 + `-d " " ` có nghĩa là cho biết các cột được ngăn cách bằng kí tự gì, vd: như câu này là dấu `space`
</details>
<details>
  <summary><code>🏴Sorting data(Sắp xếp dữ liệu)</code></summary>

 * Các tập tin (hoặc các dòng đầu ra của lệnh) không phải lúc nào cũng được sắp xếp theo thứ tự bạn cần! sortLệnh này giúp bạn tổ chức dữ liệu. Nó đọc các dòng từ đầu vào (hoặc tập tin) và xuất chúng theo thứ tự đã được sắp xếp:
```sh
hacker@dojo:~$ cat names.txt
  hack
  the
  planet
  with
  pwn
  college
hacker@dojo:~$ sort names.txt
  college
  hack
  planet
  pwn
  the
  with
hacker@dojo:~$
```
* Mặc định, `sort`chương trình sắp xếp các dòng theo thứ tự bảng chữ cái. Có thể thay đổi điều này bằng các tham số:

`-r`Thứ tự ngược lại (từ Z đến A)
`-n`: sắp xếp theo thứ tự số (cho các số)
`-u`Chỉ giữ lại các dòng duy nhất (loại bỏ các dòng trùng lặp)
`-R`Thứ tự ngẫu nhiên!
Trong thử thách này, có một tập tin `/challenge/flags.txt`hứa 100 lá cờ giả, trong đó có một lá cờ thật. Khi sắp xếp theo thứ tự bảng chữ cái, lá cờ thật sẽ nằm ở cuối (chúng tôi đã đảm bảo điều này khi tạo ra các lá cờ giả). Cố lên nào!


</details>
