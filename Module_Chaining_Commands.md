# Chaining Commands
*  Trong mô-đun đường ống, bạn đã khám phá khái niệm sử dụng nhiều lệnh, với dữ liệu truyền giữa chúng thông qua các đường ống, để thực hiện một việc phức tạp hơn một chút so với việc sử dụng các lệnh riêng lẻ. Tất nhiên, khái niệm này cũng áp dụng độc lập với việc truyền dữ liệu: đôi khi, bạn có thể muốn chạy một số lệnh liên tiếp nhanh chóng để đạt được một hiệu ứng tích lũy nào đó.

* Module này sẽ đề cập đến một vài cách, ngoài việc sử dụng đường ống (piping), để xích chuỗi các lệnh lại với nhau. Sau khi hoàn thành, bạn sẽ có thể tự viết các script shell !
<details>
<summary><code>🏴Chaining with Semicolons(Nối chuỗi bằng dấu `;`)</code></summary>

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
<summary><code>🏴Building on Success(Xây dựng trên nền tảng thành công)</code></summary>

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
<summary><code>🏴Handing  Failure(Xử lý thất bại)</code></summary>

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
<summary><code>🏴Your First Shell Script(Tệp lệnh Sell đầu tiên của bạn)</code></summary>

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
<summary><code>🏴Redirecting Script Output(Chuyển hướng đầu ra của tập lệnh)</code></summary>

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
<summary><code>🏴Executable Shell Scripts(Các tập lệnh Shell có thể thực thi)</code></summary>

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
<summary><code>🏴Understanding Shebangs(Hiểu về `Shebangs`)</code></summary>

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
<summary><code>🏴Scripting with Arguments(Lập trình kịch bản với đối số)</code></summary>

 * Bạn đã học cách tạo các tập lệnh shell, nhưng cho đến nay chúng chỉ là danh sách các lệnh. Các tập lệnh sẽ trở nên mạnh mẽ hơn nhiều khi chúng có thể chấp nhận các đối số! Điều này có thể trông như sau:
```sh
hacker@dojo:~$ bash myscript.sh hello world
```
* Tập lệnh có thể truy cập các đối số này bằng cách sử dụng các biến đặc biệt:
 - $1chứa đối số đầu tiên ("hello")
 - $2chứa đối số thứ hai ("thế giới")
 - $3sẽ bao gồm lập luận thứ ba (nếu có).
 -  ...và cứ thế tiếp tục
* Đây là một ví dụ đơn giản:
```sh
hacker@dojo:~$ cat myscript.sh
#!/bin/bash
echo "First argument: $1"
echo "Second argument: $2"
hacker@dojo:~$ bash myscript.sh hello world
First argument: hello
Second argument: world
hacker@dojo:~$
```
* Đối với thử thách này, bạn cần viết một kịch bản như `/home/hacker/solve.sh`sau:

1.Cần hai đối số

2.Xuất các giá trị theo thứ tự NGƯỢC (đối số thứ hai trước, sau đó là đối số thứ nhất).
* Ví dụ:
```sh
hacker@dojo:~$ bash /home/hacker/solve.sh pwn college
college pwn
hacker@dojo:~$
```
* Sau khi kịch bản của bạn hoạt động chính xác, hãy chạy `/challenge/run`để lấy cờ!
* <img width="401" height="98" alt="image" src="https://github.com/user-attachments/assets/cedf8051-b02a-4681-830f-7d48ace7e35c" />
* `Lưu ý` : Thử thách này giúp ra hiểu cách `shell` truyền và nhận tham số , shell sẽ sử dụng dấu `cách` giữa các đối số để phân chia các đối số với các giá trị `$`, và khi thực thi shell sẽ dựa vào thứ tự các đối số để thực thi các lệnh trong file.
</details>
<details>
<summary><code>🏴Scripting with Conditionals(Lập trình kịch bản với điều kiện)</code></summary>

* Giờ bạn đã có thể sử dụng các tham số trong kịch bản, hãy làm cho chúng thông minh hơn bằng logic điều kiện!

* Trong bash, bạn có thể sử dụng `if`các câu lệnh để đưa ra quyết định:
```sh
if [ "$1" == "ping" ]
then
    echo "pong"
fi
```
* Đoạn mã trên, bằng tiếng Anh, là `if the first argument is "ping", print out "pong"`. Cú pháp khá khắt khe vì một vài lý do. Thứ nhất, bạn phải có khoảng trắng sau `if`(nếu bạn quen với một ngôn ngữ như C, điều này sẽ khác), sau `[`, và trước `]`. Thứ hai, `if`, `then`, và `fi`phải nằm trên các dòng khác nhau (hoặc được phân cách bằng dấu chấm phẩy); bạn không thể gộp chúng vào cùng một câu lệnh. Nó cũng hơi kỳ lạ: thay vì `endif`hoặc `end`hoặc đại loại như vậy, ký tự kết thúc của `if`câu lệnh là `fi`( `if`viết ngược). Chỉ là điều bạn cần nhớ.

