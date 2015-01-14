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

###1. attributes

+ i 忽略大小写(ignoreCase)
+ g 全部匹配(globle)
+ m 多行匹配(multiline)

三个属性可以任意组合。

###2. pattern

