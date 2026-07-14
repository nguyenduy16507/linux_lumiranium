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
</details>
<details>
  <summary><code>🏴Extracting the first lines with `head`(Trích xuất các dòng đầu tiên bằng `head`)</code></summary>
</details>
<details>
  <summary><code>🏴Extracting specific sections of text(Trích xuất các phần văn bản cụ thể)</code></summary>
</details>
<details>
  <summary><code>🏴Sorting data(Sắp xếp dữ liệu)</code></summary>
</details>
