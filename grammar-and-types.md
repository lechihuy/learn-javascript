# Cấu trúc và kiểu dữ liệu
Chương này nói về cấu trúc cơ bản của Javascript, các kiểu khai báo, kiểu dữ liệu và literal.

## Cơ bản
Javascript mượn hầu hết các cú pháp từ Java, C và C++, nhưng cũng có chút ảnh hưởng bởi Awk, Perl và Python.
Javascript là case-sensitive (tức là phân biệt các các ký tự hoa thường) và sử dụng ký tự Unicode. Ví dụ từ "sớm" có thể sử dụng như một tên biến

```js
let sớm = "foobar"
```

Nhưng biến `sớm` không giống với `Sớm` vì Javascript là case-sentitive.

Trong Javascript, các câu lệnh được ngăn cách nhau bởi dấu chấm phẩy (;).

Một dấu chẩm phẩy là không cần thiết sau mỗi câu lệnh nếu nó được viết trên dòng riêng của nó. Nhưng nếu có nhiều hơn một câu lệnh trên một dòng, chúng ta phải ngăn cách chúng bằng dấu chấm phẩy.

> ECMAScript, một chuẩn hóa ngôn ngữ client, cũng ràng buộc tự động thêm các dấu chấm phẩy để kết thúc câu lệnh.

Nó được xem xét như là thực tiễn tốt nhất, tuy nhiên, luôn luôn viết một dấu chấm phẩy sau mỗi câu lệnh, thậm chí khi nó không thật sự cần thiết. Điều này giảm thiếu cơ hội các lỗi trong lập trình (bug) đến với code của bạn.

Code Javascript được quét từ trái sang phải, và được chuyển thành một chuỗi các yếu tố đầu vào như token, ký tự điều khiển (control characters), dấu kết thúc dòng (line terminators), chú thích (comments) hoặc whitespace (Khoảng trắng, tab và ký tự dòng mới được xem là whitespace).

## Comments
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

## Kiểu khai báo (Declarations)
Javascript có ba kiểu khai báo

`var`: khởi tạo một biến (variable), tùy chọn khởi tạo nó thành một giá trị.

`let`: khởi tạo một khối phạm vi (block-scoped), biến cục bộ (local variable), tùy chọn khởi tạo nó thành một giá trị.

`const`: khởi tạo một block-scoped, chỉ được đọc gọi là hằng số (constant).

## Variables
Bạn sử dụng biến như các tên tượng trưng cho giá trị cho ứng dụng. Các tên của biến, được gọi là định danh (identifiers), tuân thủ các nguyên tắc nhất định.

Định danh Javascript nên bắt đầu với chữ cái, dấu gạch dưới (`_`), hoặc dấu dollar (`$`). Các ký tự tiếp theo có thể là số (`0`-`9`).

Bởi vì Javascript là case-sentitive, các chữ cái bao gồm các ký tự từ "`A`" đến "`Z`" (chữ hoa) cũng như "`a`" đến "`z`" (chữ thường).

Một vài ví dụ cho tên hợp pháp là `Number_hits`, `temp99`, `$credit`, và `_name`.

## Khai báo biến (Declaring variables)
Bạn có thể khai báo một biến trong hai cách:
* Với từ khóa `var`. Ví dụ `var x = 42`. Cú pháp này được có thể sử dụng để khai báo cho local variable và biến toàn cục (global variable), tùy thuộc vào bối cảnh thực thi.
* Với từ khóa `let` hoặc `const`. Ví dụ `let y = 13`. Cú pháp này có thể được sử dụng để khai báo local variable trong block-scoped.

Bạn cũng có thể đơn giản chỉ định một giá trị thành một biến. Ví dụ, `x = 42`. Cú pháp này tạo ra một biến toàn cầu chưa khai báo (undeclared global variable). Nó cũng tạo ra một cảnh báo Javascript nghiêm ngặt. Undeclared global variable có thể thường dẫn đến các hành vi không mong muốn. Do đó, không khuyến khích sử dụng undeclared global variable.

## Đánh giá các biến
Một biến được khai báo mà không gán giá trị thì được chỉ định với giá trị là `undefined`.

Sự cố gắng truy cập một biến chưa được khai báo (undeclared variable) sẽ trả về một ngoại lệ (exception) `ReferenceError`.

```js
var a;
console.log('Giá trị biến a là ' + a); // Giá trị biến a là undefined

console.log('Giá trị biến b là ' + b); // Giá trị biến b là undefined
var b;
// Bạn sẽ hiểu vấn đề này khi tìm hiểu đến "Variable hoisting"

console.log('Giá trị biến c là ' + c); // Uncaught ReferenceError: c is not defined

let x;
console.log('Giá trị biến x là ' + x); // Giá trị biến x là undefined

console.log('Giá trị biến y là ' + y); // Uncaught ReferenceError: y is not defined
let y; 
```

