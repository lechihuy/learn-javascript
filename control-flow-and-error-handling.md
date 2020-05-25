# Điều khiển luồng và xử lý lỗi

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

Đây, `{ x++ }` là một block statement.

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
