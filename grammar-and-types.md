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

### Variables
Bạn sử dụng biến như các tên tượng trưng cho giá trị cho ứng dụng. Các tên của biến, được gọi là định danh (identifiers), tuân thủ các nguyên tắc nhất định.

Định danh Javascript nên bắt đầu với chữ cái, dấu gạch dưới (`_`), hoặc dấu dollar (`$`). Các ký tự tiếp theo có thể là số (`0`-`9`).

Bởi vì Javascript là case-sentitive, các chữ cái bao gồm các ký tự từ "`A`" đến "`Z`" (chữ hoa) cũng như "`a`" đến "`z`" (chữ thường).

Một vài ví dụ cho tên hợp pháp là `Number_hits`, `temp99`, `$credit`, và `_name`.

### Khai báo biến (Declaring variables)
Bạn có thể khai báo một biến trong hai cách:
* Với từ khóa `var`. Ví dụ `var x = 42`. Cú pháp này được có thể sử dụng để khai báo cho local variable và biến toàn cục (global variable), tùy thuộc vào bối cảnh thực thi.
* Với từ khóa `let` hoặc `const`. Ví dụ `let y = 13`. Cú pháp này có thể được sử dụng để khai báo local variable trong block-scoped.

Bạn cũng có thể đơn giản chỉ định một giá trị thành một biến. Ví dụ, `x = 42`. Cú pháp này tạo ra một biến toàn cầu chưa khai báo (undeclared global variable). Nó cũng tạo ra một cảnh báo Javascript nghiêm ngặt. Undeclared global variable có thể thường dẫn đến các hành vi không mong muốn. Do đó, không khuyến khích sử dụng undeclared global variable.

### Đánh giá các biến
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

### Phạm vi biến (Variable scope)
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

### Variable hoisting
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

### Function hoisting
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

### Global variables
Các global variable trong thực tế là các thuộc tính của global object.

Trong trang web, global object là `window`, vì vậy bạn có thể thiết lập và truy cập các global variable thông qua cú pháp `window.variable`.

Do đó, bạn có thể truy cập global variable được khai báo trong 1 window hoặc frame từ một window hoặc frame khác bằng cách chỉ định tên `window` hoặc `frame`. Chẳng hạn, nếu một biến có tên là `phoneNumber` trong document. Bạn có thể gọi đến biến này từ một frame với `parent.phoneNumber`.

### Constant
Bạn có thể tạo một biến chỉ để đọc, gọi là hằng số với từ khóa `const`.

Cú pháp định danh một constant rất giống với bất kỳ định danh biến nào. Nó phải bắt đầu với chữ cái, dấu gạch dưới hoặc dấu dollar (`$`), và có thể chứa ký tự alphabet, số, và ký tự gạch dưới.

```js
const PI = 3.14;
```

Một constant không thể thay đổi giá trị thông qua phép gán hoặc khai báo lại trong suốt kịch bản đang chạy. Nó bắt buộc phải được khởi tạo với một giá trị.

Nguyên tắc phạm vi của constant cũng tương tự như phạm vi biến `let`. Nếu từ khóa `const` bị bỏ qua, định danh được coi là đại diện một undeclared variable.

Bạn không thể khai báo một constant với tên giống với một hàm hoặc một biến trong cùng một phạm vi.

```js
// Điều này dẫn đến lỗi
function f() {};
const f = 5;

// Điều này cũng dẫn đến lỗi
function f() {
  const g = 5;
  var g;

  // ...
}
```

Tuy nhiên, các thuộc tính trong object được gán cho constant không được bảo vệ, vì vậy các câu lệnh dưới đây được thực thi mà không có vấn đề gì.

```js
const MY_OBJECT = {'key': 'value'};
MY_OBJECT.key = 'otherValue';
```

Tương tự, nội dung trong array cũng không được bảo vệ.

```js
const MY_ARRAY = ['HTML','CSS'];
MY_ARRAY.push('JAVASCRIPT');
console.log(MY_ARRAY); // ['HTML','CSS','JAVASCRIPT'];
```

## Cấu trúc dữ liệu và kiểu dữ liệu (Data structures and types)

