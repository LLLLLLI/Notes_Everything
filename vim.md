# Vim 
内容主要来自慕课网 [玩转Vim：从放弃到爱不释手](https://www.imooc.com/learn/1129)  
Thanks To [PegasusWang](https://www.zhihu.com/people/pegasus-wang/activities)!
## insert模式
进入插入模式  
a append 在当前光标后插入 A 在行尾插入  
i insert 在当前光标前插入 I 在行首插入  
o 在下一行插入
### 删除
ctrl+h 删除上一个字符  
ctrl+w 删除上一个单词  
ctrl+u 删除当前行  
上述命令终端也适用  
其他终端命令  
ctrl+a 移动到行首  
ctrl+e 移动到行尾
### 切换normal与insert模式
normal模式下gi可以直接进入insert模式并跳转到上次编辑的位置
## normal模式
### 移动
hjkl  
w/W 移动到下一个word开头  
e/E 移动到下一个word结尾  
b/B 移动当上一个单词开头
#### 行间搜索移动
f{char} 移动到第一个char字符上 t移动到char前一个字符，;/,搜索下一个上一个
#### 水平移动
0 移动到行首第一个字符  
$ 移动到行尾  
^ 移动到第一个非空白字符
#### 页面移动
gg/G 移动到文件开头和结尾，ctrl+o快速返回  
zz 把当前行放到屏幕中间  
ctrl+u/f 上翻页和下翻页
### 删除
x 快速删除一个字符  
d 配合文本对象快速删除一个单词daw(d around word)  
dw 删除一个单词  
dt( 删除直到括号  
dd 删除一行  
d和x都可以搭配数字执行多次
### 修改
r(replace) 替换一个字符  
c(change) 配合文本对象 和删除的区别就是删除后进入插入模式  
caw 删除一个单词并进入插入模式  
ct) 删除到)并进入插入模式  
s(substitue) 删除当前字符并进入插入模式
### 查询
/或者? 前向和反向搜索  
n/N 跳转到下一个或上一个匹配  
\*或者# 当前单词前向和后向匹配
### 替换
:[range]s[ubstite]/{pattern}/{string}/[flags]  
range 表示范围 :10,20表示10-20行，%表示全部  
pattern 表示要替换的模式，支持正则表达式  
string 是替换后的文本  
Flags 替换标志为 g(global)全部替换 n(number) 只统计字数不替换  
示例  
:% s/self/this/g
## 多文件操作
#### Buffer
:ls 列举当前缓冲区  
:b n 跳转到第n个缓冲区  
:e filename 打开文件
#### Window
在多个窗口打开相同的buffer或不同的buffer  
:sp 上下分割  
:vs 左右分割  
Ctrl-w+w 窗口循环切换  
Ctrl-w+{hjkl}上下左右移动
#### Tab
将窗口分组  
不常用  
:tabnew filename 打开新tab  
gt 切换tab
## text object
[number][command][text object]  
dw w就是文本对象  
ci" 删除""里面的并进入插入模式  
ci( 删除()里面的并计入插入模式  
常用 c d v y
## 复制粘贴
### normal模式
y(ank) 复制 p(ut)粘贴 剪切d  
使用v命令选中要复制的地方，然后使用p粘贴
##### 配合文本对象使用
yiw 复制一个单词  
yy 复制一行
### Insert模式
解决insert模式下粘贴代码缩进错误  
粘贴前先  
:set paste 此时会取消自动缩进  
粘贴后  
:set nopaste 回复自动缩进
### 寄存器
通过"{register}指定寄存器 如："ayiw 复制一个单词到寄存器a中  
"+ 复制到系统剪贴板  
"+p 复制系统剪贴板到vim
## 宏（macro）
相当于函数，操作于每一行  
normal模式下使用q来录制，q结束录制，将命令放入寄存器中，使用q{register}指定寄存器  
@{register}回放命令  
shift-v 选中一行  
对全部文件进行操作  
先用shift-v然后G对进行全选  
然后输入命令（不退出visual模式）  
:normal @a 表示执行normal模式下的@a操作，即可文章对所有行操作
## 自动补全
ctrl-np 单词补全  
ctrl-xf 不全文件名  
ctrl-xo 依赖python-mode智能补全
## 美化
配色 hybrid  
状态栏 airline  
缩进线条 indentline
