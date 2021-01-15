
## Ký tự thể hiện vị trí  ^ và $

## Ký hiệu phân nhóm ()
* a(bc) trong cặp dấu ngoặc là một group, giá trị trong group sẽ được capture lại
* a(?:bc)* giá trị trong group sẽ không được capture lại
* a(?<foo>bc) đặt tên cho group, mặc địng group sẽ có chỉ số là group[0], group[1], trường hợp này group sẽ là group[foo]
  
## Kí hiệu chỉ phạm vi []
* [abc] khớp với 1 ký tự a hoặc b hoặc c -> tương tự cách dùng a|b|c
* [a-c] tác dụng như trên
* [a-fA-F0-9] khớp với 1 ký tự nằm trong khoảng từ a -> z hoặc A -> Z hoặc 0 -> 9(đây chính là đoạn regex để bắt ký tự trong hệ HEX)
* [0-9]% khớp với 1 ký tự từ 0 ->9 và theo sau nó là ký tự %
* [^a-zA-Z] khớp với ký tự không nằm nằm trong a -> z và A -> Z
## Ranh giới — \b và \B
* \babc\b => thực hiện tìm kiếm toàn bộ từ, tức là chỉ tìm từ nào chính xác là abc

\blà một điểm neo giống như ^ hoặc $, nhưng neo cả 2 đầu, đi kèm với nó là phủ định \B, ví dụ như:

* \Babc\B sẽ khớp với các chuỗi mà có kí tự 'abc' được bao quanh bởi các kí tự khác (ví dụ: 'gabcy')

## Phía trước và phía sau — (?=) và (?<=)
* d(?=r) => khớp với kí tự d chỉ khi phía sau nó là kí tự r, nhưng r không phải 1 phần của chuỗi regex (ví dụ: drone)
* (?<=r)d => tương tự trên, nhưng d phải đi ngay sau r (ví dụ: third)
Tương tự ta cũng có phủ định của nó là (?!) và (?<!)

* d(?!r) => khớp với kí tự d nếu phía sau nó không phải kí tự r, r cũng không phải 1 phần của chuỗi regex
* (?<!r)d => tương tự trên, nhưng d không được đi sau r

