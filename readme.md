RegExp in JavaScript
====

一、相关 API
----

###1. Object RegExp

[RegExp](https://github.com/LearnShare/blog/blob/master/posts/drafts/javascript/js_object-regexp.md)

###2. Object String

[String](https://github.com/LearnShare/blog/blob/master/posts/drafts/javascript/js_object-string.md)

二、使用
----

###1. 创建

直接量

`/` pattern `/` attributes

	/abc/ig

创建对象

`new RegExp(` pattern `,` attributes `)`

	new RegExp("abc", "ig");

attributes:

+ i 忽略大小写(ignoreCase)
+ g 全部匹配(globle)
+ m 多行匹配(multiline)

三个属性可以任意组合。

###2. 使用

Object RegExp

	// 寻找 string 中所有匹配的结果，以数组返回
	regexp.exec(string);
	// 测试 string 是否匹配
	regexp.test(string);

Object String

	// 寻找 string 中所有匹配的结果，以数组返回
	string.match(regexp);
	// 寻找 string 中所有匹配的结果，并替换为指定内容
	string.replace(regexp, newString);
	// 寻找 string 中第一个匹配结果的位置
	string.search(regexp);

三、 语法
----

+ [MDN: RegExp](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
+ [Adobe: RegExp](http://help.adobe.com/zh_CN/as3/dev/WS5b3ccc516d4fbf351e63e3d118a9b90204-7ea9.html)
+ [MSDN: RegExp](http://msdn.microsoft.com/zh-cn/library/vstudio/ae5bf541(v=vs.100).aspx)
+ [Wiki: RegExp](http://zh.wikipedia.org/wiki/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)

###1. 字符和序列

#### ① 字符和序列

`/a/` 可以匹配 `abc` 中的字符 `a`。

`/abc/` 可以匹配 `abcdefg` 中的序列 `abc`。

#### ② 元字符

`^ $ \ / . * + - ? ( ) [ ] { } |` 在 pattern 中有特殊含义，称为 **元字符**。

+ `^` 匹配行的开头。如果设置了 `m` 属性，则会匹配每一行的开始位置；
+ `$` 匹配行的结尾。如果设置了 `m` 属性，则会匹配每一行的结尾位置；
+ `\` `\` 与元字符组合，会取消元字符的特殊含义，而变成普通字符：`/\\a/` 可以匹配 `\a\b\c` 中的 `\a`；`\` 与特定字符组合成 **元序列**；
+ `/` 是正则表达式直接量的 pattern 部分开始和结束的标记；
+ `.` 代表任意单个字符，但换行符除外（`\n`、`\r`）；
+ `*` 代表 pattern 片段匹配 >= 0 次：`/ab*c/g` 匹配 `acabcdaabbccdd` 中的 `ac` `abc` 和 `abbc`；
+ `+` 代表 pattern 片段匹配 >= 1 次：`/ab+c/g` 匹配 `acabcdaabbccdd` 中的 `abc` 和 `abbc`；
+ `-` 用于指定集合中字符的范围：`[abc]` 等价于 `[a-c]`；
+ `?` 代表 pattern 片段匹配 0 或 1 次：`/ab?c/g` 匹配 `acabcdaabbccdd` 中的 `ac` 和 `abc`；
+ `(` 和 `)` 用于对 pattern 中的片段进行分组；
+ `[` 和 `]` 用于声明字符集合；
+ `{` 和 `}` 用于声明 pattern 片段的数量；
+ `|` 表示或：`/ab|de/g` 可以匹配 `abcdefg` 中的 `ab` 和 `de`。

如果需要在 pattern 中包含元字符的字符，需要在该字符前加 `\`，将该字符标记为特殊字符。

#### ③ 元序列

`\d \s` 等字符组合在 pattern 中代表了特定的字符，称之为 **元序列**。

+ `\d` 代表拉丁数字字符(0~9)，与 `[0-9]` 等价；
+ `\D` 代表任意非拉丁数字字符，与 `[^0-9]` 等价；
+ `\w` 代表任意拉丁字母、数字和下划线(`_`)，与 `[A-Za-z0-9_]` 等价；
+ `\W` 代表任意非拉丁字母、数字或下划线(`_`)，与 `[^A-Za-z0-9_]` 等价；
+ `\s` 代表任意空白符（``）；
+ '\S' 代表任意非空白符。
+ `\b` 匹配字符和空白符之间的边界，比如 `/\ba/` 可以匹配 `abc a b cabc` 中的前两个 'a'，因为它们的左侧是空白符；
+ `\B` 匹配字符之间或空白符之间的边界，比如 `/\Ba/` 可以匹配 `abc a b cabc` 中的第三个 'a'，因为它的左侧是字符。

空白符

+ `\t` 水平制表符(`tab`)；
+ `\r` 回车换行(`enter`)；
+ `\n` 换行；
+ `\v` 垂直制表符；
+ `\f` 换页符；
+ `\0` NUL 字符；
+ `[\b]` 退格符(`backspace`)。

###2. 集合

`[abc]` 代表字符集合，会匹配包含在 `[]` 中的所有字符；`[^abc]` 则匹配任何不含在 `[]` 中字符。

+ `/[abc]/` 可以匹配 `a b c d e` 中的 `a` `b` 和 `c`；
+ `/[^abc]/` 可以匹配 `a b c d e` 中的 `d` 和 `e`；
+ `/[a-c]/` 等价于 `[abc]`，`a-c` 代表了从 `a` 到 `c` 的所有字符；
+ `/^[a-c]/` 等价于 `[^abc]` 代表了所有不在 `a` 到 `c` 中的字符。

###3. 数量

+ `*` 参考前面的内容；
+ `+` 参考前面的内容；
+ `?` 参考前面的内容；
+ `a*?` 执行类似 `*` 的匹配，但只匹配最小的结果；
+ `a+?` 执行类似 `+` 的匹配，但只匹配最小的结果；
+ `a{n}` 匹配片段 `a` n 次；
+ `a{n,}` 匹配片段 `a` >= n 次；
+ `a{n,m}` 匹配片段 `a` n 至 m 次，n <= m；

###4. 条件

+ `|` 参考前面的内容；
+ `a(?=b)` 只匹配后面紧跟着 `b` 的 `a`；
+ `a(?!b)` 只匹配后面没有紧跟着 `b` 的 `a`；

###5. 优先级

优先级从高到低：

+ `\`
+ `( ) (?:) (?=) [ ]`
+ `* + ? {n} {n,} {n,m}`
+ `^ $ 元字符`
+ `|`

四、实例
----

###1. IPv4

x.x.x.x x: (0~255)

x: 

+ 250~255: `25[0-5]`
+ 200~249: `2[0-4]\d`
+ 0~99、10~199 `1?\d{1,2}`

-> `(25[0-5])|(2[0-4]\d)|(1?\d{1,2})`

error: `/^((25[0-5])|(2[0-4]\d)|(1?\d{1,2})\.){3}((25[0-5])|(2[0-4]\d)|(1?\d{1,2}))$/gm`

tests:

	0.0.0.0
	1.1.1.1
	10.10.10.10
	134.134.134.134
	200.200.200.200
	255.255.255.255
	255.255.255.256
	255.256.255.255

reg: `/^(((25[0-5])|(2[0-4]\d)|(1?\d{1,2}))\.){3}((25[0-5])|(2[0-4]\d)|(1?\d{1,2}))$/gm`

###2. Email

xxx@xx.xx

+ xxx: (A~Z/a~z/0~9/./_/-)
+ xx: any sub domain
+ x: top domain (A~Z/a~z >= 2)

###3. Domain

xxx.xx

###4. URL

xxxx://xxx.xx/x