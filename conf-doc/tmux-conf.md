# tmux 工具
tmux 是一款终端复用命令行工具

具体的tmux的配置，可以参考对应的github中tmux的配置
## 开发机如何安装
1. 解决 tmux问题
老的机器安装tmux（yum没有），需要从源码编译。一般使用2.0版本的。
tmux，需要的libevent的版本比较高，但是目前开发机安装的都是1.4版本的。

2. 安装2.x版本的libevent
直接安装libevent的github指南安装

3. 启动tmux
启动tmux，会出现一些 os找不到的问题。

解决方法：

[https://github.com/liudf0716/apfree_wifidog/issues/73](https://github.com/liudf0716/apfree_wifidog/issues/73)

[https://blog.csdn.net/aoshilang2249/article/details/78366355](https://blog.csdn.net/aoshilang2249/article/details/78366355)

问题的原因可以通过 LD_DEBUG=libs  tmux

查看 tmux去哪里查找对应的lib文件，可以发现是在

```
3134504:   trying file=/lib64/tls/x86_64/libevent-2.1.so.7
   3134504:   trying file=/lib64/tls/libevent-2.1.so.7
   3134504:   trying file=/lib64/x86_64/libevent-2.1.so.7
   3134504:   trying file=/lib64/libevent-2.1.so.7
   3134504:   trying file=/usr/lib64/tls/x86_64/libevent-2.1.so.7
   3134504:   trying file=/usr/lib64/tls/libevent-2.1.so.7
   3134504:   trying file=/usr/lib64/x86_64/libevent-2.1.so.7
   3134504:   trying file=/usr/lib64/libevent-2.1.so.7
```

从而可以看下 lib64中是否存在，理论上是不存在的。那么就创建对应的 ln 过去。
ln -s /usr/local/lib/libevent-2.1.so.7 /usr/lib64/libevent-2.1.so.7

## 概念
session，会话：

window，窗口：

pane，窗格：

三个概念从大到小，是一个包含关系，会话可以有多个窗口，窗口可以有多个窗格。一般使用session和window的内容即可。
attach,detach：字面含义。用来attach到某个session，或者从某个session上detach。
快捷点前缀：C+b，这种快捷键相当于组合按键，首先需要按  C+b，然后输入对应的按键。后续使用prefix表示这个前缀按键。
## 使用
安装：linux，mac查阅网络即可
### session管理

1. 查看 session ： tmux ls
2. 关闭所有session：tmux kill-server
3. 关闭某个session：tmux kill-server -t name
4. 其从一个新的session：


	tmux
	
	这种方式 tmux session是默认按照数字排序的
	
	tmux ls
	
	0: 1 windows (created Thu Oct 10 23:08:34 2019)
	
	1: 2 windows (created Thu Oct 10 23:09:03 2019)
	
	tmux new -s  name
	
	session名字为 name

5. attach到需要的session上

	tmux  a
	
	attach到最近的session
	
	tmux a -t  name
	
	attach 到name session上
	
	在session中attach切换   prefix  + s

6. detach

7. prefix + d

### window使用
1. 创建一个窗口  prefix + c
2. list窗口  prefix + w
3. 数字切换窗口 prefix + number

### tmux 模式问题（后续补充）


### 特殊需求配置&常见问题
tmux.conf 文件配置可以参考，非常多的自定义命令:
https://jermine.vdo.pub/linux/终端利器tmux不止完美替换nohup--screen等进程守护命令/
鼠标滚屏问题

```
    # 开启鼠标模式
    set -g mode-mouse on
    # 允许鼠标选择窗格
    set -g mouse-select-pane on
    # 如果喜欢给窗口自定义命名，那么需要关闭窗口的自动命名
    set-option -g allow-rename off
    # 如果对 vim 比较熟悉，可以将 copy mode 的快捷键换成 vi 模式
    set-window-option -g mode-keys vi
```
## 鼠标复制问题
tmux 下开启鼠标滚屏后，复制文本有两种方式：

```
方法 1：使用 ⌃b z 进入窗格全屏模式，鼠标选择文本的同时按住 option 键 ⌥，然后使用 ⌘c 进行复制；

方法 2：开启 iTerm2 「在选择时复制」选项，即可实现自动选择复制。
```

### 复制问题解决
https://harttle.land/2015/11/06/tmux-startup.html

vim 模式的复制和tmux融合
## vim 模式操作tmux

[https://cizixs.com/2015/08/16/vi-mode-in-tmux/](https://cizixs.com/2015/08/16/vi-mode-in-tmux/)

## pane split

```
Ctrl+b " — split pane horizontally.
Ctrl+b % — split pane vertically.
Ctrl+b arrow key — switch pane.
Hold Ctrl+b, don’t release it and hold one of the arrow keys — resize pane.
Ctrl+b c — (c)reate a new window.
Ctrl+b n — move to the (n)ext window.
Ctrl+b p — move to the (p)revious window.
```
## plugins

[https://github.com/tmux-plugins](https://github.com/tmux-plugins)
