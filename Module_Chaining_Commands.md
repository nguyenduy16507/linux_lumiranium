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
   - `>` : Ghi đè vào cuối file
   - `>>` : Nối thêm vào cuối file
   - `2>` : Ghi đè lỗi vào file
   - `2>>` : Nối thêm lỗi vào file
   - `<` : Lấy dữ liệu đầi vào từ file
   - `>&` : Gom luồng, chuyển lệnh từ luồng này sang luồng khác(VD: 2>&1)
</details>
<details>
<summary><code>🏴Executable Shell Scripts(Các tập lệnh Shell có thể thực thi)</code><summary>

 * Bạn đã viết xong tập lệnh shell đầu tiên của mình, nhưng việc gọi nó thông qua lại `bash script.sh`khá rắc rối. Tại sao bạn cần điều đó `bash`?

* Khi bạn gọi lệnh này `bash script.sh`, tất nhiên bạn đang khởi chạy `bash`lệnh với `script.sh`đối số. Điều này cho `bash` biết rằng nó sẽ đọc các lệnh từ `script.sh`thay vì đầu vào chuẩn, và do đó tập lệnh shell của bạn sẽ được thực thi.

* Hóa ra bạn có thể tránh việc phải tự tay gọi lệnh `bash`. Nếu tập lệnh shell của bạn có thể thực thi được (hãy nhớ lại `Quyền truy cập tập tin` ), bạn chỉ cần gọi nó thông qua đường dẫn tương đối hoặc tuyệt đối! Ví dụ, nếu bạn tạo tập `script.sh`lệnh trong thư mục chính của mình và cấp quyền thực thi cho nó , bạn có thể gọi nó thông qua `/home/hacker/script.sh`hoặc `~/script.sh`hoặc  `./script.sh` (nếu thư mục làm việc của bạn là `/home/hacker`).

* Hãy thử cách này xem! Tạo một shellscript để gọi hàm đó `/challenge/solve`, cấp quyền thực thi cho nó, và chạy nó mà không cần gọi hàm một cách rõ ràng `bash`!
* <img width="379" height="59" alt="image" src="https://github.com/user-attachments/assets/770dd04e-acd0-439c-ae8e-343a7513dbd1" />
 - Thử thách này ta phải tạo 1 file shellscript sau đó ta sử dụng lệnh `chmod` để cấp quyền thực thi cho nó, sau đó chạy nó mà không cần gọi hàm `bash`, sử dụng lệnh `./script.sh`
* Câu lệnh `home/hacker/script.sh hoặc ~/script.sh hoặc là ./script.sh (với thư mục là home/hacker)` được sử dụng để thực thi sau khi có/được cấp quyền thực thi để tránh sử dụng lệnh `bash`
 -> Ý nghĩa cốt lõi của kiểu lệnh này là khi đã có quyền thực thi thì bạn chỉ cần gõ `./+file` là hệ thống sẽ tự nhìn vào dòng `Shebang` để biết phải dùng `Bash,Zsh,Python,perl hay Node.js` để chạy file đó.Bạn không cần quan tâm script này viết bằng ngôn ngữ gì, bạn chỉ cần chạy đúng tên file là nó tự chạy đúng môi trường.                
</details>
<details>
<summary><code>🏴Understanding Shebangs(Hiểu về `Shebangs`)</code><summary>

 * Bạn đang tiến rất gần đến cuộc sống mới của mình với tư cách là một lập trình viên shell! Tuy nhiên, cho đến nay, các shellscript của bạn chỉ có thể được chạy từ shell . Mọi thứ hoạt động rất tốt ở cấp độ trước (vì bạn đang gọi script của mình từ `bash`shell), nhưng chúng sẽ không hoạt động nếu script của bạn được gọi bởi, ví dụ, một chương trình được viết bằng Python (hoặc bất kỳ ngôn ngữ nào khác).

Khi một chương trình được gọi trong Linux, nhân Linux trước tiên sẽ kiểm tra tệp để xác định cách thức chạy chương trình đó. Quá trình này KHÔNG sử dụng phần mở rộng (đó là lý do tại sao bạn không cần đặt tên cho các tập lệnh shell của mình với `.sh`phần mở rộng, hoặc các tập lệnh Python của mình với `.py`phần mở rộng, v.v.). Thay vào đó, Linux xem xét một vài byte đầu tiên của tệp để tìm thông tin này.

Có rất nhiều loại chương trình khác nhau, nhưng nếu tệp chương trình bắt đầu bằng các ký tự `#!`(thường được gọi là " `shebang` "), Linux sẽ coi tệp đó là một chương trình được thông dịch , và nội dung của phần còn lại của dòng là đường dẫn đến trình thông dịch . Sau đó, nó sẽ gọi trình thông dịch với đường dẫn đến tệp chương trình làm đối số duy nhất.

Hãy xem xét đoạn mã lệnh shell này:
```sh
#!/bin/bash

echo "Hello Hackers!"
```
* Việc này có thể được thực hiện như sau:
```sh
hacker@dojo:~$ chmod a+x script.sh
hacker@dojo:~$ ./script.sh
Hello Hackers!
hacker@dojo:~$
```
* Khi `./script.sh`được thực thi, Linux mở tệp, đọc dòng đầu tiên, trích xuất `/bin/bash`dưới dạng trình thông dịch và thực thi `/bin/bash ./script.sh`để chạy tập lệnh!

* Lưu ý, dòng `shebang` phải là dòng ĐẦU TIÊN của tập tin - không được có dòng trống hoặc khoảng trắng trước đó!

* Đối với thử thách này, hãy tạo một tập lệnh `/home/hacker/solve.sh`có dòng shebang hợp lệ và xuất ra "hack the planet". Nhớ cấp quyền thực thi cho tập lệnh, sau đó chạy `/challenge/run`để xác minh xem tập lệnh của bạn có hoạt động chính xác hay không!

* THÔNG TIN THÚ VỊ: Những từ viết tắt phổ biến bạn có thể thấy:
```sh
`#!/bin/bash`cho các tập lệnh bash
`#!/usr/bin/python3`cho các tập lệnh Python
`#!/bin/sh`Đối với các tập lệnh shell POSIX --- đây là một phiên bản tiền thân thô sơ hơn `bash`với ít tính năng hơn, nhưng tương thích tốt hơn với các hệ thống không phải Linux!
```
* <img width="398" height="86" alt="image" src="https://github.com/user-attachments/assets/435d144f-e053-42fc-a8b3-091305cc6703" />
 -Lưu ý : viết 1 file có chứa các dòng `shebang` ở ngay đầu tiên và cấp quyền thực thi cho nó ,sau đó ta có thể chạy các lệnh `./+Tên file` để chạy nó .
     + `Shellscript` có thể được coi như là 1 lệnh như các lệnh khác trong linux .
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
