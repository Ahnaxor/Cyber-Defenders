# Contents 

1. Memory Forensics Overview
2. Volatile Data _(explain what is volatility data and why is it relevent to memory forensics)_
3. Memory Dump / RAM Dump
4. Benifits of memory analysis
5. Tools for memory analysis

### 1. Memory Forensics Overview

Memory forensics là quá trình ghi lại bộ nhớ đang chạy của thiết bị rồi phân tích và lưu lại bằng chứng của các phần mềm độc hại. Khác với hard-disk forensics (khôi phục và phân tích những file hệ thống của thiết bị hoặc tất cả các file trong đĩa), memory forensics tập trung vào phân tích các chương trình đang thực thi trong thiết bị khi mà memory dump được lưu lại.

Khi mà một ứng dụng được mở/khởi động, nó sẽ cần được RAM phân bổ bộ nhớ để ứng dụng có thể chạy, vì vậy chúng ta cần một thanh RAM lớn hơn để thiết bị thực thi nhanh hơn khi có nhiều ứng dụng được mở.

### 2. Volatile Data 

Volatile Data là dữ liệu sẽ mất đi nếu như chúng ta tắt máy.

Đây là một cái gì đó khiến người dùng cần phải lo lắng, vì khi đối mặt với một thiết bị tổn hại thì chúng ta thường ngay lập tức tắt máy để ngăn chặn mối nguy hại. Tuy nhiên, các phần mềm độc hại đang hoạt động sẽ được lưu lại dưới dạng volatile data trong memory, vì vậy mọi kết nối hay các chương trình đang thực thi hay phần mềm độc hại sẽ không được ghi lại. Volatile data không được ghi và bị thay đổi ngay lập tức, có nghĩa là những bằng chứng giá trị đều đã bị hủy.

Network containment (cô lập thiết bị khỏi phần còn lại của kết nối) là một phương pháp ưu tiên sử dụng khi thiết bị bị hư hại. Nó sẽ chứa phần hư hại một cách an toàn mà không làm mất những bằng chứng quan trọng/ phá hủy volitle data trong memory.

### 3. Memory Dump

Memory dump hay RAM dump là hình ảnh chụp nhanh của bộ nhớ cho memory analysis. Khi RAM được chụp/capture lại, nó sẽ chứa tất cả dữ liệu liên quan đến chương trình đang được thực thi tại thời điểm bị chụp. 

### 4. Benifits of memory analysis 

Đối mặt với việc xử lý sự cố không hề dễ và nó cần đến các công cụ chuyên dụng. 

Để có thể ứng phó với các sự cố an ninh mạng, thì cần có [incident response plan](https://www.varonis.com/blog/incident-response-plan) và [specialist tool](https://www.varonis.com/blog/malware-analysis-tools).

Việc sử dụng memory analysis có thể giúp bạn chuyển dữ liệu nhanh và ít hơn.

### 5. Tools for memory analysis

Dưới đây là một số tool miễn phí và được sử dụng cho memory analysis!

1. [Volatility](https://www.volatilityfoundation.org/)
   
   Volatility có sẵn cho cả Windows và Linux.
   
   Nó sẽ cho bạn thông tin hữu ích như chương trình nào đang được chạy trên hệ thống, kết nối mạng và chương trình chứa mã độc.   Nó cũng hỗ trợ phân tích memory dump từ thiết bị Unix và một loạt các plugin đã được thiết kế bởi cộng đồng forensics.

   Nên sử dụng Vol3 vì nó đã thiết lập sẵn cấu hình.
   
2. [Rekall](http://www.rekall-forensic.com/)
   
   Tương tự với Volatility.
   
3. [RedLine](https://fireeye.market/)

   Nó chỉ sử dụng cho Windows, là một công cụ GUI.

**_What Should I Look For In a Memory Dump?_**. 

Có một câu nói là 'Malware can hide but it must run'. Các phần mềm độc hại sẽ cố gắng bị ẩn đi tại nơi mà người dùng ít sử dụng, tuy nhiên khi nó chạy thì vẫn là một running process trong thiết bị. Vì vậy, cách đơn giản nhất là nhìn tất cả các running process trên một thiết bị.

Hãy xem tất cả các tên process mà không được chấp nhận trong process listing, khi mà bạn google thì nó có trả về kết quả nào không?

Hoặc bạn cũng có thể xem các process trees, xem xem nó được tạo ở đâu, đâu là chương trình cha của nó, nó có phải là hành động mà bạn muốn thực hiện không?

Một lời khuyên tốt nữa là nhìn vào những cái tên windows uy tín như 'svchost.exe', windows system process luôn được cài đặt parent process và run locations. Nếu như bạn thấy một chương trình chạy từ một vị trí bất thường thì nó có thể là một điều tra giá trị. 

Các malicious process có thể được nhận dạng trong [hunt evil](https://sansgear.com/product/dfir-hunt-evil-poster/).

Một cách khác là kiểm tra network connections, nó có phải là các unusual ports được kết nối không? Đặc biệt chú ý vào 'poker hand' - các cổng mà người tấn công cài đặt port như là '4444' hay '1234'.

### [References](https://www.varonis.com/blog/memory-forensics)
