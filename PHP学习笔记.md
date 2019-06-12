# PHP筆記

---

### PHP 是一门弱类型语言
PHP 会根据变量的值，自动把变量转换为正确的数据类型。

### PHP 变量规则：

- 变量以`$`符号开始，后面跟着变量的名称
-  变量名必须以字母或者下划线字符开始
- 变量名只能包含字母数字字符以及下划线（A-z、0-9 和 _ ）
- 变量名不能包含空格
- 变量名是区分大小写的（$y 和 $Y 是两个不同的变量）
- PHP 语句和 PHP 变量都是区分大小写的。

### 比较运算符
|例子|	名称|	结果|
|:--: |:--: |:--|
|\$a == \$b|	等于|	TRUE，如果类型转换后 \$a 等于 \$b。|
|\$a === \$b|	全等|	TRUE，如果 \$a 等于 \$b，并且它们的类型也相同。|
|\$a != \$b|	不等|	TRUE，如果类型转换后 \$a 不等于 \$b。|
|\$a <> \$b|	不等|	TRUE，如果类型转换后 \$a 不等于 \$b。|
|\$a !== \$b|	不全等|	TRUE，如果 \$a 不等于 \$b，或者它们的类型不同。|
|\$a < \$b	|小与|	TRUE，如果 \$a 严格小于 \$b。|
|\$a > \$b	|大于|	TRUE，如果 \$a 严格大于 \$b。|
|\$a <= \$b|	小于等于|	TRUE，如果 \$a 小于或者等于 \$b。|
|\$a >= \$b|	大于等于|	TRUE，如果 \$a 大于或者等于 \$b。|
|\$a <=> \$b|	太空船运算符（组合比较符）|	当\$a小于、等于、大于\$b时 分别返回一个小于、等于、大于0的integer 值。 PHP7开始提供.|
|\$a ?? \$b ?? \$c|	NULL 合并操作符|	从左往右第一个存在且不为 NULL 的操作数。如果都没有定义且不为 NULL，则返回 NULL。PHP7开始提供。|

### key
`key ( array $array ) : mixed`
返回数组中当前单元的键名。
**返回值：** key() 函数返回数组中内部指针指向的当前单元的键名。 但它不会移动指针。如果内部指针超过了元素列表尾部，或者数组是空的，key() 会返回 NULL。

### isset
isset — 检测变量是否已设置并且非 NULL
`isset ( mixed $var [, mixed $... ] ) : bool`