* Đối với thử thách này, hãy viết một kịch bản như `/home/hacker/solve.sh`sau:

Lấy một lập luận
Nếu đối số là "pwn", hãy xuất ra "college".
Với bất kỳ đầu vào nào khác, không xuất ra gì cả.
Ví dụ:

hacker@dojo:~$ bash /home/hacker/solve.sh pwn
college
hacker@dojo:~$ bash /home/hacker/solve.sh foo
hacker@dojo:~$
Sau khi kịch bản của bạn hoạt động chính xác, hãy chạy /challenge/runđể lấy cờ!

LƯU Ý: Bạn muốn tìm hiểu thêm về những điều kiện khác mà một điều kiện có thể kiểm tra, ngoài việc so sánh chuỗi? Hãy đọc tất cả về điều đó với help test! 
* <img width="403" height="57" alt="image" src="https://github.com/user-attachments/assets/53621b4c-0c89-4b45-a073-c6a026d663c1" />
 - Đầu tiên ta chạy lệnh `nano /home/hacker/solve.sh` để tạo file và ghi vào file dạng văn bản,sau khi ghi xong ta dùng tổ hợp phím `ctrl+x` để thoát và chọn `y` để lưu , sau đó ấn `enter` để ghi đè lên file đó.
* <img width="355" height="85" alt="image" src="https://github.com/user-attachments/assets/2e9a14f2-3644-4a34-bb37-0efe4d0756c4" />
 - Sau khi cấp quyền thực thi cho file ta chạy lệnh `bash+file+đốiso` chạy file .
</details>
<details>
<summary><code>🏴Scripting with Default Cases(Lập trình kịch bản với các trường hợp mặc định)</code>
</summary>

 * Những phát biểu của bạn `if`cho đến nay chỉ đề cập đến các trường hợp cụ thể, nhưng còn những trường hợp khác thì sao? Đó là lúc `else`chúng tôi phát huy tác dụng!

* Mệnh đề này `else`được thực thi khi `if`điều kiện không đúng:
```sh
if [ "$1" == "hello" ]
then
    echo "Hi there!"
else
    echo "I don't understand"
fi
```
* Lưu ý rằng mệnh đề này `else`không có điều kiện --- nó bắt tất cả những gì không khớp trước đó. Nó cũng không có `then`câu lệnh. Cuối cùng, mệnh đề này `fi`được đặt sau `else`khối lệnh để biểu thị sự kết thúc của toàn bộ câu lệnh phức tạp! Nó cũng là tùy chọn: bạn không có nó ở cấp độ trước đó, và bạn chỉ cần nó nếu logic bạn đang cố gắng thực hiện yêu cầu điều đó.

* Dưới đây là một ví dụ thực tế:
```sh
if [ "$1" == "start" ]
then
    echo "Starting the service..."
else
    echo "Unknown command. Use 'start' to begin."
fi
```
* Đối với thử thách này, hãy viết một kịch bản như `/home/hacker/solve.sh`sau:

   1.Lấy một lập luận
  
   2.Nếu đối số là "pwn", hãy xuất ra "college".
  
   3.Với bất kỳ đầu vào nào khác, hãy xuất ra "nope".
* Ví dụ:
```sh
hacker@dojo:~$ bash /home/hacker/solve.sh pwn
college
hacker@dojo:~$ bash /home/hacker/solve.sh hack
nope
hacker@dojo:~$ bash /home/hacker/solve.sh anything
nope
hacker@dojo:~$
```
* Sau khi kịch bản của bạn hoạt động chính xác, hãy chạy `/challenge/run`để lấy cờ!
* <img width="262" height="80" alt="image" src="https://github.com/user-attachments/assets/f892412f-8d66-4581-a0c4-2914a91dc9da" />
  - Viết vào file `/home/hacker/solve.sh` bằng lệnh `nano` 
 
* <img width="359" height="107" alt="image" src="https://github.com/user-attachments/assets/e92ef16c-fb12-4fb5-b327-883a59445e71" />

</details>
<details>
<summary><code>🏴Scripting with Multiple Conditons(Lập trình kịch bản với nhiều điều kiện)</code></summary>

