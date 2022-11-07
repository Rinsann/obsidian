### vi 和 vim 编辑器
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107124123.png)
`Linux` 系统会内置 `vi` 文本编辑器。
`Vim` 具有程序编辑的能力，可以看做是`Vi`的增强版本，可以主动的以字体颜色辨别语法的正确性，方便程序设计，代码补完、编译及错误跳转等方便编程的功能特别丰富，在很多场景被广泛使用。

### vi 和 vim 常用的三种模式

**正常模式**
以 vim 打开一个文件就直接进入一般模式了（默认），在这个文件中，可以使用【上下左右】按键来移动光标，可以使用【删除字符】或【删除整行】来处理文件内容，也可以使用【复制、粘贴】来处理文件数据。

**插入模式**
按下 `i,I,o,O,a,A,r,R`等任何一个字母之后才会进入编辑模式，一般来说按 `i` 即可。

**命令行模式**
先按下 `Esc`键，然后输入`:`，就进入了命令行模式。在这个模式当中，可以输入你的相关命令。完成读取、存盘、替换、离开 `vim`、显示行号等动作。

### vi 和 vim 的基本使用
使用 `vim` 创建一个 `.java` 的程序
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107133317.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107133329.png)
敲完回车就会进入到这样一个界面，这里就是 `vim` 的一般模式，直接打字是没有用的，要先按 `i`进入插入模式才能输入。
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107133756.png)
写完了之后 按下 `Esc` 输入 `:wq`，代表保存并退出。![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107133853.png)重新编辑也只需要输入 `vim Hello.java` 即可！

### 各种模式切换
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/20221107134103.png)

### vi 和 vim 快捷键
**常用**
1. 拷贝当前行[ `yy`]，拷贝当前行向下的5行 [`5yy`]，并输入[`p`]粘贴
2. 删除当前行 [`dd`]，删除当前行向下的5行 [`5dd`]
3. 在文件中查找某个单词 【/+关键字进入命令行模式(/和:是不同的命令行模式)，回车查找，输入 `n` 就是查找下一个】
4. 设置文件的行号，取消文件的行号 .[命令行下 `:set nu` 和 `:set nonu`]
5. 编辑 `/etc/profile` 文件，使用快捷键到该文件最末行[`G`] 和 最行首 [`gg`]
6. 在一个文件中输入 "Hello"，然后又撤销这个动作 [`u`]
7. 编辑 `/etc/profile` 文件，并将光标移动到 20 行，输入20 +  [`shift+g`]

**快捷键图**
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/U3LMG%G4N9T4Y622ATG9TQW.png)
![](https://markdown-ft.oss-cn-shenzhen.aliyuncs.com/image-for-typora/vi-vim-cheat-sheet-sch1.gif)
