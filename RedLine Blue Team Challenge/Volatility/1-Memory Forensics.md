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

1. Volatility

### [References](https://www.varonis.com/blog/memory-forensics)
