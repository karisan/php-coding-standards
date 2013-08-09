Coding Style Guide
==================

This guide extends and expands on [PSR-1][], the basic coding standard.

The intent of this guide is to reduce cognitive friction when scanning code
from different authors. It does so by enumerating a shared set of rules and
expectations about how to format PHP code.

The style rules herein are derived from commonalities among the various member
projects. When various authors collaborate across multiple projects, it helps
to have one set of guidelines to be used among all those projects. Thus, the
benefit of this guide is not in the rules themselves, but in the sharing of
those rules.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[PSR-1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md


1. 概觀
-----------

- 程式碼必須遵循 [PSR-1][].

- 程式碼必須使用4個`空格`縮排，而非`tab`。

- 行的長度不須硬性限制，軟性限制必須是120個字元;行應該是80個字元或更少。

- `namespace`宣告後必須有一個空行，`use`宣告區塊後，必須有一個空行。

- `class`的開始大括號必須在下一行，結束大括號必須在內容後的下一行。

- `methods`的開始大括號必須在下一行，結束大括號必須在內容後的下一行。

- 可視性，即指 `public`, `protected`, 或 `private`，必須宣告於所有的 `properties` 和 `methods`;
  `abstract` 和 `final` 必須宣告在可視性之前; `static` 必須宣告在可視性之後。
  
- 控制結構的關鍵字後面必須有一個空格，`method`及`function`呼叫則不必。

- 控制結構的開始大括號必須在同一行上，結束大括號必須在內容後的下一行。

- 控制結構的開始大括號後面，不必有一個空格，控制結構的結束大括號之前，不必有一個空格

### 1.1. 範例

這個例子包含下面的規則，可以作為一個快速概述。:

```php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```

2. 一般原则
----------

### 2.1 基本編程標準

編程遵守 [PSR-1][].

### 2.2 檔案規則

所有PHP檔案，必須使用Unix LF換行符號。

所有PHP檔案，必須使用一個空白行作為結尾。

當檔案中只包含PHP程式，`?>` tag 必須省略。

### 2.3. Lines

並不需要嚴格限制每行長度。

軟性限制的每行長度為120個字元，自動化風格檢測程式必須提出警告，但不視為軟性限制錯誤。

每行不應超過80字元;行長於應分為​​多個後續行不超過80個字元。

每行末端不可附有多餘空格。

空行可能被添加，以提高可讀性，以利區分相關的程式碼區塊。

每行不可超過一個敘述。

### 2.4. 縮排

使用4個空格代替Tab

> N.b.: Using only spaces, and not mixing spaces with tabs, helps to avoid
> problems with diffs, patches, history, and annotations. The use of spaces
> also makes it easy to insert fine-grained sub-indentation for inter-line 
> alignment.

### 2.5. Keywords and True/False/Null

PHP [keywords][] 必須小寫。

PHP 內建常數 `true`, `false`, and `null` 必須小寫。.

[keywords]: http://php.net/manual/en/reserved.keywords.php



3. Namespace 及 Use 宣告
---------------------------------

在 `namespace` 宣告之後必須有一個空行。

所有 `use` 宣告必須在 `namespace` 宣告之後。

一個 `use` 關鍵字，對應一個宣告。

`use` 宣告區塊之後，必須有一個空白行

例如:

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...

```


4. Classes、Properties與Methods
-----------------------------------
 
該名詞 "class" 對應到所有的 classes、interfaces 和 traits。
 
 
### 4.1. Extends 與 Implements
 
`extends` 與 `implements` 之關鍵字必須宣告在與該class名稱同一行的位置。
 
該class所對應開始的大括號 `{` 必須在該class名稱下一行開始的位置上；接著從大括號那行的下一行才開始此class的主要程式碼。
 
```php
<?php
namespace Vendor\Package;
 
use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;
 
class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```
 
`implements` 的所有interface必須被分成多行宣告時，每一行都只能有一個interface，而當中的第一個interface必須由 `implements` 關鍵字的下一行開始。
 
```php
<?php
namespace Vendor\Package;
 
use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;
 
class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```
 
 
### 4.2. Properties
 
property命名時任何的存取修飾子(`private` 、 `protected` 與 `public`)必須要宣告出來。
 
不可使用關鍵字 `var` 在property的宣告上。
 
在同一行中不可宣告超過一個以上的property。
 
property的名稱命名不可以底線 `_` 開頭來表示 `protected` 或 `private`的存取修飾子。
 
一個property的宣告如下。
 
```php
<?php
namespace Vendor\Package;
 
class ClassName
{
    public $foo = null;
}
```
 
 
### 4.3. Methods
 
method命名時任何的存取修飾子(`private` 、 `protected` 與 `public`)必須要宣告出來。
 
method的名稱命名不可以底線 `_` 開頭來表示 `protected` 或 `private`的存取修飾子。
 
method的命名不可在該method名稱的後面接著一個空白 ` ` ，而該method所對應開始的大括號 `{` 必須在該method名稱下一行開始的位置上；接著從大括號那行的下一行才開始此method的主要程式碼，而在開始的圓括號 `(`　後面與在結束的 `)` 前面都不要使用一個空白 ` `。
 
一個method的宣告如下，注意圓括號 `()` 、逗號 `,` 、空白 ` ` 與大括號 `{}` 的位置：
 
```php
<?php
namespace Vendor\Package;
 
class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```   
 
 
### 4.4. Method的參數
 
若有多個參數，每個參數必須以一個逗號加空白如 `, ` 隔開，且在每個逗號前面不可有一個空白。
 
method參數的預設值必須在該參數宣告位置的後面
 
```php
<?php
namespace Vendor\Package;
 
class ClassName
{
    public function foo($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```
 
method的所有參數必須被分成多行宣告時，每一行都只能有一個參數，而當中的第一個參數必須由method名稱後 `(` 的下一行開始。
 
當參數被分成多行時，method結束的圓括號 `)` 與開始的大括號 `{` 必須宣告在獨立的一行，且兩者在同一行並在中間使用一個空白隔開。
 
```php
<?php
namespace Vendor\Package;
 
class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```
 
 
### 4.5. `abstract` 、 `final` 與 `static`
 
`abstract` 與 `final` 的宣告必須在存取修飾子的前面。
 
`static` 的宣告必須在存取修飾子的後面。
 
```php
<?php
namespace Vendor\Package;
 
abstract class ClassName
{
    protected static $foo;
 
    abstract protected function zim();
 
    final public static function bar()
    {
        // method body
    }
}
```
 
 
### 4.6. 呼叫Method與Function
 
當呼叫method或function時，在其名稱與開始的圓括號 `(` 中間不可以使用一個空白，而在開始的圓括號 `(` 後也不可以有一個空白，且在結束的圓括號 `)` 前面也不可以有一個空白，而在圓括號 `()` 中用於分隔每個參數的逗號如 `, ` 後面有一個空白而前面沒有空白。
 
```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```
 
method的所有參數必須被分成多行宣告時，每一行都只能有一個參數，而當中的第一個參數必須由method名稱後 `(` 的下一行開始。
 
```php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```
 
5. 控制結構
---------------------
 
一般的控制結構的程式碼寫作風格如下：
 
- 在控制結構的關鍵字宣告後必須有一個空白。
- 在開始的圓括號 `(` 後不可以有一個空白。
- 在結束的圓括號 `)` 前不可以有一個空白。
- 在結束的圓括號 `)` 與開始的大括號 `{` 中間必須有一個空白。
- 結構中的主要程式碼必須在上述的開始大括號 `{` 的下一行開始。
- 結束的大括號 `}` 必須在主要程式碼的下一行開始。
 
結構中的主要程式碼必須由大括號 `{}` 包覆，此標準的目的為避免在之後加入的程式碼被誤認為結構中的主要程式碼的一部分。
 
 
### 5.1. `if`, `elseif`, `else`
 
一個 `if` 結構的宣告如下，注意圓括號 `()` 、逗號 `,` 、空白 ` ` 與大括號 `{}` 的位置，而 `else` 與 `elseif` 的位置必須與上一個結構結束的大括號 `}` 同一行的位置。
 
```php
<?php
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```
 
必須使用關鍵字 `elseif` 取代 `else if` 使得所有的控制結構的關鍵字都只有一個字。
 
 
### 5.2. `switch`, `case`
 
一個 `switch` 結構的宣告如下，注意圓括號 `()` 、逗號 `,` 、空白 ` ` 與大括號 `{}` 的位置，而 `case` 關鍵字必須由`switch`名稱後 `{` 的下一行開始，而 `break` 關鍵字(或其它的中斷關鍵字)必須在 `case` 中的主要程式碼同一層，且在該 `case` 中沒有 `break` 時必須寫上 `// no break` 的註解。
 
```php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```
 
 
### 5.3. `while`, `do while`
 
一個 `while` 結構的宣告如下，注意圓括號 `()` 、逗號 `,` 、空白 ` ` 與大括號 `{}` 的位置。
 
```php
<?php
while ($expr) {
    // structure body
}
```
 
同樣地，一個 `do while` 結構的宣告如下，注意圓括號 `()` 、逗號 `,` 、空白 ` ` 與大括號 `{}` 的位置。
 
```php
<?php
do {
    // structure body;
} while ($expr);
```
 
### 5.4. `for`
 
一個 `for` 結構的宣告如下，注意圓括號 `()` 、逗號 `,` 、空白 ` ` 與大括號 `{}` 的位置。
 
```php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```
 
### 5.5. `foreach`
一個 `foreach` 結構的宣告如下，注意圓括號 `()` 、逗號 `,` 、空白 ` ` 與大括號 `{}` 的位置。
 
```php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
```
 
### 5.6. `try`, `catch`
 
一個 `try catch` 結構的宣告如下，注意圓括號 `()` 、逗號 `,` 、空白 ` ` 與大括號 `{}` 的位置。
 
```php
<?php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```

6. 匿名函数
-----------

宣告匿名函数必須於 `function` 後留一個空格，在 `use` 的前後各留一個空格。

開始大括號必須在同一行，而結束大括號必須在接在內容的下一行。

參數、變數列表的開始括號之後，不必留一個空格，參數、變數列表的結束括號之前，不必留一個空格。

參數、變數列表，每個逗號前不必留一個空格，但逗號之後，必須留一個空格。

有預設值的匿名函数參數，必須放在參數列表的最後。

匿名函数宣告如下所示。注意大括號，逗號，空格和括號的位置：

```php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```

參數和變量列表可以拆為多行，隨後的每一行縮排一次。這樣做時，列表中的第一項必須是下一行，每行必須只有一個參數或變數。

當拆為多行的（不論參數或變數）列表結束時，右括號、左大括號必須放在同一行，中間留一個空格 ` ) { ` 。

以下是匿名函数帶或不帶參數、變數列表，並拆為多行的例子。

```php
<?php
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
```

注意：格式化規則也可適用於匿名函数，當匿名函数直接使用一個 function 或 method call 作為參數時。

```php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```


7. 結論
--------------

有許多因素故意省略本指南的風格和實踐。這些包括但不限於：

- 全域變數和全域常數宣告

- 函數宣告

- 運算子和指派運算子

- 跨線對齊

- 註解和文檔區塊

- 類別名稱的前綴和後綴

- 最佳實例

未來建議可修改和延長本指南，以解決這些或其他元素的風格和實踐。


Appendix A. Survey
------------------

In writing this style guide, the group took a survey of member projects to
determine common practices.  The survey is retained herein for posterity.

### A.1. Survey Data

    url,http://www.horde.org/apps/horde/docs/CODING_STANDARDS,http://pear.php.net/manual/en/standards.php,http://solarphp.com/manual/appendix-standards.style,http://framework.zend.com/manual/en/coding-standard.html,http://symfony.com/doc/2.0/contributing/code/standards.html,http://www.ppi.io/docs/coding-standards.html,https://github.com/ezsystems/ezp-next/wiki/codingstandards,http://book.cakephp.org/2.0/en/contributing/cakephp-coding-conventions.html,https://github.com/UnionOfRAD/lithium/wiki/Spec%3A-Coding,http://drupal.org/coding-standards,http://code.google.com/p/sabredav/,http://area51.phpbb.com/docs/31x/coding-guidelines.html,https://docs.google.com/a/zikula.org/document/edit?authkey=CPCU0Us&hgd=1&id=1fcqb93Sn-hR9c0mkN6m_tyWnmEvoswKBtSc0tKkZmJA,http://www.chisimba.com,n/a,https://github.com/Respect/project-info/blob/master/coding-standards-sample.php,n/a,Object Calisthenics for PHP,http://doc.nette.org/en/coding-standard,http://flow3.typo3.org,https://github.com/propelorm/Propel2/wiki/Coding-Standards,http://developer.joomla.org/coding-standards.html
    voting,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,no,no,no,?,yes,no,yes
    indent_type,4,4,4,4,4,tab,4,tab,tab,2,4,tab,4,4,4,4,4,4,tab,tab,4,tab
    line_length_limit_soft,75,75,75,75,no,85,120,120,80,80,80,no,100,80,80,?,?,120,80,120,no,150
    line_length_limit_hard,85,85,85,85,no,no,no,no,100,?,no,no,no,100,100,?,120,120,no,no,no,no
    class_names,studly,studly,studly,studly,studly,studly,studly,studly,studly,studly,studly,lower_under,studly,lower,studly,studly,studly,studly,?,studly,studly,studly
    class_brace_line,next,next,next,next,next,same,next,same,same,same,same,next,next,next,next,next,next,next,next,same,next,next
    constant_names,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper
    true_false_null,lower,lower,lower,lower,lower,lower,lower,lower,lower,upper,lower,lower,lower,upper,lower,lower,lower,lower,lower,upper,lower,lower
    method_names,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel,lower_under,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel
    method_brace_line,next,next,next,next,next,same,next,same,same,same,same,next,next,same,next,next,next,next,next,same,next,next
    control_brace_line,same,same,same,same,same,same,next,same,same,same,same,next,same,same,next,same,same,same,same,same,same,next
    control_space_after,yes,yes,yes,yes,yes,no,yes,yes,yes,yes,no,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes
    always_use_control_braces,yes,yes,yes,yes,yes,yes,no,yes,yes,yes,no,yes,yes,yes,yes,no,yes,yes,yes,yes,yes,yes
    else_elseif_line,same,same,same,same,same,same,next,same,same,next,same,next,same,next,next,same,same,same,same,same,same,next
    case_break_indent_from_switch,0/1,0/1,0/1,1/2,1/2,1/2,1/2,1/1,1/1,1/2,1/2,1/1,1/2,1/2,1/2,1/2,1/2,1/2,0/1,1/1,1/2,1/2
    function_space_after,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no
    closing_php_tag_required,no,no,no,no,no,no,no,no,yes,no,no,no,no,yes,no,no,no,no,no,yes,no,no
    line_endings,LF,LF,LF,LF,LF,LF,LF,LF,?,LF,?,LF,LF,LF,LF,?,,LF,?,LF,LF,LF
    static_or_visibility_first,static,?,static,either,either,either,visibility,visibility,visibility,either,static,either,?,visibility,?,?,either,either,visibility,visibility,static,?
    control_space_parens,no,no,no,no,no,no,yes,no,no,no,no,no,no,yes,?,no,no,no,no,no,no,no
    blank_line_after_php,no,no,no,no,yes,no,no,no,no,yes,yes,no,no,yes,?,yes,yes,no,yes,no,yes,no
    class_method_control_brace,next/next/same,next/next/same,next/next/same,next/next/same,next/next/same,same/same/same,next/next/next,same/same/same,same/same/same,same/same/same,same/same/same,next/next/next,next/next/same,next/same/same,next/next/next,next/next/same,next/next/same,next/next/same,next/next/same,same/same/same,next/next/same,next/next/next

### A.2. Survey Legend

`indent_type`:
The type of indenting. `tab` = "Use a tab", `2` or `4` = "number of spaces"

`line_length_limit_soft`:
The "soft" line length limit, in characters. `?` = not discernible or no response, `no` means no limit.

`line_length_limit_hard`:
The "hard" line length limit, in characters. `?` = not discernible or no response, `no` means no limit.

`class_names`:
How classes are named. `lower` = lowercase only, `lower_under` = lowercase with underscore separators, `studly` = StudlyCase.

`class_brace_line`:
Does the opening brace for a class go on the `same` line as the class keyword, or on the `next` line after it?

`constant_names`:
How are class constants named? `upper` = Uppercase with underscore separators.

`true_false_null`:
Are the `true`, `false`, and `null` keywords spelled as all `lower` case, or all `upper` case?

`method_names`:
How are methods named? `camel` = `camelCase`, `lower_under` = lowercase with underscore separators.

`method_brace_line`:
Does the opening brace for a method go on the `same` line as the method name, or on the `next` line?

`control_brace_line`:
Does the opening brace for a control structure go on the `same` line, or on the `next` line?

`control_space_after`:
Is there a space after the control structure keyword?

`always_use_control_braces`:
Do control structures always use braces?

`else_elseif_line`:
When using `else` or `elseif`, does it go on the `same` line as the previous closing brace, or does it go on the `next` line?

`case_break_indent_from_switch`:
How many times are `case` and `break` indented from an opening `switch` statement?

`function_space_after`:
Do function calls have a space after the function name and before the opening parenthesis?

`closing_php_tag_required`:
In files containing only PHP, is the closing `?>` tag required?

`line_endings`:
What type of line ending is used?

`static_or_visibility_first`:
When declaring a method, does `static` come first, or does the visibility come first?

`control_space_parens`:
In a control structure expression, is there a space after the opening parenthesis and a space before the closing parenthesis? `yes` = `if ( $expr )`, `no` = `if ($expr)`.

`blank_line_after_php`:
Is there a blank line after the opening PHP tag?

`class_method_control_brace`:
A summary of what line the opening braces go on for classes, methods, and control structures.

### A.3. Survey Results

    indent_type:
        tab: 7
        2: 1
        4: 14
    line_length_limit_soft:
        ?: 2
        no: 3
        75: 4
        80: 6
        85: 1
        100: 1
        120: 4
        150: 1
    line_length_limit_hard:
        ?: 2
        no: 11
        85: 4
        100: 3
        120: 2
    class_names:
        ?: 1
        lower: 1
        lower_under: 1
        studly: 19
    class_brace_line:
        next: 16
        same: 6
    constant_names:
        upper: 22
    true_false_null:
        lower: 19
        upper: 3
    method_names:
        camel: 21
        lower_under: 1
    method_brace_line:
        next: 15
        same: 7
    control_brace_line:
        next: 4
        same: 18
    control_space_after:
        no: 2
        yes: 20
    always_use_control_braces:
        no: 3
        yes: 19
    else_elseif_line:
        next: 6
        same: 16
    case_break_indent_from_switch:
        0/1: 4
        1/1: 4
        1/2: 14
    function_space_after:
        no: 22
    closing_php_tag_required:
        no: 19
        yes: 3
    line_endings:
        ?: 5
        LF: 17
    static_or_visibility_first:
        ?: 5
        either: 7
        static: 4
        visibility: 6
    control_space_parens:
        ?: 1
        no: 19
        yes: 2
    blank_line_after_php:
        ?: 1
        no: 13
        yes: 8
    class_method_control_brace:
        next/next/next: 4
        next/next/same: 11
        next/same/same: 1
        same/same/same: 6
