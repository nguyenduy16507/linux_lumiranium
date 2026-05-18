# Pondering Paths

* Module này sẽ dạy cho bạn những điều cơ bản về các đường dẫn tệp (file paths) trong Linux!

  Hệ thống tệp (filesystem) Linux là một "cây". Nghĩa là, nó có một gốc (được viết là /). Gốc của hệ thống tệp là một thư mục (directory), và mọi thư mục đều có thể chứa các thư mục và tệp khác. Bạn tham chiếu đến các tệp và thư mục bằng đường dẫn (path) của chúng. Một đường dẫn đi từ gốc của hệ thống tệp bắt đầu bằng / (nghĩa là, gốc của hệ thống tệp), và mô tả tập hợp các thư mục mà bạn phải đi sâu xuống (descended into) để tìm thấy tệp. Mỗi phần của đường dẫn được phân định (phân cách) bằng một dấu / khác.


<details>
  <summary>🎥 <code>The File System</code></summary>

  * **File**

    Các máy tính lưu trữ dữ liệu trong các tệp.

  * **Directories(Thư mục)**

    Bạn không thể cứ để các tệp nằm rải rác một cách ngẫu nhiên được... Bạn sẽ chẳng bao giờ có thể tìm thấy bất cứ thứ gì!

    Các máy tính lưu trữ các tệp trong các thư mục bên trong hệ thống tệp. Mỗi thư mục có thể chứa nhiều tệp, giống như một cái hộp.

  * **Nesting Directories(Thư mục lồng nhau)** 

    Để tổ chức tốt hơn, các thư mục có thể được lưu trữ trong các thư mục khác!

  * **The "root" Directory(Thư mục"gốc")**

    "Luôn có một cái hộp lớn hơn"... cho đến khi không còn nữa.

    Trong Linux, các thư mục được lưu trữ trong các thư mục khác, đến lượt chúng lại được lưu trữ trong các thư mục khác nữa. Điều này không thể tiếp diễn mãi mãi. Cái hộp "ngoài cùng" là / (được gọi là thư mục "gốc").

  * **A "path"(Đường dẫn)**

    Con đường, chà, xuyên qua các thư mục lồng nhau này mà máy tính nên đi theo để tìm thấy tệp hoặc thư mục của bạn được gọi là một "đường dẫn" (path).

    For example:
    ```sh
    /UserData/YansData/Personal/Cooking/PumpkinPieRecipe
    ```
  
  * **The Typical File System Layout(Bố cục hệ thống tệp điển hình)**

    Linux có một bố cục hệ thống tệp được tiêu chuẩn hóa.
    |Tên thư mục|Mô tả|
    |:--|:--|
    |`/`|"Mỏ neo"(anchor) của hệ thống tệp. |
    |`/usr`|Tài nguyên Hệ thống Unix (Unix System Resource). Chứa tất cả các tệp hệ thống.|
    |`/usr/bin`|Các tệp thực thi (executable files) cho các chương trình được cài đặt trên máy tính.|
    |`/usr/lib`|Các thư viện dùng chung (share libararies) để sử dụng bởi các chương trình trên máy tính.|
    |`/usr/share`|Các tài nguyên của chương trình (các biểu tượng, tài nguyên đồ họa, ...)|
    |`/etc`|Cấu hình hệ thống.|
    |`/var`|Các nhật ký (logs), bộ nhớ đếm (caches), ...|
    |`/home`|Dữ liệu thuộc sở hữu của người dùng|
    |`/home/hacker`|Dữ liệu thuộc sở hữu của bạn trong cơ sở hạ tầng pwn.college.|
    |`/proc`|Dữ liệu tiến trình thời gian chạy(runtime process data).|
    |`/tmp`|Nơi lưu trữ dữ liệu tạm thời.|

  * **Navigating The File System(Điều hướng hệ thống tệp)**

    Mỗi tiến trình đều có một "thư mục làm việc hiện tại" (current working directory): thư mục mà nó đang xem xét vào thời điểm hiện tại. Bạn có thể xem nó bằng lệnh `pwd` (và nó thường hiển thị trong dấu nhắc lệnh của bạn) và thay đổi nó bằng lệnh `cd`.

    ```sh
    yans@asdf:~$ cd /
    yans@asdf:/$ cd home
    yans@asdf:/home$ pwd
    /home
    yans@asdf:/home$ cd hacker
    yans@asdf:/home/hacker$ pwd
    /home/hacker
    yans@asdf:/home/hacker$
    ```

    Bạn có thể liệt kê các tệp trong một thư mục bằng cách sử dụng lệnh `ls`. Nếu không có đối số nào, nó sẽ liệt kê các tệp trong thư mục hiện tại.

    ```sh
    yans@asdf:/$ ls
    bin boot challenge dev etc flag home lib lib32 lib64 libx32 media mnt nix opt proc root run sbin srv sys tmp usr var
    yans@asdf:/$ ls /home
    hacker
    yans@asdf:/$
    ```

  * **Specifying paths...(Chỉ định đường dẫn)**

    Có hai cách để chỉ định các đường dẫn:

    **Absolute Paths** (Các đường dẫn tuyệt đối) bắt đầu bằng `/`, chẳng hạn như `/usr`, `/home/yans/flags/TOPSECRET`, v.v.

    **Relative Paths** (Các đường dẫn tương đối) không bắt đầu bằng `/`, và có tính tương đối dựa trên thư mục làm việc hiện tại.

    ```sh
    yans@asdf ~ $ ls /home/yans/flags           <- Absolute path!
    TOPSECRET
    yans@asdf ~ $ pwd
    /home/yans
    yans@asdf ~ $ cat TOPSECRET                 <- Relative path!
    cat: TOPSECRET: No such file or directory
    yans@asdf ~ $ cd flags                      <- Relative path!
    yans@asdf ~/flags $ pwd
    /home/yans/flags
    yans@asdf ~/flags $ cat TOPSECRET           <- Relative path!
    pwn_college{1337}
    yans@asdf ~/flags $ █
    ```

  * **Closer look: Paths**

    Một "đường dẫn" chứa:
     * Một dấu `/` có thể có ở đầu (leading) để chỉ định rằng đường dẫn là tuyệt đối (bắt đầu tại gốc).
     * Các tên thư mục, theo sau là dấu `/` để tham chiếu đến các tài nguyên "bên trong" một thư mục.
     * Một dấu `.`, biểu thị "thư mục hiện tại".
     * Một dấu `..`, biểu thị "thư mục mà thư mục hiện tại nằm trong đó".
     * Một tên tệp ở cuối đường dẫn, tham chiếu đến một tệp có tên đó.
   
    ```sh
    yans@asdf /usr/bin $ cat /home/yans/flags/TOPSECRET
    pwn_college{1337}
    yans@asdf /usr/bin $ cat ../../home/yans/flags/TOPSECRET
    pwn_college{1337}
    yans@asdf /usr/bin $ cat ./../../usr/./lib/../bin/../../home/yans/flags/TOPSECRET
    pwn_college{1337}
    yans@asdf /usr/bin $ █
    ```    
