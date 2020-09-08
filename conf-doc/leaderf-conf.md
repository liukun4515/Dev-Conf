## leaderF
用在vim中的一个fuzzy search 工具。相比FZF，其只用于VIM，不能用于本地的文本搜索。
## 需求
1. 模糊搜索文件
2. 按照关键字查找文件的内容（ define  symbol等）
3. 查找实现（通过定义查找，查找实现，一键式）
4. 查找引用（通过方法查找引用）
5. 查找全局、局部变量的使用/引用

## 配置leaderF
1. leaderF 非常好安装，可以直接按照官网教程（还有一个 performance 加速方式）
基本的leaderf只有 搜索  file，buffer，function等常用功能
2. 按照 ripgrep，可以使用rp搜索的结果
3. 结果gtags，可以使用global，gtags-cspose的方式来搜索内容。

## 如何选中光标所在的内容（tag）

## 在leaderf下如何使用gtags
https://github.com/Yggdroot/LeaderF/wiki/Leaderf-gtags  具体的配置内容。
使用介绍：直接使用官网给出的配置键，来使用

1. https://juejin.im/post/5cd032cc51882564083e0062

2. https://github.com/Yggdroot/LeaderF/wiki/Leaderf-gtags

快捷键与功能：

1. ctags ： 一种建立 tag的工具；vim中有插件来自动管理 tags的产生与存储位置；
如果没有使用自动管理tag的插件，就需要手动更新，产生tags文件，然后手动使用vim的时候载入tags文件。
有了这个以后，就可以在vim中进行函数或者宏定义的跳转。（但是OB项目太大，准确性不咋够）
2. cscope：使用前需要建立索引，把索引存储在数据库中（cscope组织的一种结构），并且提供了一个交互式的查找工具。
交互使用的结果。
https://www.cnblogs.com/litifeng/p/8448411.html  介绍了一些修改 scope功能的内容,比如修改scope的位置等等，以及取代tags的内容
快速使用：https://yiwenshao.github.io/2016/12/25/cscope快速教程/
3. gtags：安装的时候，会安装上对应的global，gtags-scope工具。
可以认为global是一个 非交互式的 gtags-scope。gtags-scope的功能和scope相同或者类似。
在使用vim的时候，可以通过修改vim的配置，来将 gtags产生的静态索引作为查询的数据库，也就是将scopse的使用换位 gtags-scope。
set cscopetag // 使用 cscope作为命令
set cscopeprg = gtags-scope
"gtags.vim 设置项，可以不设置，使用没什么问题
let GtagsCscope_Auto_Load = 1
let CtagsCscope_Auto_Map = 1
let GtagsCscope_Quiet = 1
理论上，可以直接在vim中，直接使用 Gtags或者cscopse的内容
## 重点其他内容
1. 不借助leaderf，自动配置gtags自动产生，gtags-cscopse搜索内容的方法：
https://zhuanlan.zhihu.com/p/36279445
## 原生ctags，gtags的功能与使用
### ctags
对内容原生创建好ctags以后，直接使用原生的ctags命令进行查找。
https://xu3352.github.io/linux/2018/12/16/practical-vim-skills-chapter-16
http://vimcdoc.sourceforge.net/doc/tagsrch.html#tagsrch.txt
