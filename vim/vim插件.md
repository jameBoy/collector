## VIM插件

### Makedowm 插件

**vim-markdown插件**

vim-markdown插件 插件负责vim里编辑时语法高亮

使用bundle管理插件安装：

```
" Markdown 插件                                                                                                                                  
Plugin 'godlygeek/tabular'
Plugin 'plasticboy/vim-markdown'
```

**如用vundle管理插件，那么godlygeek/tabular这个插件必须在plasticboy/vim-markdown之前**

保存后，执行：BundleInstall安装插件即可

安装完后，可以打开vim 发现语法是否高亮

![](http://7xkx71.com1.z0.glb.clouddn.com/vim_md_1.png)


**实时预览插件**

因为看了几个实时预览插件发现不太满意，所以使用了曲线救国的方式：

chrome有个插件能够预览markdown文件，[Markdown Preview Plus](https://chrome.google.com/webstore/detail/markdown-preview-plus/febilkbfcbhebfnokafefeacimjdckgl)
此插件在github上的地址是:[markdown-preview](https://github.com/volca/markdown-preview)


#### 使用方法

+ 从chrome的webstore安装Markdown Preview Plus插件
+ 打开chrome://extensions/，在设置页中勾选 “允许访问文件网址”
+ 在chrome中打开本地markdown文件，http/https也是可以支持的
+ 你会看到已经转换成html的内容


在chrome中打开markdown文件，用vim编辑markdown，保存后页面就会自动刷新，实现预览。虽然不像一些工具一样是实时的，但是保存后再预览，这样我觉得也挺好。再在vimrc中加入以下内容：

```
autocmd BufRead,BufNewFile *.{md,mdown,mkd,markdown,mdwn} map <Leader>p :!google-chrome "%:p"<CR>  
```


### NERDTree插件

**[NERDTree](https://github.com/scrooloose/nerdtree)**

NERDTree的作用就是列出当前路径的目录树，一般IDE都是有的。可以方便的浏览项目的总体的目录结构和创建删除重命名文件或文件名。


#### 配置

```
" 配置使用F2快捷键快速调出和隐藏它
map <F2> :NERDTreeToggle<CR>
" 配置关闭vim时，如果打开的文件除了NERDTree没有其他文件时，它自动关闭，减少多次按:q!
autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTreeType") &&b:NERDTreeType == "primary") | q | endif
" 配置打开vim时自动打开NERDTree
autocmd vimenter * NERDTree
" 显示行号
let NERDTreeShowLineNumbers=1
let NERDTreeAutoCenter=1
" 是否显示隐藏文件
let NERDTreeShowHidden=1
" 设置宽度
let NERDTreeWinSize=31
" 在终端启动vim时，共享NERDTree
let g:nerdtree_tabs_open_on_console_startup=1
" 忽略一下文件的显示
let NERDTreeIgnore=['\.pyc','\~$','\.swp']
" 显示书签列表
let NERDTreeShowBookmarks=1
```

#### 常用命令

```
ctrl + w + h    光标 focus 左侧树形目录
ctrl + w + l    光标 focus 右侧文件显示窗口
ctrl + w + w    光标自动在左右侧窗口切换 #！！！
ctrl + w + r    移动当前窗口的布局位置


o       在已有窗口中打开文件、目录或书签，并跳到该窗口
go      在已有窗口 中打开文件、目录或书签，但不跳到该窗口
t       在新 Tab 中打开选中文件/书签，并跳到新 Tab
T       在新 Tab 中打开选中文件/书签，但不跳到新 Tab
i       split 一个新窗口打开选中文件，并跳到该窗口
gi      split 一个新窗口打开选中文件，但不跳到该窗口
s       vsplit 一个新窗口打开选中文件，并跳到该窗口
gs      vsplit 一个新 窗口打开选中文件，但不跳到该窗口
!       执行当前文件
O       递归打开选中 结点下的所有目录
x       合拢选中结点的父目录
X       递归 合拢选中结点下的所有目录
e       Edit the current dif

双击    相当于 NERDTree-o
中键    对文件相当于 NERDTree-i，对目录相当于 NERDTree-e

D       删除当前书签

P       跳到根结点
p       跳到父结点
K       跳到当前目录下同级的第一个结点
J       跳到当前目录下同级的最后一个结点
k       跳到当前目录下同级的前一个结点
j       跳到当前目录下同级的后一个结点

C       将选中目录或选中文件的父目录设为根结点
u       将当前根结点的父目录设为根目录，并变成合拢原根结点
U       将当前根结点的父目录设为根目录，但保持展开原根结点
r       递归刷新选中目录
R       递归刷新根结点
m       显示文件系统菜单 #！！！然后根据提示进行文件的操作如新建，重命名等
cd      将 CWD 设为选中目录

I       切换是否显示隐藏文件
f       切换是否使用文件过滤器
F       切换是否显示文件
B       切换是否显示书签

q       关闭 NerdTree 窗口
?       切换是否显示 Quick Help

:tabnew [++opt选项] ［＋cmd］ 文件      建立对指定文件新的tab
:tabc   关闭当前的 tab
:tabo   关闭所有其他的 tab
:tabs   查看所有打开的 tab
:tabp   前一个 tab
:tabn   后一个 tab

标准模式下：
gT      前一个 tab
gt      后一个 tab

```

#### 与git结合

**[nerdtree-git-plugin](https://github.com/Xuyuanp/nerdtree-git-plugin)**

##### 配置

```
let g:NERDTreeIndicatorMapCustom = { 
    \ "Modified"  : "✹",
    \ "Staged"    : "✚",
    \ "Untracked" : "✭",
    \ "Renamed"   : "➜",
    \ "Unmerged"  : "═",
    \ "Deleted"   : "✖",
    \ "Dirty"     : "✗",
    \ "Clean"     : "✔︎",
    \ "Unknown"   : "?"
    \ }

```

### MiniBufExplorer插件

MiniBufExplorer提供多文件同时编辑功能，并在编辑器上方显示文件的标签。 

[MiniBufExplorer](https://github.com/fholgado/minibufexpl.vim)


#### 配置

```
" 配置MiniBufExplorer
let g:miniBufExplMapWindowNavArrows = 1 
let g:miniBufExplMapWindowNavVim = 1  
let g:miniBufExplMapCTabSwitchWindows = 1  
let g:miniBufExplMapCTabSwitchBufs = 1   
let g:miniBufExplModSelTarget = 1    
"解决FileExplorer窗口变小问题  
let g:miniBufExplForceSyntaxEnable = 1  
let g:miniBufExplorerMoreThanOne=2
"这里配置了F3和F4键来进行前后buffer的跳转                                                                                                       
map <F3> :MBEbp<CR>
map <F4> :MBEbn<CR>
```

#### 效果

![](http://7xkx71.com1.z0.glb.clouddn.com/vim_md_2.png)


### Tagbar 插件

[](https://github.com/majutsushi/tagbar)

tagbar是一个taglist的替代品，比taglist更适合c++使用，函数能够按类区分，支持按类折叠显示等，显示结果清晰简洁。
由于taglist在使用过程中对中文支持不好，当文件夹是中文的时候，没法生成taglist，于是这里我使用tagbar，它可以很好的解决中文的问题。

#### 配置

```
" 设置 tagbar 子窗口的位置出现在主编辑区的右边
let tagbar_right=1 
" 设置标签子窗口的宽度 
let tagbar_width=25 
" tagbar 子窗口中不显示冗余帮助信息 
let g:tagbar_compact=1
" 设置F9快捷键开启                                                                                                                              
map <F9> :Tagbar<CR>
"如果是c语言的程序的话，tagbar自动开启
autocmd BufReadPost *.cpp,*.c,*.h,*.hpp,*.cc,*.cxx call tagbar#autoopen()
```
#### 效果

![](http://7xkx71.com1.z0.glb.clouddn.com/vim_md_3.png)


### CtrlP 插件

使用频率最高的插件之一

作用: 模糊搜索, 可以搜索文件/buffer/mru/tag等等

github: 原始[kien/ctrlp](https://github.com/kien/ctrlp.vim), 使用的是国人改进版本 [ctrlpvim/ctrlp.vim](https://github.com/ctrlpvim/ctrlp.vim)

#### 配置

```
let g:ctrlp_map = '<leader>p'
let g:ctrlp_cmd = 'CtrlP'
map <leader>f :CtrlPMRU<CR>
let g:ctrlp_custom_ignore = {
    \ 'dir':  '\v[\/]\.(git|hg|svn|rvm)$',
    \ 'file': '\v\.(exe|so|dll|zip|tar|tar.gz|pyc)$',
    \ }
let g:ctrlp_working_path_mode=0
let g:ctrlp_match_window_bottom=1
let g:ctrlp_max_height=15
let g:ctrlp_match_window_reversed=0
let g:ctrlp_mruf_max=500
let g:ctrlp_follow_symlinks=1
```

#### 使用

使用:CtrlP或:CtrlP [starting-directory]调用CtrlP进入查找文件模式
使用:CtrlPBuffer或:CtrlPMRU进入查找buffer或者查找MRU文件模式
使用:CtrlPMixed同时搜索普通文件、Buffers或者MRU文件

一旦CtrlP被打开了，就可以使用以下的命令

<F5> 清除当前目录下的缓存，获取新的结构
<c-f>和<c-b> 在各个模式下转换
<c-d> 使用文件名搜索代替全路径搜索
<c-r> 使用正则模式
<c-j>和<c-k> 上下选择文件
<c-t> <c-v>和<c-x> 在新的tab或者新的分割窗口打开选择的文件
<c-n>和<c-p> 找到之前或者之后查找的字符串
<c-y> 创建一个新的文件
<c-z> 标记或者取消标记多个文件然后使用<c-o>打开它们



### 参考

+ [vim编辑markdown时实现预览](http://howiefh.github.io/2013/05/16/vim-markdown-preview/)
+ [vim安装markdown插件](http://www.jianshu.com/p/24aefcd4ca93)
+ [NERDTree插件](http://www.jianshu.com/p/eXMxGx)
+ [上古神器vim插件：你真的学会用NERDTree了吗？](http://www.jianshu.com/p/3066b3191cb1)
+ [vim MiniBufExplorer 插件](http://www.cnblogs.com/westfly/p/3284476.html)
+ [MiniBufExplorer插件的使用](http://suchj.iteye.com/blog/1169566)
+ [VIM插件: TAGBAR](http://www.wklken.me/posts/2015/06/07/vim-plugin-tagbar.html)
+ [使用Vundle管理配置Vim基本插件](http://blog.jasonding.top/2015/04/29/Developer%20Kits/%E3%80%90Vim%E3%80%91%E4%BD%BF%E7%94%A8Vundle%E7%AE%A1%E7%90%86%E9%85%8D%E7%BD%AEVim%E5%9F%BA%E6%9C%AC%E6%8F%92%E4%BB%B6/)
+ [Vim配置、插件和使用技巧](http://www.jianshu.com/p/a0b452f8f720)
+ [VIM插件: CTRLP[文件搜索]](http://www.wklken.me/posts/2015/06/07/vim-plugin-ctrlp.html)
+ [vim每日插件之ctrlp](http://www.boiajs.com/2014/12/17/vim-ctrlp)
+ [vim中的杀手级插件：CtrlP](http://zuyunfei.com/2013/08/26/vim-plugin-ctrlp/)