</details>

<details>
  <summary>🏴 <code>The Root(Gốc rễ)</code></summary>

  * Được rồi, vậy là hệ thống tệp bắt đầu tại `/`. Dưới đó, có cả một mớ các thư mục khác, các tệp cấu hình, các chương trình, và, quan trọng nhất, các cờ (flags). Trong cấp độ này, chúng tôi đã thêm một chương trình ngay trong `/`, có tên là `pwn`, chương trình này sẽ cấp cho bạn cờ. Tất cả những gì bạn cần làm trong cấp độ này là gọi (invoke) chương trình này!

  * Bạn có thể gọi một chương trình bằng cách cung cấp đường dẫn của nó trên dòng lệnh. Trong trường hợp này, bạn sẽ đưa ra đường dẫn chính xác, bắt đầu từ `/`, do đó đường dẫn sẽ là `/pwn`. Kiểu đường dẫn này, kiểu bắt đầu bằng thư mục gốc, được gọi là một "đường dẫn tuyệt đối" (absolute path).

  * Hãy bắt đầu thử thách, khởi chạy một terminal, gọi chương trình `pwn` bằng cách sử dụng đường dẫn tuyệt đối của nó, và Chiếm lấy Cờ (Capture that Flag)! Chúc may mắn!

  * <img width="550" height="156" alt="image" src="https://github.com/user-attachments/assets/c742a9dc-43bc-4e67-a926-2a784aad027e" />