### define
define — 定义一个常量
`define ( string $name , mixed $value [, bool $case_insensitive = false ] ) : bool`
`name`:常量名。
`mixed`:说明一个参数可以接受多种不同的（但不一定是所有的）类型。
`value`:常量的值；在 PHP 5 中，value 必须是标量( integer、 float、string、boolean、NULL）在 PHP 7 中还允许是个 array 的值。
`case_insensitive`:**如果设置为TRUE，该常量则大小写不敏感**。默认是大小写敏感的。比如， CONSTANT 和 Constant 代表了不同的值。
Note:大小写不敏感的常量以小写的方式储存。
**返回值:**成功时返回 TRUE， 或者在失败时返回 FALSE。

```
<?php
define("CONSTANT", "Hello world.");
echo CONSTANT; // 输出 "Hello world."
echo Constant; // 输出 "Constant" 并导致 Notice

define("GREETING", "Hello you.", true);
echo GREETING; // 输出 "Hello you."
echo Greeting; // 输出 "Hello you."

//  PHP 7 起就可以运行了
define('ANIMALS', array(
    'dog',
    'cat',
    'bird'
));
echo ANIMALS[1]; // 输出 "cat"
?>
```

### mb_internal_encoding
`mb_internal_encoding ([ string $encoding = mb_internal_encoding() ] ) : mixed`
设置/获取内部字符编码
```
<?php
/* 设置内部字符编码为 UTF-8 */
mb_internal_encoding("UTF-8");

/* 显示当前的内部字符编码*/
echo mb_internal_encoding();
?>
```
### date_default_timezone_set
`date_default_timezone_set ( string $timezone_identifier ) : bool`
date_default_timezone_set() 设定用于所有日期时间函数的默认时区。
```
<?php
date_default_timezone_set('America/Los_Angeles');

$script_tz = date_default_timezone_get();

if (strcmp($script_tz, ini_get('date.timezone'))){
    echo 'Script timezone differs from ini-set timezone.';
} else {
    echo 'Script timezone and ini-set timezone match.';
}
?>
```
### ini_set
`ini_set ( string $varname , string $newvalue ) : string`
设置指定配置选项的值。这个选项会在脚本运行时保持新的值，并在脚本结束时恢复。
成功时返回旧的值，失败时返回 FALSE。
```
<?php
echo ini_get('display_errors');

if (!ini_get('display_errors')) {
    ini_set('display_errors', '1');
}

echo ini_get('display_errors');
?>
```
### in_array
`in_array ( mixed $needle , array $haystack [, bool $strict = FALSE ] ) : bool`
检查数组中是否存在某个值。
大海捞针，在大海（haystack）中搜索针（ needle），如果没有设置 strict 则使用宽松的比较。
如果找到 needle 则返回 TRUE，否则返回 FALSE。
```
<?php
$os = array("Mac", "NT", "Irix", "Linux");
if (in_array("Irix", $os)) {
    echo "Got Irix";
}
if (in_array("mac", $os)) {
    echo "Got mac";
}
?>
```
### list
`list ( mixed $var1 [, mixed $... ] ) : array`
把数组中的值赋给一组变量。
像 array() 一样，这不是真正的函数，而是语言结构。list()可以在单次操作内就为一组变量赋值。
返回指定的数组。
```
<?php
$info = array('coffee', 'brown', 'caffeine');

// 列出所有变量
list($drink, $color, $power) = $info;
echo "$drink is $color and $power makes it special.\n";

// 列出他们的其中一个
list($drink, , $power) = $info;
echo "$drink has $power.\n";

// 或者让我们跳到仅第三个
list( , , $power) = $info;
echo "I need $power!\n";

// list() 不能对字符串起作用
list($bar) = "abcde";
var_dump($bar); // NULL
?>
```

### intval
`intval ( mixed $var [, int $base = 10 ] ) : int`
获取变量的整数值。
通过使用指定的进制 base 转换（默认是十进制），返回变量 var 的 integer 数值。 intval() 不能用于 object，否则会产生 E_NOTICE 错误并返回 1。
```
<?php
echo intval(42);                      // 42
echo intval(4.2);                     // 4
echo intval('42');                    // 42
echo intval('+42');                   // 42
echo intval('-42');                   // -42
echo intval(042);                     // 34
echo intval('042');                   // 42
echo intval(1e10);                    // 1410065408
echo intval('1e10');                  // 1
echo intval(0x1A);                    // 26
echo intval(42000000);                // 42000000
echo intval(420000000000000000000);   // 0
echo intval('420000000000000000000'); // 2147483647
echo intval(42, 8);                   // 42
echo intval('42', 8);                 // 34
echo intval(array());                 // 0
echo intval(array('foo', 'bar'));     // 1
?>
```

### implode
`implode ( string $glue , array $pieces ) : string`
`implode ( array $pieces ) : string`
用 glue 将一维数组的值连接为一个字符串。
glue:默认为空的字符串。
pieces:你想要转换的数组。
返回一个字符串，其内容为由 glue 分割开的数组的值。
```
<?php
declare(strict_types=1);

$a = array( 'one','two','three' );
$b = array( '1st' => 'four', 'five', '3rd' => 'six' );

echo implode( ',', $a ),'/', implode( ',', $b );
?>
```
outputs: 
> one,two,three/four,five,six

### call_user_func
`call_user_func ( callable $callback [, mixed $parameter [, mixed $... ]] ) : mixed`
把第一个参数作为回调函数调用。
第一个参数 callback 是被调用的回调函数，其余参数是回调函数的参数。
```
<?php
error_reporting(E_ALL);
function increment(&$var)
{
    $var++;
}

$a = 0;
call_user_func('increment', $a);
echo $a."\n";

call_user_func_array('increment', array(&$a)); // You can use this instead before PHP 5.3
echo $a."\n";
?>
```
输出 
> 0
 1

### curl_setopt
`curl_setopt ( resource $ch , int $option , mixed $value ) : bool`
为 cURL 会话句柄设置选项。

ch:由 curl_init() 返回的 cURL 句柄。
option:需要设置的CURLOPT_XXX选项。
value:将设置在option选项上的值。
返回值:成功时返回 TRUE， 或者在失败时返回 FALSE。
```
<?php
#1 初始化一个新的cURL会话并获取一个网页
// 创建一个新cURL资源
$ch = curl_init();

// 设置URL和相应的选项
curl_setopt($ch, CURLOPT_URL, "http://www.example.com/");
curl_setopt($ch, CURLOPT_HEADER, false);

// 抓取URL并把它传递给浏览器
curl_exec($ch);

//关闭cURL资源，并且释放系统资源
curl_close($ch);
?>
```
> **CURLOPT_POSTFIELDS**
> 全部数据使用HTTP协议中的 "POST" 操作来发送。 要发送文件，在文件名前面加上@前缀并使用完整路径。 文件类型可在文件名后以 ';type=mimetype' 的格式指定。 这个参数可以是 urlencoded 后的字符串，类似'para1=val1&para2=val2&...'，也可以使用一个以字段名为键值，字段数据为值的数组。 如果value是一个数组，Content-Type头将会被设置成multipart/form-data。 从 PHP 5.2.0 开始，使用 @ 前缀传递文件时，value 必须是个数组。 从 PHP 5.5.0 开始, @ 前缀已被废弃，文件可通过 CURLFile 发送。 设置 CURLOPT_SAFE_UPLOAD 为 TRUE 可禁用 @ 前缀发送文件，以增加安全性。

|JSON| 函数|
|:--:|:--:| 
|函数|	描述|
|json_encode	|对变量进行 JSON 编码|
|json_decode|	对 JSON 格式的字符串进行解码，转换为 PHP 变量|
|json_last_error	|返回最后发生的错误|
```
<?php
   $arr = array('a' => 1, 'b' => 2, 'c' => 3, 'd' => 4, 'e' => 5);
   echo json_encode($arr);
?>
```
以上代码执行结果为：
> {"a":1,"b":2,"c":3,"d":4,"e":5}
```
<?php
   $json = '{"a":1,"b":2,"c":3,"d":4,"e":5}';

   var_dump(json_decode($json));
   var_dump(json_decode($json, true));
?>
```
以上代码执行结果为：
```
object(stdClass)#1 (5) {
    ["a"] => int(1)
    ["b"] => int(2)
    ["c"] => int(3)
    ["d"] => int(4)
    ["e"] => int(5)
}
array(5) {
    ["a"] => int(1)
    ["b"] => int(2)
    ["c"] => int(3)
    ["d"] => int(4)
    ["e"] => int(5)
}
```

### array_diff_key() 
`array_diff_key(array1,array2,array3...);`
函数用于比较两个（或更多个）数组的键名 ，并返回差集。
该函数比较两个（或更多个）数组的键名，并返回一个差集数组，该数组包括了所有在被比较的数组（array1）中，但是不在任何其他参数数组（array2 或 array3 等等）中的键名。
```
<?php
$a1=array("red","green","blue","yellow");
$a2=array("red","green","blue");

$result=array_diff_key($a1,$a2);
print_r($result);
?>
```
输出：
> Array ( [3] => yellow )

### array_flip() 
`array_flip(array);`
函数用于反转/交换数组中的键名和对应关联的键值。
```
<?php
$a1=array("a"=>"red","b"=>"green","c"=>"blue","d"=>"yellow");
$result=array_flip($a1);
print_r($result);
?>
```
输出: 
> Array ( [red] => a [green] => b [blue] => c [yellow] => d )


### string 相关函数：
`ucfirst()` - 函数把字符串中的首字符转换为大写。
`lcfirst()` - 把字符串中的首字符转换为小写
`strtolower()` - 把字符串转换为小写
`strtoupper()` - 把字符串转换为大写
`ucwords()` - 把字符串中每个单词的首字符转换为大写


### PHP Math 函数
|函数|	描述|	PHP|函数|	描述|	PHP|
|:--:|:--:|:--:|:--:|:--:|:--:|
|abs()|	绝对值。|	3|acos()|	反余弦。|	3|
|acosh()|	反双曲余弦。|	4|asin()|	反正弦。|	3|
|asinh()	|反双曲正弦。|	4|a|tan()|	反正切。|	3|
|atan2()	|两个参数的反正切。|	3|atanh()	|反双曲正切。|	4|
|base_convert()|	在任意进制之间转换数字。	3|bindec()|	把二进制转换为十进制。|	3|ceil()|	向上舍入为最接近的整数。|	3|
|cos()|	余弦。|	3|cosh()|	双曲余弦。|	4|
|decbin()|	把十进制转换为二进制。	|3|dechex()|	把十进制转换为十六进制。|	3|
|decoct()|	把十进制转换为八进制。|	3|deg2rad()|	将角度转换为弧度。|	3|
|exp()|	返回 Ex 的值。|	3|expm1()	|返回 Ex - 1 的值。|	4|
|floor()	|向下舍入为最接近的整数。|	3|fmod()|	返回除法的浮点数余数。|	4|
|getrandmax()|	显示随机数最大的可能值。|	3|hexdec()|	把十六进制转换为十进制。|	3|hypot()	|计算直角三角形的斜边长度。|	4|
|is_finite()	|判断是否为有限值。|	4|is_infinite()|	判断是否为无限值。|	4|
|is_nan()|	判断是否为合法数值。|	4|lcg_value()	|返回范围为 (0, 1) 的一个伪随机数。|	4|
|log()|	自然对数。	|3|log10()|	以 10 为底的对数。|	3|
|log1p()|	返回 log(1 + number)。|	4|max()	|返回最大值。|	3|
|min()|	返回最小值。|	3|mt_getrandmax()	|显示随机数的最大可能值。|	3|
|mt_rand()|	使用 Mersenne Twister 算法返回随机整数。|	3|mt_srand()|	播种 Mersenne Twister 随机数生成器。|	3|
|octdec()|	把八进制转换为十进制。|	3|pi()|	返回圆周率的值。|	3|
|pow()|	返回 x 的 y 次方。|	3|rad2deg()|	把弧度数转换为角度数。|	3|
|rand()	|返回随机整数。|	3|round()	|对浮点数进行四舍五入。|	3|
|sin()|	正弦。	|3|sinh()|	双曲正弦。|	4|
|sqrt()	|平方根。|	3|srand()	|播下随机数发生器种子。|	3|
|tan()|	正切。|	3|tanh()|	双曲正切。|	4|

### array_merge()
`array_merge(array1,array2,array3...)`
用于把一个或多个数组合并为一个数组。
提示：您可以向函数输入一个或者多个数组。
注释：如果两个或更多个数组元素有相同的键名，则最后的元素会覆盖其他元素。
注释：如果您仅仅向 array_merge()函数输入一个数组，且键名是整数，则该函数将返回带有整数键名的新数组，其键名以 0 开始进行重新索引（参见下面的实例 1）


## 类访问控制
类属性必须定义为公有，受保护，私有之一。如果用 var 定义，则被视为公有。
类中的方法可以被定义为公有，私有或受保护。如果没有设置这些关键字，则该方法默认为公有。
```
echo $obj->public; // 这行能被正常执行
echo $obj->protected; // 这行会产生一个致命错误
echo $obj->private; // 这行也会产生一个致命错误

$myclass->MyPublic(); // 这行能被正常执行
$myclass->MyProtected(); // 这行会产生一个致命错误
$myclass->MyPrivate(); // 这行会产生一个致命错误
```

在类的成员方法里面，可以用 `->`（对象运算符）：`$this->property`（其中 property 是该属性名）这种方式来访问非静态属性。静态属性则是用`::`（双冒号）：`self::$property` 来访问。

当一个方法在类定义内部被调用时，有一个可用的伪变量`$this`。`$this`是一个到主叫对象的引用（通常是该方法所从属的对象，但如果是从第二个对象静态调用时也可能是另一个对象）。

## extends
- 一个类可以在声明中用`extends`关键字继承另一个类的方法和属性。**PHP不支持多重继承，一个类只能继承一个基类。**
- 被继承的方法和属性可以通过用同样的名字重新声明被覆盖。但是如果父类定义方法时使用了 `final`，则该方法不可被覆盖。可以通过 `parent::`来访问被覆盖的方法或属性。
- 当覆盖方法时，参数必须保持一致否则PHP将发出`E_STRICT`级别的错误信息。但构造函数例外，构造函数可在被覆盖时使用不同的参数。

## 类的自动加载
不需要在每个脚本的开头，包含（include）一个长长的列表（每个类都有个文件）。
 `spl_autoload_register()`函数可以注册任意数量的自动加载器，当使用尚未被定义的类（class）和接口（interface）时自动去加载。通过注册自动加载器，脚本引擎在 PHP 出错失败前有了最后一个机会加载所需的类。

## 构造函数 
`__construct ([ mixed $args [, $... ]] ) : void`
Note: 如果子类中定义了构造函数则不会隐式调用其父类的构造函数。要执行父类的构造函数，需要在子类的构造函数中调用`parent::__construct()`。如果子类没有定义构造函数则会如同一个普通的类方法一样从父类继承（假如没有被定义为 private 的话）。

## 析构函数 
`__destruct ( void ) : void`
析构函数会在到某个对象的所有引用都被删除或者当对象被显式销毁时执行。
和构造函数一样，父类的析构函数不会被引擎暗中调用。要执行父类的析构函数，必须在子类的析构函数体中显式调用`parent::__destruct()`。此外也和构造函数一样，子类如果自己没有定义析构函数则会继承父类的。

析构函数即使在使用 `exit()`终止脚本运行时也会被调用。在析构函数中调用  `exit()` 将会中止其余关闭操作的运行。

## 抽象类
定义为抽象的类**不能被实例化**。**任何一个类，如果它里面至少有一个方法是被声明为抽象的，那么这个类就必须被声明为抽象的**。被定义为**抽象的方法**只是声明了其调用方式（参数），**不能定义其具体的功能实现**。

继承一个抽象类的时候，**子类必须定义父类中的所有抽象方法**；另外，**这些方法的访问控制必须和父类中一样（或者更为宽松）**。例如某个抽象方法被声明为受保护的，那么子类中实现的方法就应该声明为受保护的或者公有的，而不能定义为私有的。此外**方法的调用方式必须匹配，即类型和所需参数数量必须一致**。例如，子类定义了一个可选参数，而父类抽象方法的声明里没有，则两者的声明并无冲突。 这也适用于 PHP 5.4 起的构造函数。在 PHP 5.4 之前的构造函数声明可以不一样的。
### 范例
```
<?php
abstract class AbstractClass
{
 // 强制要求子类定义这些方法
    abstract protected function getValue();
    abstract protected function prefixValue($prefix);

    // 普通方法（非抽象方法）
    public function printOut() {
        print $this->getValue() . "\n";
    }
}

class ConcreteClass1 extends AbstractClass
{
    protected function getValue() {
        return "ConcreteClass1";
    }

    public function prefixValue($prefix) {
        return "{$prefix}ConcreteClass1";
    }
}

class ConcreteClass2 extends AbstractClass
{
    public function getValue() {
        return "ConcreteClass2";
    }

    public function prefixValue($prefix) {
        return "{$prefix}ConcreteClass2";
    }
}

$class1 = new ConcreteClass1;
$class1->printOut();
echo $class1->prefixValue('FOO_') ."\n";

$class2 = new ConcreteClass2;
$class2->printOut();
echo $class2->prefixValue('FOO_') ."\n";
?>
```
以上例程会输出：
> ConcreteClass1
FOO_ConcreteClass1
ConcreteClass2
FOO_ConcreteClass2

```
<?php
abstract class AbstractClass
{
    // 我们的抽象方法仅需要定义需要的参数
    abstract protected function prefixName($name);

}

class ConcreteClass extends AbstractClass
{

    // 我们的子类可以定义父类签名中不存在的可选参数
    public function prefixName($name, $separator = ".") {
        if ($name == "Pacman") {
            $prefix = "Mr";
        } elseif ($name == "Pacwoman") {
            $prefix = "Mrs";
        } else {
            $prefix = "";
        }
        return "{$prefix}{$separator} {$name}";
    }
}

$class = new ConcreteClass;
echo $class->prefixName("Pacman"), "\n";
echo $class->prefixName("Pacwoman"), "\n";
?>
```
以上例程会输出：
> Mr. Pacman
Mrs. Pacwoman


## 对象接口
使用接口（interface），可以指定某个类必须实现哪些方法，但不需要定义这些方法的具体内容。

接口是通过 `interface`关键字来定义的，就像定义一个标准的类一样，但其中定义所有的方法都是空的。

接口中定义的所有方法都必须是公有，这是接口的特性。
### 实现（implements）
要实现一个接口，使用 `implements`操作符。

Note:实现多个接口时，接口中的方法不能有重名。
Note:接口也可以继承，通过使用 `extends` 操作符。
Note:类要实现接口，必须使用和接口中所定义的方法完全一致的方式。否则会导致致命错误。

### 范例
```
<?php
// 声明一个'iTemplate'接口
interface iTemplate
{
    public function setVariable($name, $var);
    public function getHtml($template);
}


// 实现接口
// 下面的写法是正确的
class Template implements iTemplate
{
    private $vars = array();
  
    public function setVariable($name, $var)
    {
        $this->vars[$name] = $var;
    }
  
    public function getHtml($template)
    {
        foreach($this->vars as $name => $value) {
            $template = str_replace('{' . $name . '}', $value, $template);
        }
 
        return $template;
    }
}

// 下面的写法是错误的，会报错，因为没有实现 getHtml()：
// Fatal error: Class BadTemplate contains 1 abstract methods
// and must therefore be declared abstract (iTemplate::getHtml)
class BadTemplate implements iTemplate
{
    private $vars = array();
  
    public function setVariable($name, $var)
    {
        $this->vars[$name] = $var;
    }
}
?>
```

## Static（静态）关键字
- 声明类属性或方法为静态，就可以不实例化类而直接访问。**静态属性不能通过一个类已实例化的对象来访问（但静态方法可以）**。
- 如果没有指定访问控制，属性和方法默认为公有。
- 由于静态方法不需要通过对象即可调用，所以伪变量 $this 在静态方法中不可用。
- 静态属性不可以由对象通过 -> 操作符来访问。
- 用静态方式调用一个非静态方法会导致一个 E_STRICT 级别的错误。
- 就像其它所有的PHP静态变量一样，静态属性只能被初始化为文字或常量，不能使用表达式。所以可以把静态属性初始化为整数或数组，但不能初始化为另一个变量或函数返回值，也不能指向一个对象。
- 可以用一个变量来动态调用类。但该变量的值不能为关键字 `self`，`parent` 或 `static`。
### 范例
```
<?php
class Foo
{
    public static $my_static = 'foo';

    public function staticValue() {
        return self::$my_static;
    }
}

class Bar extends Foo
{
    public function fooStatic() {
        return parent::$my_static;
    }
}


print Foo::$my_static . "\n";

$foo = new Foo();
print $foo->staticValue() . "\n";
print $foo->my_static . "\n";      // Undefined "Property" my_static 

print $foo::$my_static . "\n";
$classname = 'Foo';
print $classname::$my_static . "\n"; // As of PHP 5.3.0

print Bar::$my_static . "\n";
$bar = new Bar();
print $bar->fooStatic() . "\n";
?>
   </programlisting>
  </example>

  <example>
   <title>静态方法示例</title>
    <programlisting role="php">
<![CDATA[
<?php
class Foo {
    public static function aStaticMethod() {
        // ...
    }
}

Foo::aStaticMethod();
$classname = 'Foo';
$classname::aStaticMethod(); // 自 PHP 5.3.0 起
?>
```


## Final 关键字
如果父类中的方法被声明为 `final`，则子类无法覆盖该方法。如果一个类被声明为 `final`，则不能被继承。
Note: 属性不能被定义为 final，**只有类和方法才能被定义为 final**。
### 范例
```
<?php
class BaseClass {
   public function test() {
       echo "BaseClass::test() called\n";
   }
   
   final public function moreTesting() {
       echo "BaseClass::moreTesting() called\n";
   }
}

class ChildClass extends BaseClass {
   public function moreTesting() {
       echo "ChildClass::moreTesting() called\n";
   }
}
// Results in Fatal error: Cannot override final method BaseClass::moreTesting()
?>
```

```
<?php
final class BaseClass {
   public function test() {
       echo "BaseClass::test() called\n";
   }
   
   // 这里无论你是否将方法声明为final，都没有关系
   final public function moreTesting() {
       echo "BaseClass::moreTesting() called\n";
   }
}

class ChildClass extends BaseClass {
}
// 产生 Fatal error: Class ChildClass may not inherit from final class (BaseClass)
?>
```

## new self()和new static()
1. new self()和new static()的区别只有在继承中才能体现出来，如果没有任何继承，那么这两者是没有区别的。
2. 在继承中，new self()返回的实例是万年不变的，无论谁去调用，都返回同一个类的实例，而new static()则是由调用者决定的。
```
//无继承
class Father
{

    public function useSelf()
    {
        return new self();
    }

    public function useStatic()
    {
        return new static();
    }

}

$f = new Father();

echo get_class($f->useSelf())."\n";//  输出  Father
echo get_class($f->useStatic())."\n";//  输出  Father
```

```
//有继承
class Sun extends Father
{

}
$sun = new Sun();

echo get_class($sun1->useSelf())."\n";     //  输出  Father
echo get_class($sun1->useStatic())."\n";  //  输出  Sun
```



