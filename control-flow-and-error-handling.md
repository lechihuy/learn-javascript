# Control flow and error handling

Javascript hỗ trợ một tập hợp các câu lệnh ngắn gọn, đặc biệt là các câu lệnh điều khiển luồng, thứ mà bạn có thể sử dụng để kết hợp nhiều tính tương tác trong ứng dụng của mình. Chương này cung cấp một cái nhìn tổng quan về các câu lệnh này.

## Block statement
Hầu hết các câu lệnh cơ bản là một block statement được dùng để nhóm các câu lệnh. Block được phân định bởi cặp dấu ngoặc nhọn (`{}`).

```
{
  statement_1;
  statement_2;
  ⋮
  statement_n;
}
```

### Ví dụ
Block statement thường được sử dụng với control flow statement (`if`, `for`, `while`).

```js
while (x < 10) {
  x++;
}
```

Ở đây, `{ x++ }` là một block statement.

> **Quan trọng:** Javascript trước ECMAScript 2015 (lần chỉnh sửa thứ 6) không có block scope! Trong Javascript cũ hơn, biến được giới thiệu trong một block được đặt trong phạm vi function hoặc script, và các hiệu ứng thiết lập chúng vẫn còn tồn tại ngoài block. Nói cách khác, block statement không định nghĩa một scope.
> Các block "độc lập" trong Javascript có thể tạo ra kết quả hoàn toàn khác so với những gì chúng sẽ tạo ra trong C hoặc Java. Ví dụ:
> ```js
> var x = 1;
> {
>   var x = 2;
> }
> console.log(x); // 2
> ```
> Output là `2` bởi vì câu lệnh `var x` trong block có scope tương tự với câu lệnh `var x` trước block. (Trong C hoặc Java, code tương tự sẽ trả về output là `1`.)
> Trong ECMAScript 2015, khai báo `let` và `const` là block-scoped.

## Conditional statements
Một conditional statement là tập hợp các lệnh sẽ được thực thi nếu một điều kiện đã được chỉ định là đúng. Javascript hỗ trợ hai conditional statement là `if...else` và `switch`.

### `if...else` statement
Sử dụng `if` statement để thực thi một câu lệnh nếu một điều kiện logic là `true`. Sử dụng tùy chọn mệnh đề `else` để thực thi câu lệnh nếu điều kiện đó là `false`.

Một `if` statement trông như thế này:

```js
if (condition) {
  statement_1;
} else {
  statement_2;
}
```

Ở đây, `condition` có thể là bất kỳ expression nào nhận giá trị là `true` hoặc `false`.

Nếu `condition` là `true`, `statement_1` sẽ được thực thi. Nếu không thì, `statement_2` sẽ được thực thi. `statement_1` và `statement_2` có thể là bất kỳ câu lệnh nào, bao gồm các `if` statement lồng tiếp tục.

Bạn cũng có thể điều chỉnh câu lệnh sử dụng `else if` để nhiều điều kiện được kiểm tra trong sự liên tục.

```js
if (condition_1) {
  statement_1;
} else if (condition_2) {
  statement_2;
} else if (condition_n) {
  statement_n;
} else {
  statement_last;
} 
```

Trong trường hợp của nhiều điều kiện, chỉ điều kiện logic đầu tiên có giá trị là `true` sẽ được thực thị. Để thực thi nhiều câu lệnh, nhóm chúng trong một block statement (`{...}`).

### Best practice
Nhìn chung, một thực tế tốt là luôn luôn sử dụng block statement, đặc biệt là khi lồng `if` statement:

```js
if (condition) {
  statement_1_runs_if_condition_is_true;
  statement_2_runs_if_condition_is_true;
} else {
  statement_3_runs_if_condition_is_false;
  statement_4_runs_if_condition_is_false;
}
```

Thật không không ngoan khi sử dụng phép gán đơn giản trong một biểu thức điều kiện, bởi vì phép gán có thể làm nhầm lẫn với so sánh khi liếc nhanh qua code.

Ví dụ, đừng viết code như thế này:

