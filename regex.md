
## Ký tự thể hiện vị trí  ^ và $

## Ký hiệu phân nhóm ()
* a(bc) trong cặp dấu ngoặc là một group, giá trị trong group sẽ được capture lại
* a(?:bc)* giá trị trong group sẽ không được capture lại
* a(?<foo>bc) đặt tên cho group, mặc địng group sẽ có chỉ số là group[0], group[1], trường hợp này group sẽ là group[foo]
  
## Some example
* "**.+?**" matches any character (except for line terminators) (Line terminators are \n)