## Some example
* "**.+?**" matches any character (except for line terminators) (Line terminators are \n)
* "**\w+**" matches any word character (equal to [a-zA-Z0-9_])
* "string1(.\*)string2" match word between string1 and string2
* "string1(.\*?)string2" match word between string 1 and string2 gan string 1 nhat (ex: \\/\\*(.\*?)\\*\\/gm: match bteen \\* and \*/
## Kí tự (kí hiệu, cờ)	Ý nghĩa
 * \	

Một dấu gạch chéo ngược sẽ biến một kí tự thường liền kế phía sau thành một kí tự đặc biệt, tức là nó không được sử dụng để tìm kiếm thông thường nữa. Ví dụ,  trường hợp kí tự 'b' không có dấu gạch chéo ngược này sẽ được khớp với các kí tự 'b' in thường, nhưng khi nó có thêm dấu gạch chéo ngược, '\b' thì nó sẽ không khớp với bất kì kí tự nào nữa, lúc này nó trở thành kí tự đặc biệt. Xem thêm phần word boundary character để biết thêm chi tiết.

Tuy nhiên nếu đứng trước một kí tự đặc biệt thì nó sẽ biến kí tự này thành một kí tự thường, tức là bạn có thể tìm kiếm kí tự đặc biệt này trong xâu chuỗi của bạn như các kí tự thường khác. Ví dụ, mẫu /a*/ có '*' là kí tự đặc biệt và mẫu này sẽ bị phụ thuộc vào kí tự này, nên được hiểu là sẽ tìm khớp  với 0 hoặc nhiều kí tự a. Nhưng, với mẫu /a\*/ thì kí tự '*' lúc này được hiểu là kí tự thường nên mẫu này sẽ tìm kiếm xâu con là 'a*'.

Đừng quên \ cũng là một kí tự đặc biệt, khi cần so khớp chính nó ta cũng phải đánh dấu nó là kí tự đặc biệt bằng cách đặt \ ở trước (\\).

* ^	
Khớp các kí tự đứng đầu một chuỗi. Nếu có nhiều cờ này thì nó còn khớp được cả các kí tự đứng đầu của mỗi dòng (sau kí tự xuống dòng).

Ví dụ, /^A/ sẽ không khớp được với 'A' trong "an A" vì 'A' lúc này không đứng đầu chuỗi, nhưng nó sẽ khớp "An E" vì lúc này 'A' đã đứng đầu chuỗi.

Ý nghĩa của '^' sẽ thay đổi khi nó xuất hiện như một kí tự đầu tiên trong một lớp kí tự, xem phần complemented character sets để biết thêm chi tiết.

* $	
So khớp ở cuối chuỗi. Nếu gắn cờ multiline (đa dòng), nó sẽ khớp ngay trước kí tự xuống dòng.

Ví dụ, /t$/ không khớp với 't' trong chuỗi "eater" nhưng lại khớp trong chuỗi "eat".

* /*	
Cho phép kí tự trước nó lặp lại 0 lần hoặc nhiều lần. Tương đương với cách viết {0,}.

Ví dụ, /bo*/ khớp với 'boooo' trong chuỗi "A ghost booooed" nhưng không khớp trong chuỗi "A birth warbled".

* +	
Cho phép kí tự trước nó lặp lại 1 lần hoặc nhiều lần. Tương đương với cách viết {1,}.

Ví dụ, /a+/ khớp với 'a' trong chuỗi "candy" và khớp với tất cả kí tự a liền nhau trong chuỗi "caaaaaaandy".

* ?	
Cho phép kí tự trước nó lặp lại 0 lần hoặc 1 lần duy nhất. Tương đương với cách viết {0,1}.

Ví dụ, /e?le?/ khớp với 'el' trong chuỗi "angel" và 'le' trong chuỗi "angle" hay 'l' trong "oslo".

Nếu sử dụng kí tự này ngay sau bất kì kí tự định lượng nào trong số *,+,? hay {}, đều làm bộ định lượng "chán ăn" (dừng so khớp sau ngay khi tìm được kí tự phù hợp), trái ngược với đức tính "tham lam" vốn sẵn của chúng (khớp tất cả kí tự chúng tìm thấy). Ví dụ, áp dụng biểu mẫu /\d+/ cho "123abc" ta được "123". Nhưng áp /\d+?/ cho chính chuỗi trên ta chỉ nhận được kết quả là "1".

Bạn có thể đọc thêm trong mục x(?=y) và x(?!y) của bảng này.

* .	
Dấu . khớp với bất kì kí tự đơn nào ngoại trừ kí tự xuống dòng.

Ví dụ, /.n/ khớp với 'an' và 'on' trong chuỗi "no, an apple is on the tree", nhưng không khớp với 'no'.

* (x)	
Khớp 'x' và nhớ kết quả so khớp này, như ví dụ ở dưới. Các dấu ngoặc tròn được gọi là các dấu ngoặc có nhớ.

Biểu mẫu /(foo) (bar) \1 \2/ khớp với 'foo' và 'bar' trong chuỗi "foo bar foo bar". \1 và \2 trong mẫu khớp với 2 từ cuối.

Chú ý rằng \1, \2, \n được sử dụng để so khớp các phần trong regex, nó đại diện cho nhóm so khớp đằng trước. Ví dụ: /(foo) (bar) \1 \2/ tương đương với biểu thức /(foo) (bar) foo bar/. 

Cú pháp $1, $2, $n còn được sử dụng trong việc thay thế các phần của một regex. Ví dụ: 'bar foo'.replace(/(...) (...)/, '$2 $1') sẽ đảo vị trí 2 từ 'bar' và 'foo' cho nhau.

* (?:x)	
Khớp 'x' nhưng không nhớ kết quả so khớp. Những dấu ngoặc tròn được gọi là những dấu ngoặc không nhớ, nó cho phép bạn định nghĩa những biểu thức con cho những toán tử so khớp. Xem xét biểu thức đơn giản /(?:foo){1,2}/. Nếu biểu thức này được viết là /foo{1,2}/, {1,2} sẽ chỉ áp dụng cho kí tự 'o' ở cuối chuỗi 'foo'. Với những dấu ngoặc không nhớ, {1,2} sẽ áp dụng cho cả cụm 'foo'.

* x(?=y)	
Chỉ khớp 'x' nếu 'x' theo sau bởi 'y'.

Ví dụ, /Jack(?=Sprat)/ chỉ khớp với 'Jack' nếu đằng sau nó là 'Sprat'. /Jack(?=Sprat|Frost)/ chỉ khớp 'Jack' nếu theo sau nó là 'Sprat' hoặc 'Frost'. Tuy nhiên, cả 'Sprat' và 'Frost' đều không phải là một phần của kết quả so khớp trả về.

* x(?!y)	
Chỉ khớp 'x' nếu 'x' không được theo sau bởi 'y'.

Ví dụ: /\d+(?!\.)/ chỉ khớp với số không có dấu . đằng sau. Biểu thức /\d+(?!\.)/.exec("3.141")​ cho kết quả là '141' mà không phải '3.141'.

* x|y	
Khớp 'x' hoặc 'y'

Ví dụ, /green|red/ khớp với 'green' trong chuỗi "green apple" và 'red' trong chuỗi "red apple".

* {n}	
Kí tự đứng trước phải xuất hiện n lần. n phải là một số nguyên dương.

Ví dụ, /a{2}/ không khớp với 'a' trong "candy", nhưng nó khớp với tất cả kí tự 'a' trong "caandy", và khớp với 2 kí tự 'a' đầu tiên trong "caaandy".

* {n,m}	
Kí tự đứng trước phải xuất hiện từ n đến m lần. n và m là số nguyên dương và n <= m. Nếu m bị bỏ qua, nó tương đương như ∞.

Ví dụ, /a{1,3}/ không khớp bất kì kí tự nào trong "cndy", kí tự 'a' trong "candy", 2 kí tự 'a' đầu tiên trong "caandy", và 3 kí tự 'a' đầu tiên trong "caaaaaaandy". Lưu ý là "caaaaaaandy" chỉ khớp với 3 kí tự 'a' đầu tiên mặc dù chuỗi đó chứa 7 kí tự 'a'.

* [xyz]	
Lớp kí tự. Loại mẫu này dùng để so khớp với một kí tự bất kì trong dấu ngoặc vuông, bao gồm cả escape sequences. Trong lớp kí tự, dấu chấm (.) và dấu hoa thị (*) không còn là kí tự đặc biệt nên ta không cần kí tự thoát đứng trước nó. Bạn có thể chỉ định một khoảng kí tự bằng cách sử dụng một kí tự gạch nối (-) như trong ví dụ dưới đây:

Mẫu [a-d] so khớp tương tự như mẫu [abcd], khớp với 'b' trong "brisket" và 'c' trong "city". Mẫu /[a-z.]+/ và /[\w.]+/ khớp với toàn chuỗi "test.i.ng".

* [^xyz]	
Lớp kí tự phủ định. Khi kí tự ^ đứng đầu tiên trong dấu ngoặc vuông, nó phủ định mẫu này.

Ví dụ, [^abc] tương tự như [^a-c], khớp với 'r' trong "brisket" và 'h' trong "chop" là kí tự đầu tiên không thuộc khoảng a đến c.

* [\b]	
Khớp với kí tự dịch lùi - backspace (U+0008). Bạn phải đặt trong dấu ngoặc vuông nếu muốn so khớp một kí tự dịch lùi. (Đừng nhầm lẫn với mẫu \b).

* \b	
Khớp với kí tự biên. Kí tự biên là một kí tự giả, nó khớp với vị trí mà một kí tự không được theo sau hoặc đứng trước bởi một kí tự khác. Tương đương với mẫu (^\w|\w$|\W\w|\w\W). Lưu ý rằng một kí tự biên được khớp sẽ không bao gồm trong kết quả so khớp. Nói cách khác, độ dài của một kí tự biên là 0. (Đừng nhầm lẫn với mẫu [\b])

Ví dụ:
/\bm/ khớp với 'm' trong chuỗi "moon";
/oo\b/ không khớp  'oo' trong chuỗi "moon", bởi vì 'oo' được theo sau bởi kí tự 'n';
 /oon\b/ khớp với 'oon' trong chuỗi "moon", bởi vì 'oon' ở cuối chuỗi nên nó không được theo sau bởi một kí tự; 
/\w\b\w/ sẽ không khớp với bất kì thứ gì, bởi vì một kí tự không thể theo sau một kí tự biên và một kí tự thường.

Chú ý: Engine biên dịch biểu thức chính quy trong Javascript định nghĩa một lớp kí tự là những kí tự thường. Bất kỳ kí tự nào không thuộc lớp kí tự bị xem như một kí tự ngắt. Lớp kí tự này khá hạn chế: nó bao gồm bộ kí tự La-tinh cả hoa và thường, số thập phân và kí tự gạch dưới. Kí tự có dấu, như "é" hay "ü", không may, bị đối xử như một kí tự ngắt.

* \B	
Khớp với kí tự không phải kí tự biên. Mẫu này khớp tại vị trí mà kí tự trước và kí tự sau nó cùng kiểu: hoặc cả hai là kí tự hoặc cả hai không phải là kí tự. Bắt đầu và kết thúc chuỗi không được xem là những kí tự.

Ví dụ, /\B../ khớp với 'oo' trong "noonday", và /y\B./ khớp với 'ye' trong "possibly yesterday."

* \cX	
X là một kí tự trong khoảng A tới Z. Mẫu này khớp với một kí tự điều khiển trong một chuỗi.

Ví dụ: /\cM/ khớp với control-M (U+000D) trong chuỗi.

* \d	
Khớp với một kí tự số. Tương đương với mẫu [0-9].

Ví dụ: /\d/ hoặc /[0-9]/ khớp với '2' trong chuỗi "B2 is the suite number."

* \D	
Khớp với một kí tự không phải là kí tự số. Tương đương với mẫu [^0-9].

Ví dụ; /\D/ hoặc /[^0-9]/ khớp với 'B' trong "B2 is the suite number."

* \f	Khớp với kí tự phân trang - form feed (U+000C).
* \n	Khớp với kí tự xuống dòng - line feed (U+000A).
* \r	Khớp với kí tự quay đầu dòng -  carriage return (U+000D).
* \s	
Khớp với một kí tự khoảng trắng, bao gồm trống - space, tab, phân trang - form feed, phân dòng - line feed. Tương đương với [ \f\n\r\t\v​\u00a0\u1680​\u180e\u2000​\u2001\u2002​\u2003\u2004​\u2005\u2006​\u2007\u2008​\u2009\u200a​\u2028\u2029​​\u202f\u205f​\u3000].

Ví dụ: /\s\w*/ khớp với ' bar' trong "foo bar."

\S	
Khớp với một kí tự không phải khoảng trắng. Tương đương với [^ \f\n\r\t\v​\u00a0\u1680​\u180e\u2000​\u2001\u2002​\u2003\u2004​\u2005\u2006​\u2007\u2008​\u2009\u200a​\u2028\u2029​\u202f\u205f​\u3000].

Ví dụ: /\S\w*/ khớp với 'foo' trong chuỗi "foo bar."

* \t	Khớp với kí tự tab (U+0009).
* \v	Khớp với kí tự vertical tab (U+000B).
* \w	
Khớp với tất cả kí tự là chữ, số và gạch dưới. Tương đương với mẫu [A-Za-z0-9_].

ví dụ, /\w/ khớp với 'a' trong "apple," '5' trong "$5.28," và '3' trong "3D."

* \W	
Khớp với tất cả kí tự không phải là chữ. Tương đương với mẫu [^A-Za-z0-9_].

ví dụ, /\W/ hoặc /[^A-Za-z0-9_]/ khớp với '%' trong "50%."

* \n	
Trong đó, n là một số nguyên dương, một tham chiếu ngược tới chuỗi khớp thứ n trong biểu thức (đếm từ trái sang, bắt đầu bằng 1).

ví dụ, /apple(,)\sorange\1/ hay /apple(,)\sorange,/ khớp với 'apple, orange,' trong chuỗi "apple, orange, cherry, peach."

* \0	Khớp với kí tự NULL (U+0000). Lưu ý: không được thêm bất kì một kí tự số nào sau 0, vì \0<các-kí-tự-số> là một biểu diễn hệ bát phân escape sequence.
* \xhh	Khớp với kí tự với mã code là hh (2 số trong hệ thập lục phân)
* \uhhhh	Khớp với kí tự có mã hhhh (4 số trong hệ thập lục phân).
