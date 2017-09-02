## Tip 1 Meet the Dot Command

==x== 命令能够删除当前光标的字符
当第一次输入==x==后再次，再次输入 ==.== 的话，会执行上次输入的命令

>点的作用就是记录上次输入的命令

==>G== 的命令可以对当前行到末尾行缩进

方向键

方向 | 按键
-----|-----
  上 | K
  下 | J
  左 | H
  右 | L
 
## Tip 2 Don't Repeat Yourself

合成命令 | 等价快速命令 | 意义
---------|------------  | ----
C        | c$           | 删除光标到末尾的内容
s        | cl           | 删除当前光标的内容并进入编辑状态
S        | ^C           | 删除光标所在行的内容并进入编辑
I        | ^i           | 光标移动到行首并进入编辑状态
A        | $a           | 光标移动到行末并进入编辑状态
o        | A<CR>        | 下方插入空行并进入编辑状态
O        | ko           | 上方插入空行并进入编辑状态

> ==$== 这个是将光标移动到行末，==^== 是将光标移动到行首

假设我们需要给每一行末尾添加分号“;”，那么最为快捷的编辑方法：

A;<Esc> -->> j -->> . -->> j.
```javascript
var foo = 1;
var bar = 'a';
var foobar = foo + bar;
```
## Tip 3 Take One Step Back, Then Three Forward

==s==命令的作用是删除光标的内容，并进入输入模式

实现内容：

```js
var​ foo = ​"method("​+argument1+​","​+argument2+​")"​;
```

到

```js
var​ foo = ​"method("​ + argument1 + ​","​ + argument2 + ​")"​;
```

命令的执行过程为：


f+ --> s空格+空格<Esc> --> ; --> . --> ;. --> ;.

>==f{char}== 的模式是匹配相应的char字符，并将光标移动到匹配的字符上，==;== 命令则是重复找到上次的匹配字符

>==t{char}== 的话则是移动到匹配字符的前面一个字符

>上面的两个匹配命令相应的换成大写就是向前匹配 ==F{char}== ==T{char}==

## Tip 4 Act, Repeat, Reverse 

### Table 1.Repeat Actions and How to Reverse Them
Intent | Act | Repeat | Reverse
-|-|-|-
Make a change | {edit} | . | u
Scan line for Next charater | f{char}/t{char} | ; | ,
Scan line for pre charater  | F{char}/T{char} | ; | ,
Scan document for next match | /pattern <CR> | n | N
Scan document for pre match  | ?pattern <CR> | n | N
Perform subsitution | :s/target/replacement | & | u
Execute a sequence of chcanges | qx{changes}q| @x |u

## Tip 5 Find and Replace by Hand

使用 ==:%s/content/copy/g== 这个命令的话则是直接将全文的 ==content== 替换为 ==copy== 

如果要分成步骤来完成这个过程的话使用如下的方式，光标移动到 ==content== 起始位置

==*== --->>> ==cw== copy ==<ESC>== --->>> ==n== --->>> ==.==

> ==*== 命令表示选择所有的content模式，并将光标移动到最后一个content的起始位置，==cw==命令表示删除该单词，并进入编辑模式，n表示重复*这个命令，.表示重复上次的编辑命令

## Tip 6 Compose Repeatable Changes

The method to delete the last word

=={start}== --->>> ==$== --->>> ==db== --->>> ==x==

=={start}== --->>> ==$== --->>> ==b== --->>> ==dw==

=={start}== --->>> ==$== --->>> ==daw== 

对于这三种方法，我们需要讨论最好的方式，在vim中应该尽量利用能够重复的原则，第一种方式中执行完成后，我们使用Dot Command(".")这个时候得到的最后一个命令 ==x==，同样对于第二种方式的话得到是==dw==，但是对于第三种方式我们得到的是整个命令==daw==，这样当我们使用Dot Command的时候就能够再次删除末尾的单词

Tip 7  Use Counts to Do Simple Arithmetic

==<C+a>== 和 ==<C+x>== 两个命令可以对数字进行操作，执行方式是同是按住==Ctrl== + ==x== 或者是 ==a== ，==a==的方式是增加数值的大小，==x==是减小数值的大小

> text:5  10<C+a> turn out: text:15

vim当中数字进制的设置是通过以下命令

> ==set nrformats==

## Tip 7 Don't Count If You Can Repeat 

删除两个单词的实现方式有两种：==d2w== 和==2dw== ，两种方式对应的解释在于==d2w==理解为delete two words，==2dw==理解为delete word two times.

另外一种方式是==dw.==，同样是也理解为delete word two times，但是这三种哪一种是最好的值得我们去了解

当我们在撤销也就是undo的时候，使用==u==命令，前面两种方式的话都会直接还原我们删除的两个单词，但是最后一种方式则是一个一个还原，这就是他们之前存在的差别。那么我们在实际使用中要使用哪一种方式呢，要根据实际的需求选择，但是如果有很多词汇需要数数的方式，还是使用==dw.......== 吧，==.== 的个数表示的就是删除的个数，使用这个的时候我们不需要去数数，但是也存在一个问题，如果删除的单词数很多，那我们就需要按下很多次的 ==.== 。