```js
// Dễ bị đọc sai thành "x == y"
if (x = y) {
  /* statements here */
}
```

Nếu bạn cần sử dụng một phép gán trong biểu thức điều kiện, một practice phổ biến là đặt dấu ngoặc đơn xung quanh phép gán, như thế này:

```js
if ((x = y)) {
  /* statements here */
}
```

### Falsy values
Các giá trị dưới đây được xem là `false` (được biết là Falsy value)

* `false`
* `undefined`
* `null`
* `0`
* `NaN`
* Empty string (`""`)

Tất cả các giá trị khác - bao gồm tất cả các object - được xem là `true` khi vượt qua một câu lệnh điều kiện.

> **Thận trọng:** Đừng nhầm lẫn giữa primitive boolean `true` và `false` với true và false của `Boolean` object.
> Ví dụ:
> ```js
> var b = new Boolean(false);
> if (b)         // điều kiện này trả về true
> if (b == true) // điều kiện này trả về false
> ```

### Ví dụ
Trong ví dụ bên dưới, function `checkData` trả về `true` nếu độ dài ký tự trong `Text` object là ba. Nếu không thì, nó sẽ hiển thị một cảnh báo và trả về `false`.

```js
function checkData() {
  if (document.form1.threeChar.value.length == 3) {
    return true;
  } else {
    alert(
        'Enter exactly three characters. ' +
        `${document.form1.threeChar.value} is not valid.`);
    return false;
  }
}
```

## `switch` statement
`switch` statement cho phép chương trình có thể đánh giá một biểu thức và cố gắng match giá trị của biểu thức với `case` label. Nếu match được tìm thấy, chương trình thực thi câu lệnh liên quan.

Một `switch` statement trông như sau:

```js
switch (expression) {
  case label_1:
    statements_1
    [break;]
  case label_2:
    statements_2
    [break;]
    …
  default:
    statements_def
    [break;]
}
```

Javascript đánh giá `switch` statement trên như sau:

- Chương trình tìm kiếm mệnh đề `case` đầu tiên với label match giá trị của biểu thức và sau đó chuyển quyền kiểm soát sang mệnh đề đó, thực thi các câu lệnh liên quan.
- Nếu không match label nào, chương trình sẽ tìm kiếm mệnh đề tùy chọn `default`:
  - Nếu mệnh đề `default` được tìm thấy, chương trình chuyển quyền kiểm soát cho mệnh đề, thực thi các câu lệnh liên quan.
  - Nếu không tìm thấy mệnh đề `default`, chương trình sẽ tiếp túc thực hiện các câu lệnh bên dưới sau khi kết thúc `switch`.
  - (Theo quy ước, mệnh đề `default` được viết như là mệnh đề cuối cùng, nhưng nó không cần phải như vậy.)
  
### `break` statements
Câu lệnh tùy chọn `break` liên quan đến mỗi mệnh đề `case` để đảm bảm chương trình thoát ra `switch` mỗi lần matched statement được thực thi, và sau đó tie16p ực thực hiện các câu lệnh bên dưới `switch`. Nếu `break` bị bỏ qua, chương trình sẽ tiếp tục thực hiện bên trong `switch` statement (và sẽ đánh giá `case` tiếp theo, và cứ thế).

#### Ví dụ
Trong ví dụ dưới đây, nếu `fruittype` có giá trị là `'Bananas'`, chương trình match giá trị này với case `'Bananas'` và thực thi các câu lệnh liên quan. Khi gặp tới `break`, chương trình thoát `switch` và tiếp tực thực hiện các statement sau `switch`. Nếu `break` bị bỏ qua, câu lệnh `case 'Cherries'` cũng sẽ được thực thi. 

