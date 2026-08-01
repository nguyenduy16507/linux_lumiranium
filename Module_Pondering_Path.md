# Pondering Path (Con đường suy ngẫm)
* Cho đến nay, bạn đã thực thi các lệnh theo nhiều cách khác nhau:

 - Thông qua một con đường tuyệt đối (ví dụ, `/challenge/run`).
 - Thông qua một đường dẫn tương đối (ví dụ, `./run`).
 - Thông qua tên lệnh đơn giản (ví dụ: `ls`).
* Hai trường hợp đầu tiên, trường hợp đường dẫn tuyệt đối và đường dẫn tương đối, khá đơn giản: `run`tệp nằm trong `/challenge`thư mục và cả hai trường hợp đều tham chiếu đến thư mục đó (tất nhiên, với điều kiện đường dẫn tương đối được gọi với thư mục làm việc hiện tại là `/challenge`). Nhưng còn trường hợp cuối cùng thì sao? Chương trình nằm ở đâu `ls`? Làm thế nào mà shell biết tìm kiếm nó ở đó?

* Trong mô-đun này, chúng ta sẽ vén màn bí mật và trả lời câu hỏi này! Hãy theo dõi nhé
  
<details>
  <summary><code>📒Resources(Tài nguyên)</code></summary>

 * https://www.linfo.org/path_env_var.html

</details>
<details>
  <summary><code>🏴The PATH Variable(Biến PATH)</code></summary>

 * Hóa ra câu trả lời cho câu hỏi "Làm thế nào mà shell tìm thấy `ls`?" khá đơn giản. Có một biến shell đặc biệt, được gọi là `PATH`, lưu trữ một loạt các đường dẫn thư mục mà shell sẽ tìm kiếm các chương trình tương ứng với các lệnh. Nếu bạn xóa trắng biến này, mọi thứ sẽ trở nên tồi tệ:
```sh
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ PATH=""
hacker@dojo:~$ ls
bash: ls: No such file or directory
hacker@dojo:~$
```
* Nếu không có biến môi trường PATH, bash không thể tìm thấy `ls`lệnh.

* Ở cấp độ này, bạn sẽ làm gián đoạn hoạt động của `/challenge/run`chương trình. Chương trình này sẽ XÓA tập tin cờ bằng `rm`lệnh. Tuy nhiên, nếu nó không tìm thấy `rm`lệnh, cờ sẽ không bị xóa và thử thách sẽ trao nó cho bạn! Vì vậy, bạn phải làm cho nó `/challenge/run`cũng không thể tìm thấy `rm`lệnh!

Hãy nhớ: nếu bạn không thành công và lá cờ bị xóa, bạn sẽ cần phải bắt đầu lại thử thách để thử lại! 
</details>
<details>
  <summary><code>🏴Setting PATH(Thiết lập PATH)</code></summary>

* Được rồi, mọi thứ sẽ hỏng khi bạn quên hết mọi thứ PATH. Nhưng còn việc tận dụng thời gian đó thì sao PATH?

* Hãy cùng tìm hiểu xem, ví dụ, cách chúng ta thêm một thư mục chương trình mới vào kho lệnh của mình. Hãy nhớ rằng kho lệnh này PATHlưu trữ một danh sách các thư mục để tìm các lệnh và đối với các lệnh ở những vị trí không chuẩn, chúng ta thường phải thực thi chúng thông qua đường dẫn của chúng:
```sh
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ goodscript
bash: goodscript: command not found
hacker@dojo:~$ /home/hacker/scripts/goodscript
YEAH! This is the best script!
hacker@dojo:~$
```
* Nếu bạn lưu trữ các tập lệnh hữu ích mà bạn muốn có thể khởi chạy chỉ bằng tên tệp, điều này khá phiền phức. Tuy nhiên, bằng cách thêm thư mục vào hoặc thay thế các thư mục trong danh sách này, bạn có thể cho phép khởi chạy các chương trình này chỉ bằng tên tệp của chúng! Ví dụ:
```sh
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```
* Hãy cùng thực hành. Ở cấp độ này, lệnh /challenge/runsẽ được chạy wintrực tiếp bằng tên của nó, nhưng lệnh này nằm trong /challenge/more_commands/thư mục, mà ban đầu không có trong biến môi trường PATH. Chỉ cần lệnh đó winlà đủ, vì vậy bạn chỉ cần ghi đè lên bằng thư mục đó. Chúc may mắn!/challenge/runPATH
</details>
<details>
  <summary><code>🏴Finding Commands(Tìm lệnh)</code></summary>

 * Khi bạn gõ tên một lệnh, một thứ gì đó bên trong một trong nhiều thư mục được liệt kê trong $PATHbiến của bạn sẽ thực sự được thực thi (tất nhiên, trừ khi lệnh đó là lệnh tích hợp sẵn!). Nhưng chính xác là tệp nào ? Bạn có thể tìm ra điều đó bằng whichlệnh có tên gọi rất phù hợp:
