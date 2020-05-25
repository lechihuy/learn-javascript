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

