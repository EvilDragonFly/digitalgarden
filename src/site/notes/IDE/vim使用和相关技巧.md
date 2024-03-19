---
{"dg-publish":true,"permalink":"/IDE/vim使用和相关技巧/","noteIcon":"3"}
---


#vim
## 常用功能快捷键
set ts=4 sw=4
### 1. 高亮搜索

```bash
:set hlsearch
/hello
:nohlsearch
vim ~/.vimrc
set hlsearch

```

### 2.  复制粘贴

```bash
y
p
#粘贴缩进没有对齐时可以先设置如下再进行粘贴
:set paste

```

### 3. undo & redo

```bash
u
ctrl R
```
### 4.批量替换

```bash
:s/hello/hi/g
```

### 5.查看当前编码


```bash
:set encoding?
:set encoding=utf-8
# 查看文件编码
file -i filename
# 默认设置vim创建文件的编码
vim ~/.vimrc
# 比如当前encoding是latin，中文就会乱码，直接set encoding的话会恢复正常，但是编码不会保存，下次打开还是乱码
set encoding=utf-8
#保存文件使用指定编码
set fileencoding=utf-8
# 解决windows文件在linux乱码问题
set fileformat=unix
```

### 6.语法高亮
```bash
:syntax on
vim ~/.vimrc
syntax on

```
### 7.visual mode
```bash
# visual block mode
ctrl v
#visual line mode
v
# 批量缩进
进入visual block mode
按向下箭头选中需要缩进的行，点击I键，单击多个whitespace，esc
多行删除反缩进
空格处选中多行，点击x键，点击多次dot
```

### 8.打开文件直接进入某一行
```
vim file +155
```
### 9.批量注释，解注释
```javascript
// 开头添加#注释
:10,20s/^/#/g
:10,20s/#//g
//开头添加//注释
:10,20s#^#//#g
:10,20s#^//##g
```
## vim推荐配置
一些需要的插件需要下载安装:
```bash
git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

```bash
 
" 去掉有关vi一致性模式
set nocompatible
"显示行号
set number
"语法高亮
syntax on
"主题颜色
colorscheme desert
"tab缩进4个字符
set tabstop=4
"突出显示当前行
set cursorline
"自动缩进
set autoindent
"c/c++自动缩进
set cindent
 
 
" 映射切换buffer的键位(bp向前，bn向后)
nnoremap [[ :bp<CR>
nnoremap ]] :bn<CR>
" 映射<leader>num到num buffer
map <leader>1 :b 1<CR>
map <leader>2 :b 2<CR>
map <leader>3 :b 3<CR>
map <leader>4 :b 4<CR>
map <leader>5 :b 5<CR>
map <leader>6 :b 6<CR>
map <leader>7 :b 7<CR>
map <leader>8 :b 8<CR>
map <leader>9 :b 9<CR>
 
" 设置背景透明(有壁纸才有效果)
" hi Normal ctermfg=12 ctermbg=none
 
 
"""""   插件
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
filetype on                  " 必须要添加
" 设置包括vundle和初始化相关的runtime path
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" 另一种选择, 指定一个vundle安装插件的路径
"call vundle#begin('~/some/path/here')
 
" 让vundle管理插件版本,必须
Plugin 'VundleVim/Vundle.vim'
Plugin 'The-NERD-tree'
"NERDTree 配置:F2快捷键显示当前目录树
map <C-n> :NERDTreeToggle<CR>
let NERDTreeWinSize=25
 
Plugin 'taglist.vim'
""ctags 配置:F3快捷键显示程序中的各种tags，包括变量和函数等。
map <C-t> :TlistToggle<CR>
let Tlist_Use_Right_Window=1
let Tlist_Show_One_File=1
let Tlist_Exit_OnlyWindow=1
let Tlist_WinWidt=25
" 选中状态下 Ctrl+c 复制
vmap <C-c> "+y
" 改建
nnoremap H 0
nnoremap L $
nnoremap J 5j
nnoremap K 5k
 
Plugin 'vim-airline/vim-airline'
Plugin 'vim-airline/vim-airline-themes'
"vim-airline配置:优化vim界面"
"let g:airline#extensions#tabline#enabled = 1
"let g:airline_theme='simple'
" airline设置
" 显示颜色
set t_Co=256
" 永远显示状态栏
set laststatus=2
" 使用powerline打过补丁的字体
let g:airline_powerline_fonts = 1
" 开启tabline
let g:airline#extensions#tabline#enabled = 1
" tabline中当前buffer两端的分隔字符
let g:airline#extensions#tabline#left_sep = ' '
" tabline中未激活buffer两端的分隔字符
let g:airline#extensions#tabline#left_alt_sep = ' '
" tabline中buffer显示编号
let g:airline#extensions#tabline#buffer_nr_show = 1
" 你的所有插件需要在下面这行之前
call vundle#end()            " 必须
filetype plugin indent on    " 必须 加载vim自带和插件相应的语法和文件类型相关脚本

```
