<div dir="rtl">

## ضمیمه‌ی «الف»: کلمات کلیدی

لیست زیر حاوی کلماتی کلیدی است که برای استفاده در نسخه‌ی فعلی یا در نسخه‌های آینده‌ی زبان برنامه‌نویسی Rust رزرو شده
است. به همین دلیل نمی‌توان این کلمات را به عنوان شناسه (مگر در شناسه‌های خام که در
بخش [Raw Identifiers][raw-identifiers] بحث خواهیم کرد)، در توابع، متغیرها، پارامترها، زمینه‌های ساختاری، ماژول‌ها،
کریت‌ها (crates)، مقادیر ثابت، ماکروها، مقادی استاتیک، صفات (attributes)، انواع داده‌ها، خصیصه‌ها (traits) و یا طول
عمرها (lifetimes) استفاده کرد.

[raw-identifiers]: #raw-identifiers

### کلمات کلیدی رزرو شده‌ی فعلی

عملکرد کلمات کلیدی ذکر شده توضیح داده شده است.

* `as` - اجرای ریخته‌گری اولیه (primitive casting)، جداسازی خصیصه‌ای خاص شامل یک آیتم، یا تغییر نام آیتم‌ها در دستورالعمل‌های `use` و `extern crate`
* `async` - برگرداندن یک `Future` به جای بستن رشته‌ی فعلی
* `await` - تعلیق اجرا تا زمان آماده شدن نتیجه‌ی یک `Future`
* `break` - خروج فوری از یک حلقه
* `const` - تعریف آیتم‌ها با مقدار ثابت یا نشانگرهای خام ثابت
* `continue` - ادامه به تکرار بعدی حلقه
* `crate` - اتصال یک کریت (crate) خارجی یا متغیر ماکرو که نشان‌دهنده‌ی کریتی‌ست که ماکرو در آن تعریف شده است.
* `dyn` - اعزام دینامیک به یک آبجکت خصیصه
* `else` - فال‌بک (fallback) برای ساختارهای کنترل جریان `if` و `if let`
* `enum` - تعریف یک شمارش
* `extern` - پیوند یک کریت، تابع یا متغیر خارجی
* `false` - معنای لفظی `نادرست` بولی
* `fn` - تعریف یک تابع یا نوع نشانگر تابع
* `for` - برای تکرار حلقه روی موارد یک نشانگر (مثلا یک لیست)، بکارگیری یک خصیصه یا تعیین طول عمر با رتبه‌ی بالاتر استفاده می‌شود
* `if` - شاخه‌ای بر اساس نتیجه‌ی یک عبارت شرطی
* `impl` - پیاده‌سازی عملکرد ذاتی یا خصیصه‌ای
* `in` - قسمتی از دستور حلقه‌ی `for`
* `let` - اتصای یک متغیر
* `loop` - حلقه‌ی بدون شرط
* `match` - تطابق یک مقدار با الگوها
* `mod` - تعریف یک ماژول
* `move` - دادن مالکیت تمام کپچرها (capture) به یک بستار (closure)
* `mut` - denote mutability in references, raw pointers, or pattern bindings
* `pub` - denote public visibility in struct fields, `impl` blocks, or modules
* `ref` - bind by reference
* `return` - return from function
* `Self` - a type alias for the type we are defining or implementing
* `self` - method subject or current module
* `static` - global variable or lifetime lasting the entire program execution
* `struct` - define a structure
* `super` - parent module of the current module
* `trait` - define a trait
* `true` - Boolean true literal
* `type` - define a type alias or associated type
* `union` - define a [union] and is only a keyword when used in a union declaration
* `unsafe` - denote unsafe code, functions, traits, or implementations
* `use` - bring symbols into scope
* `where` - denote clauses that constrain a type
* `while` - loop conditionally based on the result of an expression

[union]: ../reference/items/unions.html

### Keywords Reserved for Future Use

The following keywords do not have any functionality but are reserved by Rust for potential future use.

* `abstract`
* `become`
* `box`
* `do`
* `final`
* `macro`
* `override`
* `priv`
* `try`
* `typeof`
* `unsized`
* `virtual`
* `yield`

### Raw Identifiers

*Raw identifiers* are the syntax that lets you use keywords where they wouldn’t normally be allowed. You use a raw
identifier by prefixing a keyword with `r#`.

For example, `match` is a keyword. If you try to compile the following function that uses `match` as its name:

<span class="filename">Filename: src/main.rs</span>

```rust,ignore,does_not_compile
fn match(needle: &str, haystack: &str) -> bool {
    haystack.contains(needle)
}
```

you’ll get this error:

```text
error: expected identifier, found keyword `match`
 --> src/main.rs:4:4
  |
4 | fn match(needle: &str, haystack: &str) -> bool {
  |    ^^^^^ expected identifier, found keyword
```

The error shows that you can’t use the keyword `match` as the function identifier. To use `match` as a function name,
you need to use the raw identifier syntax, like this:

<span class="filename">Filename: src/main.rs</span>

```rust
fn r#match(needle: &str, haystack: &str) -> bool {
    haystack.contains(needle)
}

fn main() {
    assert!(r#match("foo", "foobar"));
}
```

This code will compile without any errors. Note the `r#` prefix on the function name in its definition as well as where
the function is called in `main`.

Raw identifiers allow you to use any word you choose as an identifier, even if that word happens to be a reserved
keyword. In addition, raw identifiers allow you to use libraries written in a different Rust edition than your crate
uses. For example, `try` isn’t a keyword in the 2015 edition but is in the 2018 edition. If you depend on a library
that’s written using the 2015 edition and has a `try` function, you’ll need to use the raw identifier syntax, `r#try` in
this case, to call that function from your 2018 edition code. See [Appendix E][appendix-e]<!-- ignore --> for more
information on editions.

[appendix-e]: appendix-05-editions.html
</div>