```sh
hacker@dojo:~$ which cat
/bin/cat
hacker@dojo:~$ /bin/cat /flag
YEAH
hacker@dojo:~$
```
* Tương tự như cách mà trình thông dịch lệnh (shell) thực hiện khi tìm kiếm các lệnh, whichchương trình sẽ duyệt qua từng thư mục theo $PATHthứ tự và in ra tệp đầu tiên mà nó tìm thấy có tên trùng khớp với đối số bạn đã truyền vào.

* Trong thử thách này, chúng tôi đã thêm một winlệnh vào đâu đó trong tệp của bạn $PATH, nhưng lệnh đó sẽ không cung cấp cho bạn cờ. Thay vào đó, cờ nằm ​​trong cùng thư mục với một flagtệp mà chúng tôi đã cấp quyền đọc cho bạn! Bạn phải tìm win(bằng whichlệnh ) và catcờ trong thư mục đó! 
</details>
<details>
  <summary><code>🏴Adding Commands(Thêm lệnh)</code></summary>

 * Hãy nhớ lại ví dụ từ cấp độ trước:
```SH
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```
* Điều chúng ta thấy ở đây, dĩ nhiên, là việc hackerlàm cho lớp vỏ trở nên hữu ích hơn bằng cách đưa các lệnh riêng của mình vào. Theo thời gian, bạn có thể tích lũy được những công cụ thanh lịch của riêng mình. Hãy bắt đầu với win!

* Trước đây, winlệnh được /challenge/runthực thi được lưu trữ trong /challenge/more_commands. Lần này, winkhông tồn tại! Hãy nhớ lại cấp độ cuối cùng của Chuỗi lệnh , và tạo một tập lệnh shell có tên win, thêm vị trí của nó vào PATH, và cho phép /challenge/runtìm thấy nó!

* Gợi ý: /challenge/run chạy với quyền rootvà sẽ gọi win. Do đó, winbạn chỉ cần dùng lệnh `cat` để xem nội dung tệp cờ. Một lần nữa, winlệnh là thứ duy nhất/challenge/run cần thiết, vì vậy bạn chỉ cần ghi đè PATHbằng thư mục đó. Nhưng hãy nhớ, nếu bạn làm vậy, winlệnh của bạn sẽ không thể tìm thấy cat.

* Bạn có ba lựa chọn để tránh điều đó:

- Xác định vị trí catcủa chương trình trên hệ thống tập tin. Nó phải nằm trong một thư mục được lưu trữ trong PATHbiến, vì vậy bạn có thể in biến đó ra (tham khảo phần Biến Shell để nhớ cách làm!), và duyệt qua các thư mục con trong đó (nhớ rằng các mục khác nhau được phân tách bằng dấu ngoặc đơn :), tìm thư mục nào chứa catchương trình và gọi chương trình catbằng đường dẫn tuyệt đối của nó.
- Thiết lập một PATHmục chứa các thư mục cũ cộng thêm một mục mới cho bất kỳ vị trí nào bạn tạo win.
- Hãy sử dụng read(lưu ý, hãy tham khảo lại phần Biến Shell ) để đọc /flag. Vì readđây là chức năng tích hợp sẵn của bashnên nó không bị ảnh hưởng bởi PATHcác thủ thuật khác.
Nào, đi đi win! 
</details>
<details>
  <summary><code>🏴Hijacking Commands(Lệnh chiếm quyền điều khiển)</code></summary>

  * Với kiến ​​thức đã có, giờ đây bạn có thể thực hiện một vài trò nghịch ngợm. Thử thách này gần giống với thử thách đầu tiên trong mô-đun này. Một lần nữa, thử thách này sẽ xóa cờ bằng rmlệnh. Nhưng không giống như trước, nó sẽ không in bất cứ thứ gì ra cho bạn.