### Kiểu dữ liệu
Tiêu chuẩn mới nhất của ECMAScript định nghĩa tám kiểu dữ liệu:
- Bảy kiểu dữ liệu là primitives:
 1. Boolean. `true` và `false`.
 2. `null`. Một từ khóa đặc biệt để biểu thị một vô giá trị (Bởi vì Javascript là case-sentitive nên `null` không giống với `Null`, `NULL` hoặc bất kỳ biến thể nào.
 3. `undefined`. Một thuộc tính cao cấp nhất có giá trị không xác định.
 4. Number. Một số nguyên hoặc số thập phân, ví dụ `42` hoặc `3.14`.
 5. BigInt. Một số nguyên có độ chính xác tùy ý, ví dụ `9007199254740992n`.
 6. String. Một chuỗi các ký tự đại diện cho giá trị văn bản, ví dụ `"Howdy"`.
 7. Symbol (mới trong ECMAScript 2015). Một kiểu dữ liệu khởi tạo là phiên bản duy nhất và bất biến.
- và Object

Mặc dù các kiểu dữ liệu này tương đối ít, nhưng chúng cho phép bạn thực hiện các hàm hữu ích trong ứng dụng của bạn. `Objects` và `functions` là các yếu tố cơ bản trong ngôn ngữ. Bạn có thể nghĩ object như các container của giá trị, và hàm như thủ tục mà script của bạn phải thực hiện.

### Bộ chuyển đổi kiểu dữ liệu
Javascript là ngôn ngữ kiểu dữ liệu động. Điều này có nghĩa là bạn không cần phải chỉ định kiểu dữ liệu cho một biến khi bạn khai báo nó. Điều này cũng có nghĩa là các kiểu dữ liệu được tự động chuyển đổi khi cần thiết trong suốt quá trình script thực thi.

Vì vậy, cho ví dụ, bạn có thể định nghĩa một biến như sau:

```js
var answer = 42;
```

Và sau đó, bạn đã có thể chỉ định biến tương tự là một giá trị chuỗi, ví dụ:

```js
answer = "Hello world";
```

Vì Javascript là kiểu dữ liệu động, việc chỉ định này sẽ không tạo ra lỗi.

### Số và toán tử "+"
Trong biểu thức liên quan đến số và chuỗi và toán tử `+`. Javascript sẽ chuyển đổi giá trị số sang chuỗi. Ví dụ, xem xét các câu lệnh bên dưới:

```js
x = 'The answer is ' + 42 // "The answer is 42"
y = 42 + ' is the answer' // "42 is the answer"
```

Với các toán tử khác, Javascript không chuyển số thành chuỗi. Ví dụ:

```js
'37' - 7 // 30
'37' + 7 // "377"
```

### Chuyển chuỗi thành số
Trong trường hợp một giá trị đại diện cho một số được lưu dưới dạng chuỗi, có nhiều phương phương thức để chuyển đổi.

* `parseInt()`
* `parseFloat()`

`parseInt` chỉ trả về các số nguyên, vì vậy nó sử dụng để làm tròn số thập phân.

> Ngoài ra, một thực tế tốt cho `parseInt` là luôn luôn bao gồm tham số *radix* (cơ số). Tham số *radix* được sử dụng để chỉ định hệ thống số nào sẽ được sử dụng.

```js
parseInt('101', 2) // 5
```

Một phương thúc thay thể cho việc nhận một số từ chỗi là sử dụng toán tử `+`:

```js
'1.1' + '1.1' // '1.11.1'
(+'1.1') + (+'1.1') // 2.2   
// Chú ý: các dấu ngoặc đơn được thêm vào cho rõ ràng, không bắt buộc.
```

## Literals
Literals đại diện các giá trị trong Javascript. Đó là các giá trị cố định - không phải biến - thứ mà bạn thực sự cung cấp trong script. Phần này mô tả các loại literal bên dưới:

* Array literals
* Boolean literals
* Floating-point literals
* Numeric literals
* Object literals
* RegExp literals
* String literals

### Array literals
Một array literals là một danh sách trống hoặc nhiều biểu thức, mỗi biểu thức đại diện cho một phần tử mảng, được bao quanh trong dấu ngoặc vuông (`[]`). Khi bạn tạo một mảng sử dụng một array literal, nó được khởi tạo với các giá trị đã chỉ định như các phần tử, và `length` của nó được đặt thành số lượng các đối số đã chỉ định.

Đoạn ví dụ sau tạo mảng `coffees` với ba phần tử và `length` là ba.

```js
let coffees = ['French Roast', 'Colombian', 'Kona'];
```

> **Chú ý:** Một array literal là một kiểu đối tượng khởi tạo.

Nếu một mảng được tạo bằng cách sử dụng literal trong script cấp cao nhất, Javascript diễn giải mảng này mỗi khi nó đánh giá biểu thức chứa array literal. Ngoài ra, một literal được sử dụng trong một hàm được tạo mỗi lần function đó được gọi.

> **Chú ý:** Array literal cũng là `Array` object.

#### Dấu phẩy thêm trong array literals
Bạn không phải chỉ định tất cả phần tử trong một array literal. Nếu bạn đặt hai dấu phẩy trong một hàng, mảng này điền vào giá trị `undefined` cho các phần tử không chỉ định. Ví dụ sau tạo mảng `fish`:

```js
let fish = ['Lion', , 'Angel'];
```

Mảng này có hai phần tử có giá trị và một phần tử trống:

* `fish[0]` là "Lion"
* `fish[1]` là `undefined`
* `fish[2]` là "Angel"

Nếu bạn bao gồm một dấu phẩy tại vị trí cuối của danh sách phần tử, nó sẽ bị bỏ qua.

Trong ví dụ sau, `length` của mảng là ba. Không có `myList[3]`. Tất cả các dấu phẩy khác trong danh sách biểu thị cho một phần tử mới.

> **Chú ý:** Dấu phẩu có thể tạo ra lỗi trong các phiên bản trình duyệt cũ và thực tế tốt nhất là loại bỏ chúng.

```js
let myList = ['home', , 'school', ];
```

Trong ví dụ sau, `length` của mảng là bốn, và `myList[0]` và `myList[2]` là còn thiếu.

```js
let myList = [ ,'home', , 'school'];
```

Trong ví dụ sau, `length` của mảng là bốn, và `myList[1]` và `myList[3]` là còn thiếu. **Chỉ dấu phẩu cuối cùng bị bỏ qua**.

```js
let myList = ['home', , 'school', , ];
```

Việc hiểu các hành vi của dấu phẩy thêm là quan trọng cho việc hiểu Javascript như một ngôn ngữ.

Tuy nhiên, khi biết code của bạn, bạn nên khai báo rõ ràng các phần tử thiếu là `undefined`. Làm điều này sẽ tăng sự rõ ràng cho code của bạn và có khả năng bảo trì.

### Boolean literals
Loại Boolean có hai giá trị literal: `true` và `false`.

> **Cẩn thận:** Đừng nhầm lẫn các giá trị primitive Boolean `true` và `false` với giá trị true và false của `Boolean` object.
> Boolean object là một lớp bọc xung quanh kiểu dữ liệu primitive Boolean.

### Numeric literals
Kiểu `Number` và `BigInt` có thể bị khi lại trong decimal (cơ số 10), hexadecimal (cơ số 16), octal (cơ số 8) và binary (cơ số 2).

* Một decimal numeric literal là một chuỗi các số mà không bắt đầu với `0`.
* Số `0` dẫn đầu trên một numeric literal, hoặc dẫn đầu là `0o` (hoặc `0O`) biểu thị nó là một octal. Octal numeric có thể chỉ bao gồm các số `0`-`7`.
* Dẫn đầu với `0x` (hoặc `0X`) biểu thị là một kiểu hexadecimal numeric. hexadecimal numeric có thể bao gồm các số (`0`-`9`) và các chữ cái `a`-`f` và `A`-`F`. (Trường hợp của một ký tự không thay đổi giá trĩ của nó. Vì thế: `0xa` = `0xA` = `10` và `0xf` = `0xF` = `15`).
* Dẫn đầu với `0b` (hoặc `0B`) biểu thị cho một binary numeric literal. Binary numeric chỉ có thể bao gồm các số `0` và `1`.

Một vài ví dụ cho các numeric literals là:

```js
0, 117, -345, 123456789123456789n             (decimal, base 10)
015, 0001, -0o77, 0o777777777777n             (octal, base 8) 
0x1123, 0x00111, -0xF1A7, 0x123456789ABCDEFn  (hexadecimal, "hex" or base 16)
0b11, 0b0011, -0b11, 0b11101001010101010101n  (binary, base 2)
```

### Floating-point literals
Một floating-point literal có thể có các phần sau:

* Một decimal integer có thể được ký (trước "+" hoặc "-"),
* Một decimal point ("`.`"),
* Một phân số (số thập phân khác),
* Một số mũ

Thành phần số mũ là một "`e`" hoặc "`E`" theo sau là một integer, số có thể được ký (trước "+" hoặc "-"). Một floating-point literal phải có ít nhất một số, và hoặc một decimal point hoặc "`e`" (hoặc "`E`").

Ngắn gọn hơn, cú pháp là:

```js
[(+|-)][digits].[digits][(E|e)[(+|-)]digits]
```

Ví dụ:

```js
3.1415926
-.123456789
-3.1E+12
.1e-23
```

### Object literals
Một object literal là một danh sách số trống hoặc nhiều cặp của các tên thuộc tính và các giá trị liên quan của một object, được bao quanh trong ngoặc nhọn (`{}`).

> **Đừng sử dụng một object literal khi bắt đầu của một câu lệnh!** Điều này sẽ dẫn đến một lỗi (hoặc hành vi không mong đợi), bởi vì `{` sẽ được diễn giải như một bắt đầu của block.

Theo dõi một ví dụ của object literal. Phần tử đầu tiên của object `car` định nghĩa một thuộc tính, `myCar`, và chỉ định nó một string mới, `"Saturn"`; phần tử thứ hai, thuộc tính `getCar`, ngay lập tức được chỉ định kết quả của một function `(carTypes("Honda"))`; phần tử thứ ba, thuộc tính `special`, sử dụng một biến đã tồn tại (`sales`).

```js
var sales = 'Toyota';

function carTypes(name) {
  if (name === 'Honda') {
    return name;
  } else {
    return "Sorry, we don't sell " + name + ".";
  }
}

var car = { myCar: 'Saturn', getCar: carTypes('Honda'), special: sales };

console.log(car.myCar);   // Saturn
console.log(car.getCar);  // Honda
console.log(car.special); // Toyota 
```

Ngoài ra, bạn có thể sử dụng một numeric hoặc string literal cho tên của một thuộc tính hoặc lồng một object trong một object khác. Ví dụ sau sử dụng các tùy chọn này.

```js
var car = { manyCars: {a: 'Saab', b: 'Jeep'}, 7: 'Mazda' };

console.log(car.manyCars.b); // Jeep
console.log(car[7]); // Mazda
```

Tên thuộc tính object có thẻ là bất kỳ chuỗi nào, bao gồm chuỗi trống. Nếu tên thuộc tính không phải là một định danh Javascript hợp lệ hoặc số, nó phải được bao quanh trong nháy kép hoặc nháy đơn.

Tên thuộc tính không phải định danh hợp lệ thì không thể truy cập với dấu chấm (`.`), nhưng có thể truy cập và thiết lập giống như array ("`[]`").

```js
var unusualPropertyNames = {
  '': 'An empty string',
  '!': 'Bang!'
}
console.log(unusualPropertyNames.'');   // SyntaxError: Unexpected string
console.log(unusualPropertyNames['']);  // Một chuỗi rỗng
console.log(unusualPropertyNames.!);    // SyntaxError: Unexpected token !
console.log(unusualPropertyNames['!']); // Bang!
```

### Enhanced Object literals
Trong ES2015, object literal được mở rộng để hỗ trợ thiết lập thuộc tính tại construction, shorthand cho việc chỉ định `foo: foo`, định nghĩa phương thức, tạo cuộc gọi `super`, và xử lý các tên thuộc tính với biểu thức.

Tóm lại, những điều này mang object literal và khai báo `class` gần nhau hơn và cho phép thiết kế object-based để hưởng lợi từ một vài tiện ích tương tự.

```js
var obj = {
    // __proto__
    __proto__: theProtoObj,
    // Shorthand for ‘handler: handler’
    handler,
    // Methods
    toString() {
     // Super calls
     return 'd ' + super.toString();
    },
    // Computed (dynamic) property names
    [ 'prop_' + (() => 42)() ]: 42
};
```

### RegExp literals
Một regex literal là một pattern được bao quanh giữa dấu gạch chéo. Đây là ví dụ của một regex literal.

```js
var re = /ab+c/;
```

### String literals
Một string literal là không hoặc nhiều ký tự bao quanh bởi dấu nháy kép (`"`) hoặc nháy đơn (`'`). Một chuỗi phải được phân định bởi dấu quote cùng loại (nghĩa là cả hai dấu nháy đơn, hoặc cả hai dấu kép).

Sau đây là ví dụ về string literal:

```js
'foo'
"bar"
'1234'
'one line \n another line'
"John's cat"
```

Bạn có thể gọi mất kỳ method nào của `String` object trên một giá trị string literal. Javascript tự động chuyển đổi string literal thành một String object tạm, gọi các method, sau đó loại bỏ String object tạm đi. Bạn cũng có thể sử dụng thuộc tính `String.length` với một string literal:

```js
console.log("John's cat".length)  // 10.
```

Trong ES2015, template literals cũng có sẵn. Template literal được bao quanh bởi dấu back-tick (`) thay cho dấu nháy đơn hoặc nháy kép.

Template string cung cấp cú pháp đặc biệt cho việc khởi tạo chuỗi. (Điều này giống như các tính năng string interpolation trong Perl, Python...)


