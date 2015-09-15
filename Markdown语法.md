## 区块元素
## 段落和换行
　　一个Markdown段落是由一个或多个连续的文本行组成，它的前后要有一个以上的空行，普通段落不该用空格或制表符来缩进。在插入处先按入两个以上的空格然后回车为换行。
### 标题
　　Markdown支持两种标题的语法Setext和atx形式，推荐使用Atx。它支持1～6个`#`，对应到标题1到6阶，例如：
```
# 这是H1
## 这是H2
###### 这是H6
```
　　也可以选择"闭合"形式，例如：
```
# 这是H1 #
## 这是H2 #
###### 这是H6 ######
```
### 区块引用 Blockquotes
　　Marddown标记区块引用使用`>`的引用方式：
```
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
> 
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.
```
结果表现为：
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
> 
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.

　　也可以偷懒的方式只在整个段落的第一行最前面加上`>`：
```
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.
```
　　区块可以嵌套，只要根据层次上加上不同的`>`：
```
> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.
```
结果表现为：
> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.

　　区块内也可以使用其他Markdown语法，如标题、列表、代码区块等：
```
> ## 这是一个标题。
> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
> 
>     return shell_exec("echo $input | $markdown_script");
```
结果表现为：
> ## 这是一个标题。
> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
> 
>     return shell_exec("echo $input | $markdown_script");

### 列表
Markdown 支持有序列表和无序列表。
1. 无序列表使用星号、加号或是减号作为列表标记：

```
*   Red
*   Green
*   Blue
```
等同于：
```
+   Red
+   Green
+   Blue
```
也等同于：
```
-   Red
-   Green
-   Blue
```
结果表现为：
*   Red
*   Green
*   Blue

. 有序列表则使用数字接着一个英文句点：

```
1.  Bird
2.  McHale
3.  Parish
```
结果表现为：
1.  Bird
2.  McHale
3.  Parish

列表项目标记通常是放在最左边，但是其实也可以缩进，最多 3 个空格，项目标记后面则一定要接着至少一个空格或制表符。
要让列表看起来更漂亮，你可以把内容用固定的缩进整理好：

如果列表项目间用空行分开，在输出 HTML 时 Markdown 就会将项目内容用`<p>`标签包起来，例如：
```
*   Bird
*   Magic
```
结果表现为：
*   Bird

*   Magic

列表项目可以包含多个段落，每个项目下的段落都必须缩进 4 个空格或是 1 个制表符：
```
1.  This is a list item with two paragraphs. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit. Aliquam hendrerit
    mi posuere lectus.

    Vestibulum enim wisi, viverra nec, fringilla in, laoreet
    vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
    sit amet velit.

2.  Suspendisse id sem consectetuer libero luctus adipiscing.
```
如果要在列表项目内放进引用，那 `>` 就需要缩进：
```
*   A list item with a blockquote:

    > This is a blockquote
    > inside a list item.
```
结果表现为：
*   A list item with a blockquote:

    > This is a blockquote
    > inside a list item.

如果要放代码区块的话，该区块就需要缩进两次，也就是 8 个空格或是 2 个制表符：
```
*   一列表项包含一个列表区块：

        <代码写在这>
```
结果表现为：
*   一列表项包含一个列表区块：
        <代码写在这>

### 代码区块
简单地缩进 4 个空格或是 1 个制表符就可以，例如：
```
这是一个普通段落：

    这是一个代码区块。
```
结果表现为：
这是一个普通段落：

    这是一个代码区块。

### 分隔线
可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。也可以在星号或是减号中间插入空格。
```
* * *

***

*****

- - -

---------------------------------------
```
结果表现为：
* * *

***

*****

- - -

---------------------------------------

### 区段元素
#### 链接
Markdown 支持两种形式的链接语法： 行内式和参考式两种形式。两种都用[方括号]来标记。
* 行内式
```
This is [百度](http://www.baidu.com/ "众里寻她千百度") inline link.
```
结果表现为：
This is [百度](http://www.baidu.com/ "众里寻她千百度") inline link.

* 参考式
```
[foo]: http://example.com/  "Optional Title Here"
```

#### 强调

```
*斜体*

_斜体_

**粗体**

__粗体__
```

结果表现为：
*single asterisks*

_single underscores_

**double asterisks**

__double underscores__

强调也可以直接插在文字中间：
```
un*frigging*believable**粗体**
```
结果表现为：
un*frigging*believable**粗体**

但是`*` 和 `_` 两边都有空白的话，它们就只会被当成普通的符号。

####代码
可用`来括起来：
```
Use the `printf()` function.
```
结果表现为：
Use the `printf()` function.

多行代码块可以多个反引号：
```
```
int main() {
    printf("%s\n", "hello world");
}
``````
结果表现为：
```
int main() {
    printf("%s\n", "hello world");
}
```

### 图片
有两种样式： 行内式和参考式

* 行内式

```
![Alt text](/path/to/img.jpg)

![Alt text](/path/to/img.jpg "Optional title")
```
* 参考式

```
[id]: url/to/image  "Optional title attribute"
```