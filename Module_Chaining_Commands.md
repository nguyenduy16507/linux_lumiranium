# Chaining Commands
*  Trong mô-đun đường ống, bạn đã khám phá khái niệm sử dụng nhiều lệnh, với dữ liệu truyền giữa chúng thông qua các đường ống, để thực hiện một việc phức tạp hơn một chút so với việc sử dụng các lệnh riêng lẻ. Tất nhiên, khái niệm này cũng áp dụng độc lập với việc truyền dữ liệu: đôi khi, bạn có thể muốn chạy một số lệnh liên tiếp nhanh chóng để đạt được một hiệu ứng tích lũy nào đó.

* Module này sẽ đề cập đến một vài cách, ngoài việc sử dụng đường ống (piping), để xích chuỗi các lệnh lại với nhau. Sau khi hoàn thành, bạn sẽ có thể tự viết các script shell !
<details>
<summary><code>🏴Chaining with Semicolons(Nối chuỗi bằng dấu `;`)</code><summary>

*  Cách dễ nhất để nối các lệnh là sử dụng tổ hợp phím ` ;`. Trong hầu hết các trường hợp, ;tổ hợp phím này phân tách các lệnh tương tự như cách phím Enter phân tách các dòng. Vì vậy, ta có:
```sh
hacker@dojo:~$ echo COLLEGE > pwn
hacker@dojo:~$ cat pwn
COLLEGE
hacker@dojo:~$
```
*  Về cơ bản là tương tự như thế này:
```sh
hacker@dojo:~$ echo COLLEGE > pwn; cat pwn
COLLEGE
hacker@dojo:~$
```
* Về cơ bản, khi bạn nhấn Enter, trình shell sẽ thực thi lệnh bạn đã gõ và sau khi lệnh đó kết thúc, nó sẽ hiển thị dấu nhắc để bạn nhập lệnh khác. Dấu chấm phẩy cũng tương tự, chỉ khác là không có dấu nhắc và bạn phải nhập cả hai lệnh trước khi bất kỳ lệnh nào được thực thi.

* Hãy thử ngay! Ở màn này, bạn phải chạy `/challenge/pwn`và sau đó `/challenge/college`, nối chúng lại bằng dấu chấm phẩy.
</details>
<details>
<summary><code>🏴Building on Success(Xây dựng trên nền tảng thành công)</code><summary>

*  Bạn đã học về mã thoát trong mô-đun Quy trình . Bây giờ, hãy sử dụng chúng để kết hợp các lệnh lại với nhau!

* Toán tử này &&cho phép bạn chạy lệnh thứ hai chỉ khi lệnh đầu tiên thành công (theo quy ước của Linux, điều này có nghĩa là nó thoát với mã 0). Nó được gọi là toán tử "AND" vì cả hai điều kiện phải đúng: lệnh đầu tiên phải thành công VÀ sau đó lệnh thứ hai mới được chạy. Điều này cực kỳ hữu ích cho các quy trình làm việc phức tạp trên dòng lệnh, nơi một số hành động phụ thuộc vào sự thành công của các hành động khác.

Đây là cú pháp:
```sh
hacker@dojo:~$ command1 && command2
```
* Điều này có nghĩa là: "Chạy lệnh 1, và NẾU thành công, thì chạy lệnh 2."

*  Một vài ví dụ:
```sh
hacker@dojo:~$ touch /home/hacker/file && echo "this will run"
success
this will run
hacker@dojo:~$ touch /file && echo "this will NOT run"
touch: cannot touch '/file': Permission denied
hacker@dojo:~$
```
* Lần gọi thứ hai đó `touch`đã thất bại vì người dùng hacker không có quyền ghi vào `/file`, do đó lệnh `echo`không được thực thi.

Trong thử thách này, bạn cần nối các chương trình `/challenge/first-success`lại với `/challenge/second`nhau bằng &&toán tử. Hãy thử chạy từng lệnh riêng lẻ trước để xem điều gì xảy ra (bạn sẽ không nhận được cờ). Nhưng nếu bạn nối chúng lại với nhau bằng toán tử `&&`, cờ sẽ xuất hiện!
</details>
<details>
<summary><code>🏴Handing  Failure(Xử lý thất bại)</code><summary>

