# Thao tác với tập tin trong C/C++

## 1. Trong C

### 1.a. Thao tác (các hàm) đóng mở tập tin
__Lưu ý:__ Phải thêm thư viện _stdio.h_ bằng chỉ thị _#include \<stdio.h\>_ khi muốn thao tác với tập tin ở trong C.

Tạo con trỏ FILE (tức mở tập tin):  
__FILE* fp = fopen("\<path\>", "\<mode\>");__  
_\<mode\>_: r, w, a (read, write, append) & t hoặc b (text hoặc binary).  
_\<path\>_: Đường dẫn tới tập tin, có thể là đường dẫn tuyệt đối hoặc đường dẫn tương đối.  

__Chi tiết:__  
Hàm __FILE* fopen(char* filename, char* mode)__: Mở tập tin với tên chứa trong trong tham số _filename_ và cách thức mở trong tham số _mode_.  
Tham số _mode_ nhận các giá trị:  
\+ _"rt"_: Mở tập tin văn bản để đọc.  
\+ _"wt"_: Mở tập tin văn bản để ghi, tập tin nếu đang tồn tại sẽ bị xóa.  
\+ _"at"_: Mở tập tin văn bản để ghi, nhưng ghi vào cuối file, tức dữ liệu văn bản có sẵn vẫn được giữ nguyên, chỉ thêm dữ liệu vào cuối file văn bản đó.  
\+ _"rb"_, _"wb"_, _"at"_: Tương tự như trên nhưng dùng cho tập tin nhị phân.  
\* Nếu muốn vừa đọc vừa ghi thì bổ sung dấu _'+'_, ví dụ _"r+w"_.

Hàm sẽ trả về con trỏ _FILE_ dùng để thao tác trên tập tin nếu mở thành công tập tin đó. Ngược lại, nếu không mở được tập tin, hàm sẽ trả về con trỏ _NULL_.  

Tập tin văn bản cũng có thể coi như tập tin nhị phân, tất cả các tập tin lưu trên máy tính đều có coi là tập tin nhị phân. Tập tin văn bản ở đây coi như là một trường hợp đặc biệt của tập tin nhị phân vì tập tin văn bản quy ước biểu diễn các byte để biểu diễn kí tự.

Sau khi mở tập tin, thao tác xong, nên đóng tập tin đã mở bằng hàm: __fclose(FILE* fp)__, trong đó _fp_ là con trỏ _FILE_ được tạo ra bởi hàm _fopen_ trước đó.

### 1.b. Các hàm thao tác với tập tin văn bản  
__int fscanf(FILE* stream, const char* format, ...)__  
__int fprintf(FILE* stream, const char* format, ...)__  
Dùng để đọc và ghi dữ liệu vào tập tin văn bản tương tự như cách hoạt động của các hàm _scanf_ và _printf_ nhưng thay đổi thiết bị nhập xuất mặc định từ bàn phím và màn hình thành _FILE*_.
Đối với hàm _fscanf_, giá trị trả về là số lượng mẫu dữ liệu đọc được thành công (truyền thành công). Nếu xảy ra lỗi khi mà chưa đọc được dữ liệu nào, giá trị âm sẽ được trả về.
Đối với hàm _fprintf_, giá trị trả về là số lượng kí tự được ghi. Nếu việc ghi xảy ra lỗi, giá trị âm sẽ được trả về.  

__char* fgets(char* str, int num, FILE* stream)__  
Dùng để đọc các kí tự trong stream và chứa vào trong _str_ cho tới khi đủ _(num - 1)_ kí tự hoặc gặp kí tự xuống dòng _newline_, _end-of-file_ _(EOF)_.  
__Lưu ý:__  
\+ _str_ phải được cấp phát hoặc phải được khởi tạo trước.
\+ Chỉ đọc _(num - 1)_ kí tự bởi vì kèm thêm kí tự ngắt chuỗi _'\0'_-(terminating null character) (khi đó chuỗi sẽ có _num_ kí tự), kí tự này được tự động thêm vào. Đây cũng là lí do _num_ chính là kích thước của chuỗi _str_ (không phải độ dài vì độ dài = kích thước - kí tự _'\0'_ (kích thước chỉ >= 1)).  

__int fputs(const char* str, FILE* stream)__  
Dùng để ghi chuỗi _str_ vào _stream_. Hàm sẽ ghi toàn bộ các kí từ từ chuỗi _str_ cho đến khi gặp kí tự '\0'.  

__Lưu ý:__  
Các hàm như _fgets_ và _fputs_ nếu thực hiện thành công tác vụ mà hàm được cài đặt, sẽ trả về giá trị không âm. Nếu có lỗi xảy ra, sẽ trả về giá trị _EOF_ (-1).

__int fgetc(FILE* stream)__  
Dùng để lấy một kí tự từ _stream_. Hàm sẽ trả về số nguyên biểu diễn kí tự đó trong bảng mã.  
Khi xảy ra lỗi khi đọc hoặc gặp kí tự _EOF_, hàm sẽ trả về _EOF_.  

__int fputs(char character, FILE* stream)__  
Dùng để ghi một kí tự vào stream.  
Nếu việc ghi không thành công, trả về _EOF_.  

### 1.c. Các hàm thao tác với tập tin nhị phân

## 2. Trong C++:
Trong C++ có các lớp để xử lí tập tin.  

Trong bài viết:  
\+ string là chuỗi (trong tiếng Anh).  
\+ stream có thể hiểu là "dòng" dữ liệu (các byte) "chảy".  
\+ Để tìm hiểu thêm, có thể vào trang web: [www.cplusplus.com](http://www.cplusplus.com/ "www.cplusplus.com"), đây là nơi chứa thông tin khá chi tiết về ngôn ngữ C/C++.  