* Bạn đã học cách sử dụng một `if`câu lệnh duy nhất để kiểm tra một điều kiện. Nhưng nếu bạn cần kiểm tra nhiều điều kiện thì sao? Bạn có thể sử dụng `elif`(viết tắt của `else if`):
```sh
if [ "$1" == "one" ]
then
    echo "1"
elif [ "$1" == "two" ]
then
    echo "2"
elif [ "$1" == "three" ]
then
    echo "3"
else
    echo "unknown"
fi
```
* Lưu ý rằng bạn cần có một `then`câu lệnh `else` sau `elif`, giống như `else` `if`. Như đã nói ở trên, `else`câu lệnh `else` ở cuối sẽ bắt tất cả những phần tử không khớp.

Đối với thử thách này, hãy viết một kịch bản như `/home/hacker/solve.sh`sau:

1.Lấy một lập luận

2.Nếu đối số là "hack", hãy xuất ra "the planet"

3.Nếu đối số là "pwn", hãy xuất ra "college".

4.Nếu đối số là "learn", hãy xuất ra "linux".

5.Với bất kỳ đầu vào nào khác, đầu ra sẽ là "không xác định".
* Ví dụ:
```sh
hacker@dojo:~$ bash /home/hacker/solve.sh hack
the planet
hacker@dojo:~$ bash /home/hacker/solve.sh pwn
college
hacker@dojo:~$ bash /home/hacker/solve.sh learn
linux
hacker@dojo:~$ bash /home/hacker/solve.sh foo
unknown
hacker@dojo:~$
```
* Sau khi kịch bản của bạn hoạt động chính xác, hãy chạy `/challenge/run`để lấy cờ!

LƯU Ý: Khi tạo kịch bản của mình, hãy đảm bảo tuân thủ chặt chẽ khoảng cách trong các ví dụ. Không giống như nhiều ngôn ngữ khác, bash yêu cầu dấu phẩy `[`và dấu cách `]`phải được phân tách với các ký tự khác, nếu không nó không thể phân tích điều kiện.
</details>
<details>
<summary><code>🏴Reading Shell Scripts(Đọc các tệp lệnh `Shell`)</code></summary>

* Bạn không phải là người duy nhất viết script shell! Chúng rất tiện dụng để thực hiện các tác vụ "cấp hệ thống" đơn giản và là công cụ phổ biến mà các nhà phát triển và quản trị viên hệ thống thường sử dụng. Trên thực tế, một phần đáng kể các chương trình trên một máy Linux điển hình là script shell.

* Ở cấp độ này, chúng ta sẽ học cách đọc các tập lệnh shell. `/challenge/run`là một tập lệnh shell yêu cầu bạn nhập mật khẩu bí mật, nhưng mật khẩu đó được mã hóa cứng trong chính tập lệnh! Hãy đọc tập lệnh (sử dụng, ví dụ, `cat`), tìm ra mật khẩu và lấy cờ!

* LƯU Ý: Bạn cũng có thể thử đọc mã nguồn của các bài toán khác! Đọc mã nguồn là một chiến lược quan trọng trong việc học các kỹ năng mới, vì bạn có thể thấy cách thức hoạt động của một số chức năng nhất định và tái sử dụng các chiến lược đó trong các kịch bản của riêng mình. Nhưng hãy cẩn thận: một số tệp chương trình là mã máy và con người sẽ không thể đọc được. Bạn có thể sử dụng lệnh `file`để phân biệt, nhưng hầu hết các bài toán trong Linux Luminarium đều được triển khai dưới dạng kịch bản shell và an toàn để `cat`đọc.
* <img width="375" height="34" alt="image" src="https://github.com/user-attachments/assets/4a9f805f-e0a8-4e70-a83b-d1f676a1906d" />
 - Sử dụng lệnh `echo` để in ra màn hình và pipe `|` để chuyển đầu ra của lệnh `echo` và đầu vào của lệnh `/challenge/run` khi đó  GUESS bên trong sẽ đọc và đối chiếu và xuất ra lá cờ nếu đúng .
* <img width="284" height="54" alt="image" src="https://github.com/user-attachments/assets/3d18f72f-654a-4cae-9819-2f27aef2c0ff" />
 - Ta cũng có thể làm bằng cách khác với việc truy cập vào /challenge bằng lệnh `cd`, sau đó thư mục hiện tại sẽ là `/challenge` và ta dùng lệnh `./run` có nghĩa là chạy file `run` ngay tại thư mục hiện tại rồi nhập theo yêu cầu và lấy flag.

</details>