*  Bạn vừa tìm hiểu về `&&`toán tử `OR`, toán tử này chỉ thực thi lệnh thứ hai nếu lệnh đầu tiên thành công. Bây giờ, hãy cùng tìm hiểu về toán tử ngược lại: `||`toán tử `OR` cho phép bạn thực thi lệnh thứ hai chỉ khi lệnh đầu tiên thất bại (thoát với mã lỗi khác 0). Toán tử này được gọi là toán tử "OR" vì hoặc lệnh đầu tiên thành công HOẶC lệnh thứ hai sẽ được thực thi.

*  Đây là cú pháp:
```sh
hacker@dojo:~$ command1 || command2
```
* Điều này có nghĩa là: "Chạy lệnh 1, và NẾU nó thất bại, thì chạy lệnh 2."

*  Một vài ví dụ:
```sh
hacker@dojo:~$ touch /file || echo "touch failed, so this runs"
touch: cannot touch '/file': Permission denied
touch failed, so this runs
hacker@dojo:~$ touch /home/hacker/file || echo "this will NOT run"
hacker@dojo:~$
```
*  Toán tử này `||`cực kỳ hữu ích để cung cấp các lệnh dự phòng hoặc xử lý lỗi!

*  Trong thử thách này, bạn cần thực hiện phép toán nối chuỗi `/challenge/first-failure`và `/challenge/second`sử dụng ||toán tử. Cố lên nào!

</details>
<details>
<summary><code>🏴Your First Shell Script(Tệp lệnh Sell đầu tiên của bạn)</code><summary>

*  Khi bạn kết hợp ngày càng nhiều lệnh để đạt được các hiệu ứng phức tạp, độ dài của lời nhắc kết hợp sẽ nhanh chóng trở nên rất khó chịu. Khi điều này xảy ra, bạn có thể đặt các lệnh này vào một tệp, được gọi là tập lệnh shell , và chạy chúng bằng cách thực thi tệp đó! Ví dụ, hãy xem xét kỹ thuật dấu chấm phẩy của chúng ta:
```sh
hacker@dojo:~$ echo COLLEGE > pwn; cat pwn
COLLEGE
hacker@dojo:~$
```
* Chúng ta có thể tạo một tập lệnh shell có tên là `pwn.sh`(theo quy ước, các tập lệnh shell thường được đặt tên kèm theo `sh`hậu tố):
```sh
echo COLLEGE > pwn
cat pwn
```
*  Và sau đó chúng ta có thể thực thi bằng cách truyền nó như một đối số cho một thể hiện mới của shell của chúng ta ( `bash`)! Khi một shell được gọi theo cách này, thay vì nhận lệnh từ người dùng, nó sẽ đọc lệnh từ tệp.
```sh
hacker@dojo:~$ ls
hacker@dojo:~$ bash pwn.sh
COLLEGE
hacker@dojo:~$ ls
pwn
hacker@dojo:~$
```
*  Như bạn thấy, tập lệnh shell đã thực thi cả hai lệnh, tạo và in tập `pwn`tin.

*  Giờ đến lượt bạn! Tương tự như màn trước, chạy lệnh `/challenge/pwn`rồi sau đó `/challenge/college`, nhưng lần này trong một tập lệnh shell có tên `x.sh`, rồi chạy nó bằng lệnh `bash`!

*  LƯU Ý: Chúng ta vẫn chưa nói về hàng loạt trình soạn thảo tệp dòng lệnh mạnh mẽ tuyệt vời của Linux. Hiện tại, bạn có thể thoải mái sử dụng ứng `Text Editor`dụng ở chế độ Desktop ( `Applications->Accessories->Text Editor`) hoặc trình soạn thảo mặc định trong VSCode Workspace!
*  <img width="344" height="56" alt="image" src="https://github.com/user-attachments/assets/223b2a10-5816-436a-b391-bbee36697314" />
 - Ta sử dụng lệnh như trên để lưu các lệnh vào file sau đó mở file để chạy toàn bộ lệnh 
 - Nếu muốn chứa nhiều câu lệnh vào 1 file ta có thể dùng các trình chỉnh sửa văn bản như `nano` hay `vim` . VD:`nano.sh hay vim.sh`.

