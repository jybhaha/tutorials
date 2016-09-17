# vim配置

这两天vim8.0重新更新了，据说更新了很多新特新。是时候重新拾起我的vim了。

![]配置图](https://github.com/jybhaha/tutorials/blob/master/IMAGE/VIM-1.png)


## 安装gvim

由于是在Windows平台，所以安装gvim，另外gvim支持鼠标模式，别跟我说情怀，我要的是效率。

**注意：**安装的时候记得安装full模式。

安装完成后，开始配置vim。

这是windows平台下的目录结构：

+vim80/
+vimfiles/
  _vimrc
  
vim80是vim程序的执行文件。

+vimfiles是vim的一些设置和插件配置。

_vimrc是vim的配置文件。工作的大部分时间全部话费在操作此文件上。

##  vundle

插件管理插件。

非常方便的插件管理工具。

要想快速的安装插件，第一件事情就是安装它。

官方网站在[这里](https://github.com/VundleVim/Vundle.vim)

只需按照配置一步一步来即可。

安装步骤也很简单：
1. 在_vimrc相应位置添加：Plugin 'tpope/vim-fugitive'即可。
2. 跟新_vimrc文件，输入命令：`:so %` 或者 `:source %`
3. 再次输入命令 `:PluginInstall`等待安装即可


## 安装插件

安装插件的所知的途径有：

- [vim官网](http://www.vim.org/)
- [vimawsome](http://vimawesome.com/)

推荐vimawsome网站，在网站上可以找到大部分插件，并且有详细教程

因为官网下载的gvim，不支持python，所以强大的插件YouCompleteMe没有安装成功，不过我也不需要它，我用vim就是用一个编辑器，并不会当作ide来使用。

配置文件如下。有详细注释：

- 加入了改键
- 将F2到F5，F8重新映射，其中F2映射为绝对行号，相对行号的切换。
- 等等


其他设置：

- 用vim打开一个新文档的时候，gvim默认重新用一个窗口打开。很不方便一起查看。只需要在total commander的F4启用编辑器的默认设置改为：`E:\program\Vim\vim80\gvim.exe -p --remote-tab-silent "%1"` 。这样打开新文档的时候默认用新标签页打开。





```
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=e:/program/Vim/vimfiles/bundle/Vundle.vim/
call vundle#begin('e:/program/Vim/vimfiles/bundle')
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

" The following are examples of different formats supported.
" Keep Plugin commands between vundle#begin/end.
" plugin on GitHub repo
Plugin 'tpope/vim-fugitive'
Plugin 'scrooloose/nerdtree'
Plugin 'scrooloose/nerdcommenter'
Plugin 'luochen1990/rainbow'
"Plugin 'scrooloose/syntastic'
Plugin 'kien/ctrlp.vim'
Plugin 'altercation/vim-colors-solarized'
Plugin 'majutsushi/tagbar'
Plugin 'tpope/vim-surround'
Plugin 'easymotion/vim-easymotion'
Plugin 'nathanaelkane/vim-indent-guides'
Plugin 'raimondi/delimitmate'
Plugin 'sjl/gundo.vim'
"Plugin 'ervandew/supertab'
"Plugin 'tpope/vim-markdown'
"Plugin 'suan/vim-instant-markdown'
"Plugin 'valloric/youcompleteme'
Plugin 'vim-airline/vim-airline'
Plugin 'vim-airline/vim-airline-themes'
" plugin from http://vim-scripts.org/vim/scripts.html
Plugin 'L9'
Plugin 'OmniCppComplete'
" Git plugin not hosted on GitHu
Plugin 'git://git.wincent.com/command-t.git'
" git repos on your local machine (i.e. when working on your own plugin)
Plugin 'file:///home/gmarik/path/to/plugin'
" The sparkup vim script is in a subdirectory of this repo called vim.
" Pass the path to set the runtimepath properly.
Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}
" Install L9 and avoid a Naming conflict if you've already installed a
" different version somewhere else.
Plugin 'ascenator/L9', {'name': 'newL9'}

" All of your PlPlugin 'vim-airline/vim-airline'ugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line



source $VIMRUNTIME/vimrc_example.vim
source $VIMRUNTIME/mswin.vim
behave mswin

set diffexpr=MyDiff()
function MyDiff()
  let opt = '-a --binary '
  if &diffopt =~ 'icase' | let opt = opt . '-i ' | endif
  if &diffopt =~ 'iwhite' | let opt = opt . '-b ' | endif
  let arg1 = v:fname_in
  if arg1 =~ ' ' | let arg1 = '"' . arg1 . '"' | endif
  let arg2 = v:fname_new
  if arg2 =~ ' ' | let arg2 = '"' . arg2 . '"' | endif
  let arg3 = v:fname_out
  if arg3 =~ ' ' | let arg3 = '"' . arg3 . '"' | endif
  if $VIMRUNTIME =~ ' '
    if &sh =~ '\<cmd'
      if empty(&shellxquote)
        let l:shxq_sav = ''
        set shellxquote&
      endif
      let cmd = '"' . $VIMRUNTIME . '\diff"'
    else
      let cmd = substitute($VIMRUNTIME, ' ', '" ', '') . '\diff"'
    endif
  else
    let cmd = $VIMRUNTIME . '\diff'
  endif
  silent execute '!' . cmd . ' ' . opt . arg1 . ' ' . arg2 . ' > ' . arg3
  if exists('l:shxq_sav')
    let &shellxquote=l:shxq_sav
  endif
endfunction

"""""""""""""""""""""""""""""""
"快捷键
"""""""""""""""""""""""""""""""
" 目录树快捷键
nnoremap <silent> <F5> :NERDTree<CR>
"tagbar 快捷键
nmap <F8> :TagbarToggle<CR>
""""""""""""""
"ctrlP快捷键
""""""""""""""
let g:ctrlp_map = '<c-p>'
let g:ctrlp_cmd = 'CtrlP'
""""""""""""""""""""
"我的自定义快捷键
""""""""""""""""""""
map <Leader>w <esc>:w<CR>
map <Leader>wq <esc>:wq<CR>
map <Leader>q <esc>:q<CR>
map <Leader>q! <esc>:q!<CR>
map <Leader>s <esc>:sp<CR>
map <Leader>vs <esc>:vsp<CR>

imap <M-j> <esc>

" 分屏窗口移动, Smart way to move between windows
map <C-j> <C-W>j
map <C-k> <C-W>k
map <C-h> <C-W>h
map <C-l> <C-W>l

" 搜索相关
" Map <Space> to / (search) and Ctrl-<Space> to ? (backwards search)
map <space> /

"""""""""""""
"tab 操作
""""""""""""


" 新建tab  Ctrl+t
nnoremap <C-t>     :tabnew<CR>
inoremap <C-t>     <Esc>:tabnew<CR>
" tab切换
map <leader>th :tabfirst<cr>
map <leader>tl :tablast<cr>

map <leader>tj :tabnext<cr>
map <leader>tk :tabprev<cr>
map <leader>tn :tabnext<cr>
map <leader>tp :tabprev<cr>

map <leader>te :tabedit<cr>
map <leader>td :tabclose<cr>
map <leader>tm :tabm<cr>

" normal模式下切换到确切的tab
noremap <leader>1 1gt
noremap <leader>2 2gt
noremap <leader>3 3gt
noremap <leader>4 4gt
noremap <leader>5 5gt
noremap <leader>6 6gt
noremap <leader>7 7gt
noremap <leader>8 8gt
noremap <leader>9 9gt
noremap <leader>0 :tablast<cr>


" F2 行号模式切换
function! HideNumber()
  if(&relativenumber)
    set number
	set relativenumber!
  elseif(&number)
    set relativenumber
	set number!
  endif
endfunc
nnoremap <F2> :call HideNumber()<CR>


" F3 显示可打印字符开关
nnoremap <F3> :set list! list?<CR>
" F4 换行开关
nnoremap <F4> :set wrap! wrap?<CR>
" F6 语法开关，关闭语法可以加快大文件的展示
nnoremap <F6> :exec exists('syntax_on') ? 'syn off' : 'syn on'<CR>


"""""""""""""
"插件设置
"""""""""""""



"easymotion设置
map <Leader> <Plug>(easymotion-prefix)




""""""""""""""""
"rainbow 设置
""""""""""""""""
let g:rainbow_active = 1 "0 if you want to enable it later via :RainbowToggle

"tags 设置
set tags=e:\program\Vim\ctags58\tags

set tags=tags;
set autochdir

"nerdcomment 设置
" Add spaces after comment delimiters by default
let g:NERDSpaceDelims = 1

" Use compact syntax for prettified multi-line comments
let g:NERDCompactSexyComs = 1

" Align line-wise comment delimiters flush left instead of following code indentation
let g:NERDDefaultAlign = 'left'

" Set a language to use its alternate delimiters by default
let g:NERDAltDelims_java = 1

" Add your own custom formats or override the defaults
let g:NERDCustomDelimiters = { 'c': { 'left': '/**','right': '*/' } }

" Allow commenting and inverting empty lines (useful when commenting a region)
let g:NERDCommentEmptyLines = 1

" Enable trimming of trailing whitespace when uncommenting
let g:NERDTrimTrailingWhitespace = 1

"IndentGuides设置
let g:indent_guides_auto_colors = 0
autocmd VimEnter,Colorscheme * :hi IndentGuidesOdd  guibg=red   ctermbg=3
autocmd VimEnter,Colorscheme * :hi IndentGuidesEven guibg=green ctermbg=4


"vim-markdown 设置
autocmd BufNewFile,BufReadPost *.md set filetype=markdown
let g:markdown_fenced_languages = ['html', 'python', 'bash=sh', 'c']

"vim-instant-markdown 设置
let g:instant_markdown_slow = 1
let g:instant_markdown_autostart = 0

"""""""""""""""""""""""""""""
"显示
"""""""""""""""""""""""""""""
set nu "行号
set ruler  "标尺

set cursorline "高亮当前行
set cursorcolumn "高亮当前列

" 高亮搜索
set hlsearch
set incsearch                   " Find as you type search
set showmatch " 高亮显示匹配的括号
set matchtime=5 " 匹配括号高亮的时间（单位是十分之一秒）
set scrolloff=10 " 光标移动到buffer的顶部和底部时保持10行距离 
set hlsearch " 高亮搜索 "
set nowrapscan " 查找到文件头或文件尾时停止
set incsearch " 边输入边查找 "
set laststatus=2 " 总是显示状态行 
set ignorecase " 在搜索的时候忽略大小写 

" 字体设置
set guifont=Consolas:h11

"""语法高亮
syntax enable
set background=dark
colorscheme solarized
syntax on
autocmd InsertEnter * se cul    " 用浅色高亮当前行  

" 禁止显示菜单栏和工具栏
set guioptions-=m
set guioptions-=T

" 设置tab
filetype indent on
set tabstop=4 
" 统一tab长度4
set softtabstop=4
set shiftwidth=4
" 不以空格代替tab
set noexpandtab
" 状态栏个数
set laststatus=2
"中文设置
set encoding=utf-8
"set termencoding=utf-8
set fileencodings=ucs-bom,utf-8,chinese,latin-1
if has("win32")
set fileencoding=chinese
else
set fileencoding=utf-8
endif
set langmenu=zh_CN.utf-8
source $VIMRUNTIME/delmenu.vim
source $VIMRUNTIME/menu.vim
language messages zh_cn.utf-8

set ai " autoindent自动对齐
set si " smartindent只能对齐

set showcmd         " 输入的命令显示出来，看的清楚些 

set showmode		" 左下角显示当前vim模式
set vb t_vb=   "去掉错误提示声音"  

set nobackup  "不备份"
"在windows版本中vim的退格键模式默认与vi兼容，与我们的使用习惯不太符合，下边这条可以改过来 
set backspace=indent,eol,start 
" history存储容量
set history=2000

" 文件修改之后自动载入
set autoread
" 启动的时候不显示那个援助乌干达儿童的提示
set shortmess=atI
" 关闭交换文件
set noswapfile
" vimrc文件修改之后自动加载, windows
autocmd! bufwritepost _vimrc source %
" vim 自身命令行模式智能补全
set wildmenu

"Alt 组合键不映射到菜单上
 set winaltkeys=no

""""""""""""""""""
"autocmd
"""""""""""""""""""
autocmd FileType python setlocal shiftwidth=4 tabstop=4 softtabstop=4 expandtab
autocmd FileType c,cpp set cindent 



```