</details>

<details>
  <summary>🏴 <code>Program and absolute paths(Đường dẫn chương trình và đường dẫn tuyệt đối)</code></summary>

  * Hãy cùng khám phá một đường dẫn phức tạp hơn một chút! Ngoại trừ trong cấp độ trước, các thử thách trong pwn.college nằm trong thư mục `challenge` và đến lượt nó, thư mục `challenge` lại nằm ngay trong thư mục gốc (`/`). Do đó, đường dẫn đến thư mục thử thách là `/challenge`. Tên của chương trình thử thách trong cấp độ này là `run`, và nó nằm trong thư mục `/challenge`. Do đó, đường dẫn đến chương trình thử thách `run` là `/challenge/run`.

  * Thử thách này một lần nữa yêu cầu bạn thực thi nó bằng cách gọi (invoking) đường dẫn tuyệt đối của nó. Bạn sẽ muốn thực thi tệp `run` nằm trong thư mục `challenge`, mà thư mục này đến lượt nó lại nằm trong thư mục `/`. Nếu bạn gọi thử thách một cách chính xác, nó sẽ cấp cho bạn cờ (flag). Chúc may mắn!
  
  * <img width="504" height="124" alt="image" src="https://github.com/user-attachments/assets/bdaf5eaa-3003-48b9-acef-a1bfaefc39d1" />

</details>


<details>
  <summary>🏴 <code>Posotion thy self</code></code></summary>

  * Hệ thống tệp Linux có vô số thư mục với vô số tệp. Bạn có thể điều hướng qua lại giữa các thư mục bằng cách sử dụng lệnh cd (change directory - thay đổi thư mục) và truyền một đường dẫn cho nó như một đối số, giống như thế này:
    ```sh
    hacker@dojo:~$ cd /some/new/directory
    hacker@dojo:/some/new/directory$
    ```

  * Điều này ảnh hưởng đến "thư mục làm việc hiện tại" (current working directory) của tiến trình của bạn (trong trường hợp này là bash shell). Mỗi tiến trình đều có một thư mục mà hiện tại nó đang nằm trong đó (hanging out). Các lý do cho điều này sẽ trở nên rõ ràng ở phần sau của module.
  
  * Nói ngoài lề một chút (as an aside), bây giờ bạn đã có thể thấy ký tự ~ trong dấu nhắc lệnh là gì rồi đấy! Nó hiển thị đường dẫn hiện tại mà shell của bạn đang nằm ở đó.
  
  * Thử thách này sẽ yêu cầu bạn thực thi chương trình /challenge/run từ một đường dẫn cụ thể (mà nó sẽ cho bạn biết). Bạn sẽ cần phải cd đến thư mục đó trước khi chạy lại chương trình thử thách. Chúc may mắn!
  
  * <img width="583" height="243" alt="image" src="https://github.com/user-attachments/assets/ed68814c-aa0b-4f88-8b84-50865437917b" />
</details>


<details>
  <summary>🏴 <code>Postion elsewhere(Vị trí khác)</code></summary>

  * Same thing, but 5 times!

  * <img width="637" height="392" alt="image" src="https://github.com/user-attachments/assets/7ce29042-9daa-4830-b7c3-89388cc1a85b" />

</details>


