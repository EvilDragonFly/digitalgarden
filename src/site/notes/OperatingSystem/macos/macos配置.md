---
{"dg-publish":true,"permalink":"/OperatingSystem/macos/macos配置/","noteIcon":"3"}
---

#macos
1. macos键盘配置
设置page up page down terminal history macth
设置成功之后可以直接在terminal先输入命令前缀之后点击向上arrow就可以调出匹配的历史命令记录
![Pasted image 20230729125944.png|undefined](/img/user/pics/Pasted%20image%2020230729125944.png)

#keyboard #hotkey
## 直接terminal
mac终端默认到行首是ctrl A，行尾是ctrl E，fn <-和fn ->没有作用(离谱的设计)
如果想要像其他软件一样使用fn加方向键来navigate in terminal，需要设置terminal
这里设置了home(fn <-)和end(fn ->)会发送\\001(ctrl A)和\\005(ctrl E)到终端
![Pasted image 20240130233704.png|undefined](/img/user/Pasted%20image%2020240130233704.png)
home: fn + <-
end: fn + ->
## 如果是使用使用terminal登录到linux，
pageup :     shift + fn+ up
pagedown: shift + fn + down
home:         shift + fn + left
end:            shift + fn + right
## 在编辑器内如vscode内
home: command + left
end:    command +right
体验起来macos的键盘还有快捷键确实比win的差好多，对于自带的terminal登录到linux和不登录的快捷键和是不同的，且terminal和editor中的快捷键也不一样？？
3. 截屏快捷键
shift+command+5, ,之后选择截取的是当前window或者指定区域，如果在选择的时候不按住control键，截屏会自动保存在桌面，如果在选择的时候按住control键，截屏会保存到clipboard
5. 快速打开桌面
![Pasted image 20230808004913.png|undefined](/img/user/pics/Pasted%20image%2020230808004913.png)

## vscode添加code到系统路径
windows安装vscode会默认将code可执行文件添加到系统路径，但是在mac中需要额外执行命令添加code到系统路径从而实现直接terminal中输入code  path打开制定路径的项目

![Pasted image 20230906130054.png|undefined](/img/user/pics/Pasted%20image%2020230906130054.png)

vscode shortcut for mac
[[keyboard-shortcuts-macos.pdf]]
[shortcut](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)

mac高效率
快捷键
command H: 隐藏当前应用，比minimize更高效
option command H：隐藏其他应用，类似windows的抖动当前window快速隐藏其他windows，需要show all隐藏的应用的话可以点击当前应用左上角标识选择show all
commmand tab: 跳转到其他应用
command Q： 退出当前应用
shift command . :隐藏/显示设置为hidden的文件，文件夹或者app
隐藏文件或者文件夹
```bash
chflags hidden path
chflags nohidden path
```

### 切换shell
```bash
chsh -s bash
chsh -s zsh
```
