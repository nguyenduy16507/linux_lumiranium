# File Globbing

Chỉ cần gõ vài cấp độ thôi, bạn có thể đã thấy mệt mỏi vì phải gõ lại tất cả các đường dẫn tệp. May mắn thay, shell có giải pháp: sử dụng ký tự đại diện (globbing)! Đó là điều chúng ta sẽ học trong module này.

Trước khi thực thi các lệnh bạn nhập vào, shell sẽ thực hiện các phép biến đổi mở rộng trên chúng, và một trong những phép biến đổi mở rộng đó là globbing. Globbing cho phép bạn tham chiếu đến các tệp mà không cần phải gõ toàn bộ tên tệp hoặc gõ toàn bộ đường dẫn của chúng. Hãy cùng tìm hiểu sâu hơn!

<details>
  <summary><code>📒Further Reading(Đọc Thêm)</code></summary>

  
</details>

<details>
  <summary><code>🏴Matching with `*`(Phù hợp với *) </code></summary>

 * Glob đầu tiên chúng ta sẽ học là *`. Khi gặp một *ký tự trong bất kỳ đối số nào, shell sẽ coi nó là "ký tự đại diện" và cố gắng thay thế đối số đó bằng bất kỳ tệp nào khớp với mẫu. Sẽ dễ hiểu hơn nếu chỉ nhìn minh họa hơn là giải thích bằng lời:
```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_*
Look: file_a file_b file_c
```
* Tất nhiên, mặc dù trong trường hợp này, biểu thức chính quy tạo ra nhiều đối số, nhưng nó cũng có thể chỉ khớp với một đối số duy nhất. Ví dụ:
```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: file_*
Look: file_a
```
* Khi không có tệp nào khớp, theo mặc định, shell sẽ giữ nguyên mẫu glob:
```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: nope_*
Look: nope_*
```
* Hàm này *khớp với bất kỳ phần nào của tên tệp ngoại trừ ký tự mở /đầu hoặc .ký tự đầu tiên. Ví dụ:
```sh
hacker@dojo:~$ echo ONE: /ho*/*ck*
ONE: /home/hacker
hacker@dojo:~$ echo TWO: /*/hacker
TWO: /home/hacker
hacker@dojo:~$ echo THREE: ../*
THREE: ../hacker
```
* Giờ thì hãy tự mình thực hành nhé! Bắt đầu từ thư mục chính của bạn, hãy thay đổi thư mục thành /challenge, nhưng hãy sử dụng globbing để giới hạn đối số bạn truyền cho cdtối đa bốn ký tự! Khi đã đến đó, hãy chạy /challenge/runđể giành lấy lá cờ!

* <img width="803" height="113" alt="image" src="https://github.com/user-attachments/assets/32c4ea09-fa24-411f-a4cc-7acb2c4470c0" />

</details>

<details>
  <summary><code>🏴Matching with `?`(Phù hợp với ?)</code></summary>

* Tiếp theo, chúng ta hãy tìm hiểu về ?`.`. Khi gặp một ?ký tự trong bất kỳ đối số nào, shell sẽ coi nó như một ký tự đại diện đơn . Điều này hoạt động giống như *`,` nhưng chỉ khớp với một ký tự. Ví dụ:
```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_cc
hacker@dojo:~$ ls
file_a	file_b	file_cc
hacker@dojo:~$ echo Look: file_?
Look: file_a file_b
hacker@dojo:~$ echo Look: file_??
Look: file_cc
```
* Bây giờ, hãy tự mình thực hành! Bắt đầu từ thư mục chính của bạn, hãy thay đổi thư mục thành /challenge, nhưng sử dụng ?ký tự thay vì cvà ltrong đối số của cd! Khi đã ở đó, hãy chạy /challenge/runlệnh để lấy cờ!
* <img width="810" height="109" alt="image" src="https://github.com/user-attachments/assets/a1f7c290-983e-42ae-9767-6106f39bcace" />

</details>

<details>
  <summary><code>🏴Matching with `[]`(Phù hợp với [])</code></summary>

* Tiếp theo, chúng ta sẽ tìm hiểu về []. Về cơ bản, dấu ngoặc vuông là một dạng giới hạn của ?, ở chỗ thay vì khớp với bất kỳ ký tự nào, []nó là một ký tự đại diện cho một tập hợp con các ký tự tiềm năng, được chỉ định bên trong dấu ngoặc. Ví dụ, [pwn]sẽ khớp với các ký tự p, w, hoặc n. Ví dụ:
```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```
* Hãy thử ở đây! Chúng tôi đã đặt một loạt các tệp trong /challenge/files. Thay đổi thư mục làm việc của bạn thành /challenge/filesvà chạy /challenge/runvới một đối số duy nhất để sử dụng cú pháp ngoặc vuông cho file_b, file_a, file_s, và file_h!
* <img width="854" height="109" alt="image" src="https://github.com/user-attachments/assets/f831fbb6-52a7-45ad-a3a0-ab665705e05e" />

</details>

<details>
  <summary><code>🏴Matching parths with `[]`(Tìm các đường dẫn khớp với [])</code></summary>

* Việc sử dụng ký tự đại diện (globbing) diễn ra trên cơ sở từng đường dẫn , vì vậy bạn có thể mở rộng toàn bộ đường dẫn bằng các đối số đã được đại diện. Ví dụ:
```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: /home/hacker/file_[ab]
Look: /home/hacker/file_a /home/hacker/file_b
```
* Giờ đến lượt bạn. Một lần nữa, chúng tôi đã đặt một loạt các tập tin vào thư mục /challenge/files. Bắt đầu từ thư mục chính của bạn, hãy chạy lệnh /challenge/runvới một đối số duy nhất để lấy các đường dẫn tuyệt đối đến các tập tin file_b, file_a, file_s, và file_h!
* <img width="946" height="76" alt="image" src="https://github.com/user-attachments/assets/865b933d-17c9-44d1-bbb4-32ad64b6c7b4" />

</details>

<details>
  <summary><code>🏴Multiple globs(Nhiều khối cầu)</code></summary>

*  Cho đến nay, bạn mới chỉ chỉ định một mẫu glob tại một thời điểm, nhưng bạn có thể làm nhiều hơn nữa! Bash hỗ trợ mở rộng nhiều mẫu glob trong một từ duy nhất. Ví dụ:
```sh
hacker@dojo:~$ cat /*fl*
pwn.college{YEAH}
hacker@dojo:~$
```
* Điều xảy ra ở trên là trình thông dịch lệnh tìm kiếm tất cả các tệp /bắt đầu bằng bất kỳ ký tự nào (kể cả không có gì), sau đó có một ký tự fvà một ký tự khác l, và kết thúc bằng bất kỳ ký tự nào (kể cả ag, điều này tạo thành flag).

* Giờ bạn hãy thử xem. Chúng tôi đã đặt một vài tập tin vui vẻ, nhưng có tên khác nhau vào thư mục đó /challenge/files. Hãy vào cdđó và chạy lệnh /challenge/run, cung cấp một đối số duy nhất: một từ ngắn (3 ký tự trở xuống) được mã hóa bằng ký tự đặc biệt, *chứa hai ký tự đặc biệt bao phủ mọi từ có chứa chữ cái đó p.
* <img width="755" height="111" alt="image" src="https://github.com/user-attachments/assets/38d9fba2-b9ce-43cb-8fa5-52a33edb034b" />

</details>

<details>
  <summary><code>🏴Mixing glob(Trộn các cục)</code></summary>

 * Giờ thì hãy kết hợp các cấp độ trước lại với nhau! Chúng ta đã đặt một vài tập tin vui vẻ nhưng có tên khác nhau vào thư mục /challenge/files. Hãy vào cdđó và, sử dụng cú pháp globbing mà bạn đã học, hãy viết một chuỗi glob ngắn (6 ký tự trở xuống) mà (khi được truyền làm đối số cho /challenge/run) sẽ chỉ khớp với các tập tin "challenging", "educational" và "pwning"!

* GỢI Ý: Hãy chú ý đến tên các tệp trong thư mục đó /challenge/files. Bạn có thấy bất kỳ mẫu nào có thể giúp bạn tạo ra mẫu glob không?
* <img width="792" height="100" alt="image" src="https://github.com/user-attachments/assets/ac0556b1-9739-4c89-b4d3-684f1a65aac1" />

</details>

<details>
  <summary><code>🏴Exclusionary globbing(Sự toàn cầu hóa mang tính loại trừ)</code></summary>

*  Đôi khi, bạn muốn lọc các tập tin trong một glob! May mắn thay, lệnh này []giúp bạn làm điều đó. Nếu ký tự đầu tiên trong dấu ngoặc là `a` !hoặc (trong các phiên bản bash mới hơn) là `b` ^, glob sẽ đảo ngược và trường hợp trong dấu ngoặc đó sẽ khớp với các ký tự không được liệt kê. Ví dụ:
```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[!ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[^ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```
* Với kiến ​​thức này, hãy tiến /challenge/fileshành xử /challenge/runlý tất cả các tập tin không bắt đầu bằng p, w, hoặc n!

* LƯU Ý: Ký tự này !có ý nghĩa đặc biệt khác trong bash khi nó không phải là ký tự đầu tiên của một []glob, vì vậy hãy nhớ điều đó nếu mọi thứ trở nên khó hiểu! ^không gặp vấn đề này, nhưng cũng không tương thích với các shell cũ hơn.
* <img width="891" height="110" alt="image" src="https://github.com/user-attachments/assets/a671429a-d556-482e-b1a7-51784418ee44" />

</details>

<details>
<summary><code>🏴Tab completion(Hoàn thành tab)</code></summary>

* Dù có vẻ hấp dẫn, việc sử dụng *ký tự đại diện (glob) để rút ngắn những gì cần gõ trên dòng lệnh có thể dẫn đến sai sót. Ký tự đại diện của bạn có thể mở rộng thành các tệp không mong muốn, và bạn có thể không phát hiện ra điều đó cho đến khi rmlệnh đã được thực thi! Không ai tránh khỏi kiểu lỗi này.

* Một giải pháp an toàn hơn khi bạn muốn chỉ định một mục tiêu cụ thể là tính năng tự động hoàn thành bằng phím Tab . Nếu bạn nhấn phím Tab trong shell, nó sẽ cố gắng đoán xem bạn sẽ gõ gì và tự động hoàn thành nó. Tính năng tự động hoàn thành rất hữu ích, và thử thách này sẽ khám phá cách sử dụng nó trong việc chỉ định tệp.

* Thử thách này đã sao chép cờ vào thư mục /challenge/pwncollege, và bạn có thể tự do truy cập cattệp đó. Nhưng bạn không thể gõ tên tệp: chúng tôi đã sử dụng một số thủ thuật tinh vi để đảm bảo rằng bạn phải tự động hoàn thành bằng phím Tab. Hãy thử xem!
```sh
hacker@dojo:~$ ls /challenge
DESCRIPTION.md  pwncollege
hacker@dojo:~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@dojo:~$ cat /challenge/pwn<TAB>
pwn.college{HECK YEAH}
hacker@dojo:~$
```
* Khi bạn nhấn phím Tab, tên tệp sẽ mở rộng và bạn có thể đọc tệp. Chúc may mắn!
* Ta gõ ` cat /challenge/pwn + phím Tab `
* <img width="723" height="93" alt="image" src="https://github.com/user-attachments/assets/bbadfaea-a1bf-4903-90a8-26f40c53186e" />


</details>

 <details> 
<summary><code>🏴Multiple options for tab completion(Nhiều lựa chọn để tự động hoàn thành bằng phím Tab)</code></summary>

* Hãy xem xét tình huống sau:
```sh
hacker@dojo:~$ ls
flag  flamingo  flowers
hacker@dojo:~$ cat f<TAB>
```
*Có nhiều lựa chọn! Chuyện gì sẽ xảy ra?

 - Những gì xảy ra sẽ khác nhau tùy thuộc vào trình thông dịch lệnh cụ thể và các tùy chọn của nó. Theo mặc định , nó bashsẽ tự động mở rộng cho đến điểm đầu tiên có nhiều tùy chọn (trong trường hợp này là fl). Khi bạn nhấn phím Tab lần thứ hai , nó sẽ in ra các tùy chọn đó. Ngược lại, các trình thông dịch lệnh và cấu hình khác sẽ duyệt qua các tùy chọn theo trình tự.

 - Thử thách này có một /challenge/filesthư mục chứa nhiều tập tin bắt đầu bằng dấu chấm `pwncollege`. Sử dụng chức năng tự động hoàn thành bằng phím Tab từ /challenge/files/phoặc tương tự, và tìm đường đến lá cờ!
 - Thực hiện phím tab nhiều lần tùy bài để tìm ra tên chính  
* <img width="1054" height="130" alt="image" src="https://github.com/user-attachments/assets/ea157daa-2439-442d-a83d-3650781a1dae" />
   
 </details>

 <details>
   <summary><code>🏴Tab completion on commands(Tự động hoàn thành lệnh bằng phím Tab)</code></summary>

 * Tính năng tự động hoàn thành bằng phím Tab không chỉ dành cho tập tin! Bạn cũng có thể tự động hoàn thành các lệnh. Cấp độ này có một lệnh bắt đầu bằng pwncollege, và nó sẽ cung cấp cho bạn cờ. Gõ pwncollegevà nhấn phím Tab để tự động hoàn thành lệnh!

* LƯU Ý: Bạn có thể sử dụng tính năng tự động hoàn thành cho bất kỳ lệnh nào, nhưng hãy cẩn thận: việc tự động hoàn thành một cách thiếu thận trọng mà không kiểm tra kỹ kết quả có thể gây ra hậu quả nghiêm trọng trong shell của bạn nếu bạn vô tình chạy nhầm lệnh!
* <img width="717" height="81" alt="image" src="https://github.com/user-attachments/assets/a20f1906-8d25-4c46-893a-9a8140769fde" />

 </details>
