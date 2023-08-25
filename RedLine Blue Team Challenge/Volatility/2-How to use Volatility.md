# Contents 

1. How to install Volatility
2. Identifying Malicious Processes
3. Identifying Malicious Network Connections
4. Identifying Injected Code

### 1. How to install Volatility

Có nhiều phiên bản của Volatility, nhưng phiên bản 3 là phiên bản mới nhất, nó sẽ tự động tìm ra hệ điều hành để hoạt động. 

Vì vậy chúng ta sẽ cài đặt Volatility 3 để dễ dàng sử dụng nhất.

- B1: Download phiên bản mới nhất của Volatility:
> git clone https://github.com/volatilityfoundation/volatility3.git
- B2: Vào folder Volatility và cài đặt các phụ thuộc cần thiết để Volatility chạy mà không gặp phải vấn đề gì
  
  ![image](https://github.com/shmily-2010/Cyber-Defenders/assets/112896213/bfcc8c79-5726-4df5-afbc-9258bba8e65f)

> pip3 install -r requirements.txt
- B3: Để kiểm tra xem tool đã được cài đặt chính xác, hãy dùng lệnh sau để kiểm tra:
> python3 vol.py -h

### 2. Identifying Malicious Processes

Điều đầu tiên nên làm khi nhận được một RAM dump từ một thiết bị có khả năng bị xâm phạm là nhìn xem có những process nào đang chạy khi RAM được captured.
Tìm kiếm những process đang chạy là một cách tốt để thử và xác định phần mềm độc hại nào đó có thể đang chạy trên thiết bị.

Có khá ít command có thể sử dụng để phân tích các process đang chạy, và đây là các lệnh được sử dụng:

- `pslist`
  - Lệnh này sẽ cho ra một lượng lớn dữ liệu
    > python3 vol.py -f <filename> windows.pslist

    ![image](https://github.com/shmily-2010/Cyber-Defenders/assets/112896213/70e327b7-2e68-47a0-814a-534b7f687878)

  - Lệnh này sẽ không cho phép sử dụng thêm lệnh khác trong terminal
    > python3 vol.py -f <filename> windows.pslist | less
    
    ![image](https://github.com/shmily-2010/Cyber-Defenders/assets/112896213/d5d5834d-b69f-4ed1-b1e8-d0bedbe4188a)

  - Lệnh này sẽ đưa đầu ra vào file output.txt
    > python3 vol.py -f <filename> windows.pslist > output.txt
  - Các key headers cần chú ý trong `pslist`:
    - **PID**: Process ID number
    - **PPID**: Parent process ID number
    - **Image file name**: Name of running process
    - **Offset**: Giá trị hex đại diện cho vị trí trong bộ nhớ mà quá trình đang chạy
    - **Create time**: Thời gian khởi chạy
    - **Exit time**: Thời gian kết thúc
  - Khi sử dụng command này, hãy chú ý vào tên process và xem có điều gì bất thường không. Bất cứ điều gì khiến bạn nghi ngờ,
  bạn đều có thể tra trên google để kiểm tra xem có hợp pháp hay cần chú ý thêm.

- `pstree`
  
  `pstree` sẽ giúp chúng ta biết được process nào sinh ra process khác, điều này sẽ giúp chúng ta dễ dàng phát hiện hoạt động của một số process đáng ngờ.
  (Vì có thể chúng ta sẽ thấy quy trình nào được khởi chạy `cmd.exe` hoặc `powershell.exe` và xem nó có hợp lệ hay không)

  **_Ví dụ:_** Kẻ tấn công thường đặt tên cho process độc hại theo các chương trình Windows hợp pháp như `svchost.exe`.
  Nó sẽ giúp ẩn tầm nhìn vì nó không quá đáng ngờ so với các chương trình windows khác.
  `pstree` sẽ giúp chúng ta phát hiện các process giả mạo. Các process windows luôn chạy từ các vị trí trên đĩa được thiết lập sẵn (`taskhostw` sẽ
  luôn chạy từ `%systemroot%\system32\taskhostw.exe` và parent process của nó là `scvhost.exe`. Nếu như `taskhostw` chạy từ vị trí khác hay với một parent
  process khác thì đó chắc chắn là điều mà bạn cần chú ý hơn)

  > python3 vol.py -f <tên tệp> windows.pstree
  
  ![image](https://github.com/shmily-2010/Cyber-Defenders/assets/112896213/aedf4eb9-62c9-4690-93a6-0ce5eb0f7fe3)

  Thứ tự của cột PID được sắp xếp theo một thứ tự và process con của nó, mỗi process con sẽ nhận thêm 1 * trước PID của nó.

### 3. Identifying Malicious Network Connections

Khi RAM dump được captured thì các network connections tại thời điểm đó cũng bị captured và lưu lại. Nó có ích cho người ứng phó sự cố vì kết nối mạng độc hại đều có thể được định danh qua source port, destination IP, destincation port và process liên quan. 

Để xem được các kết nối mạng liên kết với RAM dump sẽ phân tích ta sử dụng command:

> python3 vol.py -f <filename> windows.netscan

Những thông tin sau sẽ hiển thị sau khi sử dụng command

### 4. Identifying Injected Code

### [Reference](https://www.varonis.com/blog/how-to-use-volatility)