<details>
  <summary>🏴 <code>implict relative paths, from /(Các đường dẫn tương đối ngầm định, từ/) </code></summary>

   * Bây giờ bạn đã quen thuộc với khái niệm tham chiếu đến các đường dẫn tuyệt đối (absolute paths) và thay đổi các thư mục. Nếu bạn đưa vào các đường dẫn tuyệt đối ở khắp mọi nơi, thì việc bạn đang ở thư mục nào thực sự không quan trọng, như bạn có lẽ đã nhận ra trong ba thử thách trước.

  * Tuy nhiên, thư mục làm việc hiện tại (current working directory) lại rất quan trọng đối với các đường dẫn tương đối (relative paths).

  * Một đường dẫn tương đối là bất kỳ đường dẫn nào không bắt đầu tại thư mục gốc (tức là, nó không bắt đầu bằng `/`).

  * Một đường dẫn tương đối được diễn giải **một cách tương đối** dựa trên **thư mục làm việc hiện tại** (cwd - current working directory) của bạn.

  * `cwd` của bạn là thư mục mà dấu nhắc lệnh (prompt) của bạn hiện đang nằm ở đó.

  * Điều này có nghĩa là cách bạn chỉ định một tệp cụ thể, phụ thuộc vào việc dấu nhắc terminal đang nằm ở đâu.

  * Hãy tưởng tượng chúng ta muốn truy cập một tệp nào đó nằm ở `/tmp/a/b/my_file`.

    * Nếu `cwd` của tôi là `/`, thì một đường dẫn tương đối đến tệp là `tmp/a/b/my_file`.

    * Nếu `cwd` của tôi là `/tmp`, thì một đường dẫn tương đối đến tệp là `a/b/my_file`.

    * Nếu `cwd` của tôi là `/tmp/a/b/c`, thì một đường dẫn tương đối đến tệp là `../my_file`. Ký tự `.. `tham chiếu đến thư mục cha (parent directory).

  * Hãy thử nó ở đây! Bạn sẽ cần chạy chương trình `/challenge/run` bằng cách sử dụng một đường dẫn tương đối trong khi có thư mục làm việc hiện tại là `/`. Đối với cấp độ này, tôi sẽ cho bạn một gợi ý. Đường dẫn tương đối của bạn bắt đầu bằng chữ cái `c` 😊

  * <img width="578" height="153" alt="image" src="https://github.com/user-attachments/assets/08fc6ae0-b38f-4748-a098-d5d4d39de90b" />

</details>

<details>
  <summary>🏴 <code>explicit relative paths, from /(Các đường dẫn tương đối rõ ràng,từ /)</code></summary>

  * Trước đây, đường dẫn tương đối của bạn là "trần trụi" (naked): nó chỉ định trực tiếp thư mục để đi sâu xuống từ thư mục hiện tại. Trong cấp độ này, chúng ta sẽ khám phá các đường dẫn tương đối tường minh (explicit) hơn.

  * Trong hầu hết các hệ điều hành, bao gồm cả Linux, mọi thư mục đều có hai mục ngầm định (implicit entries) mà bạn có thể tham chiếu trong các đường dẫn: `.` và `..`. Mục đầu tiên, `.`, tham chiếu ngay đến chính thư mục đó, vì vậy các đường dẫn tuyệt đối sau đây đều giống hệt nhau:
    ```sh
    /challenge
    /challenge.
    /challenge/ ./././././././././
    /./././challenge/././
    ```

  * Các đường dẫn tương đối sau đây cũng đều giống hệt nhau:
    ```sh
    challenge
    ./challenge
    ./././challenge
    challenge/.
    ```

  * Tất nhiên, nếu thư mục làm việc hiện tại của bạn là `/`, các đường dẫn tương đối ở trên sẽ tương đương với các đường dẫn tuyệt đối ở trên.
  
  * Thử thách này sẽ yêu cầu bạn sử dụng `.` trong các đường dẫn tương đối của mình. Hãy sẵn sàng!

  * <img width="598" height="161" alt="image" src="https://github.com/user-attachments/assets/4ac308cb-a0fc-4ab7-b883-75c731041471" />

</details>


<details>
  <summary>🏴 <code>implicit relative path(Đường dẫn tương đối ngầm định)</code></summary>

  * Trong cấp độ này, chúng ta sẽ thực hành việc tham chiếu đến các đường dẫn bằng cách sử dụng `.` nhiều hơn một chút. Thử thách này sẽ cần bạn chạy nó từ thư mục `/challenge`. Ở đây, mọi thứ trở nên hơi lắt léo một chút.

  * Linux chủ ý tránh việc tự động tìm kiếm trong thư mục hiện tại khi bạn cung cấp một đường dẫn "trần trụi". Hãy xem xét ví dụ sau:

    ```sh
    hacker@dojo:~$ cd /challenge
    hacker@dojo:/challenge$ run
    ```
    
  * Điều này sẽ **không gọi** (invoke) `/challenge/run`. Đây thực sự là một biện pháp an toàn: nếu Linux tìm kiếm các chương trình trong thư mục hiện tại mỗi khi bạn nhập một đường dẫn trần trụi, bạn có thể vô tình thực thi các chương trình trong thư mục hiện tại tình cờ có cùng tên với các tiện ích hệ thống cốt lõi! Kết quả là, các lệnh ở trên sẽ trả về lỗi sau:

    ```sh
    bash: run: command not found
    ```
    
  * Chúng ta sẽ khám phá các cơ chế đằng sau khái niệm này sau, nhưng trong thử thách này, chúng ta sẽ học cách sử dụng các đường dẫn tương đối một cách tường minh (explicitly) để khởi chạy `run` trong kịch bản này. Cách để làm điều này là bảo cho Linux biết một cách tường minh rằng bạn muốn thực thi một chương trình trong thư mục hiện tại, bằng cách sử dụng `.` giống như trong các cấp độ trước. Hãy thử ngay bây giờ!

  * <img width="527" height="174" alt="image" src="https://github.com/user-attachments/assets/92653473-c981-4e86-ba21-0b0718ef52c7" />