```js
switch (fruittype) {
  case 'Oranges':
    console.log('Oranges are $0.59 a pound.');
    break;
  case 'Apples':
    console.log('Apples are $0.32 a pound.');
    break;
  case 'Bananas':
    console.log('Bananas are $0.48 a pound.');
    break;
  case 'Cherries':
    console.log('Cherries are $3.00 a pound.');
    break;
  case 'Mangoes':
    console.log('Mangoes are $0.56 a pound.');
    break;
  case 'Papayas':
    console.log('Mangoes and papayas are $2.79 a pound.');
    break;
  default:
   console.log(`Sorry, we are out of ${fruittype}.`);
}
console.log("Is there anything else you'd like?");
```

## Exception handling statements
Bạn có thể ném các exception sử dụng `throw` statement và xử lý chúng bằng cách sử dụng `try...catch` statement.

* `throw` statement
* `try...catch` statement

### Exception types
Bất kỳ đối tượng nào cũng có thể throw trong Javascript. Tuy nhiên, không phải tất cả thrown object được tạo ra bằng nhau. Trong khi thông thường là ném các số hoặc chuỗi như các lỗi, nhưng thường hiệu quả hơn để sử dụng một loại exception đặc biệt được tạo ra cho mục đích này.

* ECMAScript exceptions
* `DOMException` và `DOMError`

### `throw` statement
Sử dụng `throw` statement để throw một exception. `throw` statement chỉ định giá trị được throw.

```js
throw expression;
```

Bạn có thể ném bất kỳ expression nào, không chỉ expression của các loại cụ thể. Đoạn code dưới đây throw các exception của nhiều loại:

```js
throw 'Error2';   // String type
throw 42;         // Number type
throw true;       // Boolean type
throw {toString: function() { return "I'm an object!"; } };
```

> **Chú ý:** Bạn có thể chỉ định một object khi bạn throw một exception. Sau đó bạn có thể gọi các thuộc tính object trong `catch` block.

```js
// Khởi tạo một object loại UserException
function UserException(message) {
  this.message = message;
  this.name = 'UserException';
}

// Tạo exception chuyển đổi thành chuỗi khi sử dụng dưới dạng chuỗi
// (e.g., by the error console)
UserException.prototype.toString = function() {
  return `${this.name}: "${this.message}"`;
}

// Tạo một khởi tạo của loại object và throw nó
throw new UserException('Value too high');
```

### `try...catch` statement
`try...catch` statement đánh dấu một khối lệnh để thử, và chỉ định một hoặc nhiều response nên là một exception được throw. Nếu một exception được throw, `try...catch` statement sẽ bắt nó.

`try...catch` statement bao gồm một `try` block, nó sẽ chứa một hoặc nhiều câu lệnh, và một `catch` block, chứa các câu lệnh chỉ định phải làm gì nếu một exception được throw trong `try` block.

Nói cách khác, bạn muốn `try` block thành công - nhưng nếu nó không vậy, bạn sẽ phải  kiểm soát để vượt qua `catch` block. Nếu bất kỳ câu lệnh nào trong `try` block (hoặc trong một function ở trong `try` block) throw một exception, kiểm soát ngay lập tức chuyển sang `catch ` block. Nếu không có exception được throw trong `try` block, `catch` block sẽ bị bỏ qua. `finally` block thực thi sau khi `try` và `catch` block thực thi nhưng trước các câu lệnh bên dưới `try...catch` statement.

Ví dụ dưới đây sử dụng `try...catch` statement. Ví dụ này gọi một function lấy tên một tháng từ một mảng dựa trên giá trị được truyền vào hàm. Nếu giá trị không tương ứng với số một tháng (`1`-`12`), một exception sẽ được throw với giá trị `"InvalidMonthNo"` và các câu lệnh trong `catch` block đặt biến `monthName` thành `'unknown'`.


```js
function getMonthName(mo) {
  mo = mo - 1; // Adjust month number for array index (1 = Jan, 12 = Dec)
  let months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul',
                'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
  if (months[mo]) {
    return months[mo];
  } else {
    throw 'InvalidMonthNo'; // throw keyword is used here
  }
}

try { // statements to try
  monthName = getMonthName(myMonth); // function could throw exception
}
catch (e) {
  monthName = 'unknown';
  logMyErrors(e); // pass exception object to error handler (i.e. your own function)
}
```
