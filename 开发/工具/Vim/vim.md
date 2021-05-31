gvim按照从上到下的形式进行配置文件查找, 一旦找到就不再继续向下查找配置文件

(在配置文件中写入source的会去额外加载的).

---

默认安装存在文件:

**第三用户 vimrc 文件** C:\Program Files (x86)\Vim\_vimrc

直接编辑这个文件就可以了.

---

因为我要写C, C++程序, 空格缩进8空格缩进, 真的是有点恼火:

```shell
set ai "设置自动缩进
set cindent "设置使用 C/C++ 语言的自动缩进方式
set shiftwidth=2 "设置自动缩进 2 个空格
set sts=4 "即设置 softtabstop 为 4. 输入 tab 后就跳了 4 格
set tabstop=4 "实际的 tab 即为 4 个空格, 而不是缺省的 8 个
set expandtab "在输入 tab 后, vim 用恰当的空格来填充这个 tab
```

经常发现会生成.un.~和.~文件, 如果你打开了显示隐藏文件和系统文件

```shell
set nobackup "不生成备份文件,FileName.~
set noundofile "不生成撤销文件,FileName.un.~
set fileencodings=utf-8,gbk,ucs-bom,cp936 "设置编码
set nocompatible "关闭 vi 兼容模式
```

---

设置行号和颜色

```shell
set number
color evening
```

---

如果使用`vim -u filename`命令来启动 Vim，则会用你指定的`filename`作为 Vim 的配置文件(在调试你的 vimrc 时有用)；如果用`vim -u NONE`命令启动 Vim，则不读取任何 vimrc 文件：当你怀疑你的 vimrc 配置有问题时，可以用这种方式跳过 vimrc 的执行。

