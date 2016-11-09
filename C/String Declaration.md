```C
void main()
{
  char a[]; // Không khai báo số lượng phần tử sẽ gây lỗi.
  char a[] = "abcdefgh"; // Số lượng phần tử được trình biên dịch tự động thêm vào.
  char a[10]; a[] = "abcdefgh"; /* hoặc */ a = "abcdefgh" // đều không hợp lệ vì cách này chỉ áp dụng cho việc khai báo.
  char a[3] = "abcdefgh" // Không hợp lệ vì số lượng phần tử của mảng không đủ chứa "abcdefgh" tức 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', '\0'.

  char* a;
  a = "abcdefgh";
  *(a + 0) = 'a';
  // Không nên sử dụng cách trên bởi vì "abcdefgh" được khởi tạo trong vùng nhớ read-only (chỉ đọc),
  // con trỏ a trỏ 'a' trong "abcdefgh" nên thay đổi giá trị qua con trỏ a sẽ không hợp lệ vì không thể sửa được vùng nhớ read-only.
  
  char a[] = "abcdefgh";
  a[0] = 'z';
  // Bởi vì "abcdefgh" được sao chép vào vùng nhớ stack tức vào a[] nên có thể thay đổi được từng phần tử của a.
}
```
