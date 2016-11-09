# Flush

Flush ở đây hiểu đơn giản là dọn dẹp (quét sạch) những gì còn tồn đọng trong input/output stream.

## Trong C

Ví dụ như trường hợp sau:  
```C
#include <stdio.h>

void NhapMang(int* a, int* n);

int main(int argc, int* argv[])
{
  int* a = NULL;
  int n;
  NhapMang(&a, &n);
  if (a != NULL)
  {
  	free(a);
  }
  n = 0;
  return 0;
}
void NhapMang(int** a, int* n)
{
  *n = 0;
  int i;
  do
  {
    printf("Nhap so luong phan tu: ");
    i = scanf("%d", n);
  }
  while (*n > 0 && i == 1);
  
  *a = (int*)malloc(*n * sizeof(int));
  
  if (*a != NULL)
  {
    for (int j = 0; j < *n; j++)
    {
      printf("a[%d] = ", j);
      scanf("%d", (*a + j));
    }
  }
  else
  {
    *n = 0;
  }
}
```
Trong đoạn ví dụ trên, người sử dụng sẽ nhập số lượng phần tử, sau đó mảng được cấp phát đủ chứa n phần tử và gán địa chỉ vùng nhớ được cấp phát bằng hàm malloc vào trong con trỏ a (ngoài hàm main).

Tuy nhiên, để đảm bảo việc cấp phát suôn sẻ, thì số lượng phần tử phải lớn hơn 0, khi đó dùng vòng lặp do ... while (điều kiện) để yêu cầu người dùng nhập cho tới khi nào đúng thì thôi. Lưu ý, biến i dùng để lưu số lượng dữ liệu mà hàm scanf lấy được và sao chép chúng vào các tham số cung cấp cho hàm. Trong ví dụ trên, i bằng 1 tức n được gán dữ liệu thành công, nếu nhập sai, chẳng hạn nhập kí tự 'a', thì chắc chắn i sẽ bằng 0.

Nếu người dùng nhập sai, đáng lí ra thì ta sẽ thấy màn hình console phải tiếp tục xuất dòng "Nhap so luong phan tu: " và tất nhiên là phải đứng lại để người dùng nhập. Nhưng khi thử chạy thì ta thấy màn hình console "tràn ngập" với số lần lặp vô hạn dòng thông báo như trên. Lí do là khi dùng hàm scanf trong vòng lặp do .. while, nếu như nhập không đúng thì, scanf sẽ không lấy dữ liệu từ stream stdin, vậy thì dữ liệu nhập không đúng và lệnh "enter" từ phím Enter vẫn còn hiệu lực, sẽ lại gây nhập sai và lại lặp. Do đó chúng ta sẽ thấy việc lặp vô hạn là như vậy.

Để khắc phục điều trên thì chúng ta cần flush, dọn dẹp toàn bộ dữ liệu "rác" đó ra khỏi stdin. Bằng cách thêm dòng lệnh sau hàm scanf trong vòng lặp do ... while:  
fflush(stdin);  
Trong đó fflush là hàm dùng để flush stdin stream, mặc dù hàm với tham số đầu vào có kiểu con trỏ file FILE\*, nhưng stdin cũng là một thiết bị nhập tương tự như FILE\* với chế độ chỉ đọc, nên việc dùng chung là có thể và được chấp nhận trong C.

Khi thêm dòng lệnh trên vào, nếu "lỡ" như người dùng nhập sai thì chương trình sẽ không bị lặp lại vô tận những dòng thông báo nữa. Thay vào đó, dòng thông báo chỉ lặp một lần và người dùng có thể thoải mái nhập dữ liệu vào cho hợp lí để thoát khỏi vòng lặp.

## Trong C++

Việc nhập xuất thông thường trong console đều sử dụng các object như std::cin và std::cout. Ta cũng có thể kiểm tra việc nhập dữ liệu như thế nào và đảm bảo người dùng nhập đúng theo yêu cầu. Tuy nhiên, ta vẫn sẽ gặp phải trường hợp tương tự như trong C (tức ví dụ trên).

Đoạn code sau là một giải pháp:
```C++
if (std::cout.fail())
{
	std::cin.clear();
	std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
}
```
Nếu như sau khi nhập dữ liệu bằng std::cin vào một biến nào đó mà xảy ra lỗi thì, ta có thể dùng đoạn code trên để loại bỏ phần dữ liệu sai đó trong stream.
