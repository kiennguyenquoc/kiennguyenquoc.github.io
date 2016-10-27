---
layout: post
title: Một số Code conventions khi sử dụng Ruby on Rails.
tags: code-conventions
excerpt: "Một tài liệu dùng để tham khảo cho việc viết code Ruby on rails trở nên tốt hơn."
categories: [ruby]
comments: true
image:
  feature: simplify.png
---

### 1. Các qui tắt chung.
- Dùng 2 space.
- Dùng space trước và sau các dấu `+,-,x,/, {, }, =`.
- Không dùng space sau dấu `(, [ ` và trước dấu  `), ]`.
- Thêm dấu  `_ ` ở các số lớn. Ví dụ: `100000 –> 100_000`.

### 2. Cú pháp.
- Dùng `(, )` ở khai báo hàm có truyền tham số, không dùng `(, )` trong trường hợp hàm không nhận tham số.

### 3. Các câu lệnh điều kiện.
- Không dùng `and, or` hãy ùng `&&, ||`
- Dùng unless thay cho if not.
- Không dùng unless … else
- Không dùng` (, )` ở điều kiện trong câu `if, unless`
- Dùng các hàm số có sẵn như `x.even?`,` x.odd?`, `x.nil?`, `x.zero?` thay cho các câu so sánh `x % 2 == 0`, `x % 2 == 1`, `x == nil`, `x == 0`.
- Trong trường hợp thân câu `if/unless/while/until` chỉ có một dòng, dùng **inline format**. 

**Ví dụ:**

```
do_something if some_condition
```
*thay cho*
```
if some_condition  
  do_something  
end
```

### 4. Câu lệnh lặp.
- Hạn chế dùng câu `for`, nên dùng câu `each`.
- Dùng `until` thay cho `while not`.

### 5. Khai báo và gọi hàm.
- Bỏ `(, )` khi gọi các hàm không tham số
- Nếu hàm có tham số, để các tham số trong` ()`. Ví dụ: `foo(param1, param2)`.
- Không cần dùng `return` ở dòng cuối cùng trong khai báo hàm.

**Ví dụ:**

```
def some_method(some_arr)
  some_arr.size
end
```

- Không dùng `space` giữa tên hàm và dấu `(`
- Dùng `→` thay cho từ khóa `lambda`
- Dùng các câu `inline if` thay cho các câu `nested if`. 
 
Ví dụ:
```
# Bad
def compute_thing(thing)
  if thing[:foo]
    update_with_bar(thing)
      if thing[:foo][:bar]
        partial_compute(thing)
      else
        re_compute(thing)
      end
  end
end
```

``` 
# Good
def compute_thing(thing)
  return unless thing[:foo]
  update_with_bar(thing[:foo])
  return re_compute(thing) unless thing[:foo][:bar]
  partial_compute(thing)
end
```

- Khi khai báo biến `array, hash` dùng cấu trúc: `a_arr = []`, `a_hash = {}` thay cho `a_arr = Array.new`, `a_hash = Hash.new`

### 6. Qui tắc đặt tên.
- Tên biến, tên hàm, symbol: `a_var_name`, `get_prime`, `a_symbol`.
- Tên class, module: `SomeClass`, `SomeModule`
- Hằng số: `SOME_CONST`

### 7. Class, Module.
- Dùng include, extend ngay sau khai báo `class`.
- Dùng `attr_reader, attr_writer, attr_accessor` thay cho các hàm `set, get`.
- Hạn chế dùng `self << class`, nên dùng `def self.a_func`.

### 8. Collection.
- Dùng `%w `để khai báo mảng các chuỗi.
- Dùng `%i` để khai báo mảng các symbol.
- Nên dùng `symbol` làm key trong `hash`. Ví dụ: `{:one ⇒ 1, :two ⇒ 2}`.

### 9. String.
- Dùng `#{}` thay cho nối chuỗi. Ví dụ: `email_with_name = "#{user.name} <#{user.email}>`.
- Dùng `%Q` để khai báo chuỗi có `', ”, #{}`.
- Dùng `+` để cắt khi chuỗi quá dài. 
 
**Ví dụ:**
```
long_str = 'a very long long long long long long' + \n
           'long long long long string'
```
-----------------------------------------------------------------------------------------\n
[Tài liệu tham khảo](https://github.com/scrum2b/ruby-style-guide/blob/master/README-viVN.md)

**Nguyễn Quốc Kiện.**