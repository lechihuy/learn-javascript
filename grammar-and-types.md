# Cấu trúc và kiểu dữ liệu
Chương này nói về cấu trúc cơ bản của Javascript, các kiểu khai báo, kiểu dữ liệu và literal.

Nói một chút về thuật ngữ "literal" trong Javascript, nó là một giá trị mà thể hiện chính bản thân nó. Chẳng hạn, số 12 là một literal vì nó đại diện cho kiểu dữ liệu số nguyên, "hello" cũng là một literal vì nó đại diện cho kiểu chuỗi.

## Cơ bản
Javascript mượn hầu hết các cú pháp từ Java, C và C++, nhưng cũng có chút ảnh hưởng bởi Awk, Perl và Python.
Javascript là case-sensitive (tức là phân biệt các các ký tự hoa thường) và sử dụng ký tự Unicode. Ví dụ từ Früh (nghĩa là "sớm" trong tiếng Đức) có thể sử dụng như một tên biến

```js
let Früh = "foobar"
```

Nhưng biến `früh` không giống với `Früh` vì Javascript là case-sentitive.

Trong Javascript, các câu lệnh được ngăn cách nhau bởi dấu chấm phẩy (;).

Một dấu chẩm phẩy là không cần thiết sau mỗi câu lệnh nếu nó được viết trên dòng riêng của nó. Nhưng nếu có nhiều hơn một câu lệnh trên một dòng, chúng ta phải ngăn cách chúng bằng dấu chấm phẩy.

> ECMAScript, một chuẩn hóa ngôn ngữ client, cũng ràng buộc tự động thêm các dấu chấm phẩy để kết thúc câu lệnh.

Nó được xem xét như là thực tiễn tốt nhất, tuy nhiên, luôn luôn viết một dấu chấm phẩy sau mỗi câu lệnh, thậm chí khi nó không thật sự cần thiết. Điều này giảm thiếu cơ hội các bug (lỗi trong lập trình) đến với code của bạn.

Nguồn văn bản của mã Javascript được quét từ trái sang phải, và được chuyển thành một chuỗi các yếu tố đầu vào như token, control characters (ký tự điều khiển), line terminators (dấu kết thúc dòng), comments (chú thích) hoặc whitespace (Khoảng trắng, tab và ký tự dòng mới được xem là whitespace).

## Comment
Cú pháp comment giống với C++ cũng như nhiều ngôn ngữ khác:

```js
// một dòng comment
 
/* Đây là một comment dài hơn, 
 * Nhiều dòng comment
 */
```

Các comment hành xử như whitespace và bị loại bỏ trong quá trình thực thi code.

> **Chú ý:** Bạn có thể cũng thấy một loại cú pháp comment thứ ba tại phần bắt đầu của một vài file Javascript, trông như thế này `#!/usr/bin/env node`.
>
> Đây được gọi là cú pháp hashbang comment, một loại comment đặc biệt dùng để chỉ định đường dẫn đến một Javascript engine cụ thể để thực thi code.