</details>
<details>
<summary><code>🏴Redirecting Script Output(Chuyển hướng đầu ra của tập lệnh)</code><summary>

* Hãy thử một cái gì đó phức tạp hơn một chút! Bạn đã chuyển hướng đầu ra giữa các chương trình bằng lệnh `pip` `|`, nhưng cho đến nay, điều này chỉ áp dụng giữa đầu ra của một lệnh và đầu vào của một lệnh khác. Nhưng nếu bạn muốn gửi đầu ra của nhiều chương trình đến một lệnh thì sao? Có một vài cách để làm điều này, và chúng ta sẽ khám phá một cách đơn giản ở đây: chuyển hướng đầu ra từ tập lệnh của bạn!

Đối với giao diện dòng lệnh, tập lệnh của bạn chỉ là một lệnh khác. Điều đó có nghĩa là bạn có thể chuyển hướng đầu vào và đầu ra của nó giống như bạn đã làm với các lệnh trong mô-đun `Piping` ! Ví dụ, bạn có thể ghi nó vào một tệp:
```sh
hacker@dojo:~$ cat script.sh
echo PWN
echo COLLEGE
hacker@dojo:~$ bash script.sh > output
hacker@dojo:~$ cat output
PWN
COLLEGE
hacker@dojo:~$
```
* Tất cả các phương pháp chuyển hướng khác nhau đều hoạt động: `>`đối với stdout, `2>`stderr, `<`stdin, `>>`và `2>>`đối với chuyển hướng ở chế độ nối thêm, `>&`chuyển hướng đến các bộ mô tả tệp khác và |chuyển hướng đầu ra đến một lệnh khác.

* Ở cấp độ này, chúng ta sẽ thực hành việc truyền dữ liệu (piping `|`) từ tập lệnh của bạn đến một chương trình khác. Vì các tập lệnh có thể thực thi sẽ được đề cập sau, hãy chạy tập lệnh của bạn với lệnh `bash`pipe khi bạn truyền đầu ra của nó. Giống như trước đây, bạn cần tạo một `.sh`tập lệnh gọi `/challenge/pwn`lệnh pipe, sau đó gọi `/challenge/college`lệnh pipe, và truyền đầu ra của tập lệnh pipe vào một lần gọi duy nhất của `/challenge/solve`lệnh pipe.
* <img width="401" height="99" alt="image" src="https://github.com/user-attachments/assets/18e00ad3-cc86-43ae-9e89-ffdcb1738a6a" />

* `Chú ý` : Dấu pipe `|` trong Shell/Bash dùng để lấy luồng đầu ra chuẩn(stdout) của lệnh nằm bên trái và chuyển trực tiếp thành luổng đầu vào chuẩn(stdin) cho lệnh nằm bên phải
* `VD` : `lệnh 1 | lệnh 2` : Kết quả của lệnh 1 thay vì in ra màn hình sẽ được đẩy qua `đường oongs(pipe)`, lệnh 2 sẽ nhận dữ liệu từ đường ống đó để xử lý tiếp mà không cần bạn nhập từ bàn phím.
</details>
<details>
<summary><code>🏴Executable Shell Scripts(Các tập lệnh Shell có thể thực thi)</code><summary>
</details>
<details>
<summary><code>🏴Understanding Shebangs(Hiểu về `Shebangs`)</code><summary>
</details>
<details>
<summary><code>🏴Scripting with Arguments(Lập trình kịch bản với đối số)</code><summary>
</details>
<details>
<summary><code>🏴Scripting with Conditionals(Lập trình kịch bản với điều kiện)</code><summary>
</details>
<details>
<summary><code>🏴Scripting with Default Cases(Lập trình kịch bản với các trường hợp mặc định)</code><summary>
</details>
<details>
<summary><code>🏴Scripting with Multiple Conditons(Lập trình kịch bản với nhiều điều kiện)</code><summary>
</details>
<details>
<summary><code>🏴Reading Shell Scripts(Đọc các tệp lệnh `Shell`)</code><summary>
</details>