Bạn có thể sử dụng `undefined` dể kiểm tra liệu một biến có giá trị hay không. Theo như đoạn code này, biến `input` không được gán giá trị, và câu lệnh `if` sẽ là `true`.

```js
var input;
if (input === undefined) {
  doThis();
} else {
  doThat();
}
```

Giá trị `undefined` được xem là `false` khi sử dụng trong bối cảnh boolean (boolean context). Ví dụ, đoạn code này thực thi hàm `myFunction` bởi vì phần tử `myArray` là `undefined`.

```js
var myArray = [];
if (!myArray[0]) myFunction();
```

Giá trị `undefinied` sẽ chuyển thành `NaN` khi sử dụng trong numeric context.

```js
var a;
a + 2;  // NaN + 2
```

Khi bạn đánh giá một biến `null`, nó được xem như là `0` trong numeric context và `false` trong boolean context. Ví dụ:

```js
var n = null;
console.log(n * 32); // Sẽ trả về 0
```

## Phạm vi biến (Variable scope)
khi bạn khai báo một biến ở ngoài bất kỳ hàm nào, nó được gọi là global variable, bởi vì nó có sẵn cho bất kỳ đoạn code nào trong document hiện tại. Khi bạn khai báo một biến trong một hàm, nó gọi là local variable, bởi vì nó chỉ có sẵn trong hàm đó mà thôi.

Javascript trước ECMAScript 2015 không có cú pháp phạm vi khối. Thay vào đó, một biến được khai báo trong một khối là cục bộ của hàm (hoặc phạm vi toàn cục) mà khối nằm trong đó.

Chẳng hạn, đoạn code này sẽ trả về `5`, bởi vì phạm vị của biến `x` là global context (hoặc function context nếu code đó là một phần của hàm). Phạm vi của `x` là không giới hạn ở khối lệnh `if` luôn đúng này.

```js
if (true) {
  var x = 5;
}
console.log(x);  // x là 5
```

Hành vi này thay đổi khi sử dụng cách khai báo với từ khóa `let`.

```js
if (true) {
  let y = 5;
}
console.log(y);  // ReferenceError: y is not defined
```

## Variable hoisting
Một điều bất thường trong biến Javascript là bạn có thể gọi một biến trước khi nó được khai báo mà không xuất hiện một exception nào.

Khái niệm này được biết đến là hoisting. Các biến trong Javascript, theo một nghĩa nào đó, được "hoisted" (hoặc "lifted") lên trên đầu của hàm hoặc câu lệnh. Tuy nhiên các biến được hoisted trả về giá trị là `undefined`. Thậm chí nếu bạn khai báo hoặc khởi tạo sau khi bạn sử dụng hoặc gọi biến này, nó vẫn trả về giá trị `undefined`.

```js
/**
 * Ví dụ 1
 */
console.log(x === undefined); // true
var x = 3;

/**
 * Ví dụ 2
 */
// Trả về giá trị undefined
var myvar = 'my value';
 
(function() {
  console.log(myvar); // undefined
  var myvar = 'local value';
})();
```

Đoạn code trên sẽ được giải thích như:

```js
/**
 * Ví dụ 1
 */
console.log(x === undefined); // true
var x = 3;

/**
 * Ví dụ 2
 */
// Trả về giá trị undefined
var myvar = 'my value';
 
(function() {
  var myvar;
  console.log(myvar); // undefined
  myvar = 'local value';
})();
```

Bởi vì trong hoisting, tất cả các câu lệnh `var` trong hàm nên được đặt càng gần vị trí đầu của hàm càng tốt. Thực tế này làm tăng sự rõ ràng của code.

Trong ECMAScript 2015, `let` và `const` được hoisted nhưng không được khởi tạo. Việc gọi biến trong block trước khi khai báo biến trả về `ReferenceError` exception. Bởi vì biến nằm trong "vùng chết tạm thời" từ khi bắt đầu block cho đến khi khai báo được xử lý.

```js
console.log(x); // ReferenceError
let x = 3;
```

## Function hoisting
Trong trường hợp của hàm, chỉ có khai báo hàm (function declaration) là được hoisted, biểu thức hàm (function expression) thì không.

```js
/* Function declaration */

foo(); // "bar"

function foo() {
  console.log('bar');
}


/* Function expression */

baz(); // TypeError: baz is not a function

var baz = function() {
  console.log('bar2');
};
```

## Global variables
Các global variable trong thực tế là các thuộc tính của global object.

Trong trang web, global object là `window`, vì vậy bạn có thể thiết lập và truy cập các global variable thông qua cú pháp `window.variable`.

Do đó, bạn có thể truy cập global variable được khai báo trong 1 window hoặc frame từ một window hoặc frame khác bằng cách chỉ định tên `window` hoặc `frame`. Chẳng hạn, nếu một biến có tên là `phoneNumber` trong document. Bạn có thể gọi đến biến này từ một frame với `parent.phoneNumber`.