* Bạn có thể giải quyết vấn đề này như thế nào? Bạn biết rằng nó rmđược tìm kiếm trong các thư mục được liệt kê trong PATHbiến. Bạn có kinh nghiệm tạo winlệnh này khi thử thách trước đó cần đến nó. Bạn còn có thể tạo ra gì khác nữa?
```sh
echo "/bin/cat /flag" > /home/hacker/rm
chmod +x /home/hacker/rm
export PATH=/home/hacker:$PATH
/challenge/run
```
- `/challenge/run` chạy với quyền root và chuẩn bị thực hiện hành vi 'xóa flag' bằng cách gọi lệnh `rm`.Do bạn dã chèn `/home/hacker` lên đầu `$PATH`, hệ thống tra cứu `$PATH` và tìm thấy file `rm` của bạn trước. Thay vì xóa flag, hệ thống lại thực thi script `rm` của bạn, chạy lệnh `/bin/cat /flag` với quyền root và xuất ra cờ .
</details>

**Lưu ý** : 
1.Tìm kiếm vị trí lệnh ẩn bằng `which`
 - Khi bạn gõ 1 lệnh, trình thông dịch lệnh(shell) sẽ được thực thi một tệp nằm bên trong một trong nhiều thư mục được liêt kê trong biến `$PATH`. Lệnh `which` hoạt động bằng cách duyệt qua từng mục theo thứ tự trong `$PATH` và in ra tệp đầu tiên trùng khớp với đối số bạn truyền vào.
 - Thử thách này giấu 1 lệnh `win` ở đâu đó trong `$PATH`, nhưng việc chạy nó không cung cấp cờ. Tệp `flag` được cấp quyền đọc và nằm cùng thư mục với lệnh `win`. Bạn cần dùng lệnh `which` để tìm vị trí của win , sau đó dùng cat để đọc cờ trong thư mục đó .
2. Xóa biến `PATH` để vô hiệu hóa lệnh hệ thống
 - Biến shell `PATH` lưu trữ một loạt các chương trình dẫn thư mục mà shell dùng để tìm kiếm chương trình tương ứng với các lệnh. Nếu bạn xóa trắng biến này(VD: `PATH=""`), bash sẽ không thể tìm thấy các lệnh như `ls`.
3. Ghi đè `PATH` để thực thi lệnh ở vị trí không chuẩn
 - Bằng cách thêm hoặc thay thế các thư mục trong danh sách của `PATH`, bạn có thể khởi chay các tệp lệnh hoặc chương trình trên tệp thay vì phải gõ đường dẫn đầy đủ của chúng.
 - VD: Thử thách yêu cầu `/challenge/run` chạy lệnh `win` trực tiếp bằng tên của nó. Tuy nhiên, lệnh `win` lại nằm trong thư mục `/challenge/more_commands/` vốn ban đầu nó không có trong biến môi trường `PATH`.Giải pháp ta chỉ cần ghi đè lên `PATH` bằng thư mục đó là được.
4. Tạo lệnh tùy chỉnh và xử lý bẫy mất `PATH`
 - Bạn có thể tự tạo 1 tệp lệnh Shell(vd tên là win), thêm vị trí của nó cào `PATH` và cho phép chương trình khác như `/challenge/run` tìm thấy nó. Lệnh `/challenge/run` chạy với quyền root và sẽ gọi `win`, do đó bạn chỉ cần lệnh `win` chứa lệnh `cat` để xem tệp cờ. Neus bạn ghi đè `PATH` hoàn toàn bằng thư mục chứa `win`, lệnh `win` của bạn sẽ không thể tìm thấy lệnh `cat` của hệ thống.