</details>

<details>
  <summary>🏴 <code>home sweet home</code></summary>

  * Mọi người dùng đều có một thư mục nhà (home directory), thường nằm dưới `/home` trong hệ thống tệp. Trong dojo, bạn là người dùng `hacker`, và thư mục nhà của bạn là `/home/hacker`. Thư mục nhà thường là nơi người dùng lưu trữ hầu hết các tệp cá nhân của họ. Trong quá trình bạn vượt qua pwn.college, đây là nơi bạn sẽ lưu trữ hầu hết các giải pháp (solutions) của mình.

  * Thông thường, phiên shell của bạn sẽ bắt đầu với thư mục nhà là thư mục làm việc hiện tại của bạn. Hãy xem xét dấu nhắc lệnh ban đầu:

    ```sh
    hacker@dojo:~$
    ```
    
  * Ký tự `~` trong dấu nhắc này là thư mục làm việc hiện tại, với `~` là dạng viết tắt của `/home/hacker`. Bash cung cấp và sử dụng cách viết tắt này bởi vì, xin nhắc lại, hầu hết thời gian của bạn sẽ được dành ở trong thư mục nhà của bạn. Do đó, bất cứ khi nào bash nhìn thấy `~` được cung cấp ở phần đầu của một đối số theo một cách nhất quán với một đường dẫn, nó sẽ mở rộng (expand) nó thành thư mục nhà của bạn. Hãy xem xét:

    ```sh
    hacker@dojo:~$ echo LOOK: ~
    LOOK: /home/hacker
    hacker@dojo:~$ cd /
    hacker@dojo:/$ cd ~
    hacker@dojo:~$ cd ~/asdf
    hacker@dojo:~/asdf$ cd ~/asdf
    hacker@dojo:~/asdf$ cd ~
    hacker@dojo:~$ cd /home/hacker/asdf
    hacker@dojo:~/asdf$
    ```
    
  * Lưu ý rằng phần mở rộng của `~` là một đường dẫn tuyệt đối, và chỉ có ký tự `~` đứng đầu mới được mở rộng. Điều này có nghĩa là, ví dụ, `~/~` sẽ được mở rộng thành `/home/hacker/~` thay vì `/home/hacker/home/hacker`.

  * Sự thật thú vị (Fun fact): lệnh `cd` sẽ sử dụng thư mục nhà của bạn làm đích đến mặc định:
    ```sh
    hacker@dojo:~$ cd /tmp
    hacker@dojo:/tmp$ cd
    hacker@dojo:~$
    ```

  * Bây giờ đến lượt bạn chơi! Trong thử thách này, `/challenge/run` sẽ ghi một bản sao của cờ vào bất kỳ tệp nào mà bạn chỉ định như một đối số trên dòng lệnh, với những ràng buộc sau:

    1. Đối số của bạn phải là một đường dẫn tuyệt đối.
    2. Đường dẫn phải nằm bên trong thư mục nhà của bạn.
    3. Trước khi được mở rộng, đối số của bạn phải có ba ký tự hoặc ít hơn.

  * Một lần nữa, bạn phải chỉ định đường dẫn của mình như một đối số cho `/challenge/run` giống như sau:
    ```sh
    hacker@dojo:~$ /challenge/run YOUR_PATH_HERE
    ```

  * <img width="980" height="133" alt="image" src="https://github.com/user-attachments/assets/f3db9e2c-140e-442e-bc28-fa846d1edf2e" />

</details>
