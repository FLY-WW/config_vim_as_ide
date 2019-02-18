# config_vim_as_ide
configure vim as python ide


## 配置环境
1. OS: released centos 6.10, kernel 2.6.32-642.6.2.el6.x86_64 x86_64 GNU/Linux;
2. python: python3, anaconda3编译安装;
3. vim: 8.1编译安装;


## vim配置文件

```
    " *********************************************
    " Vbundle插件管理
    " *********************************************
    set nocompatible              " required
    set nu              " required
    filetype off                  " required
    let python_highlight_all=1
    syntax on
    set hlsearch
    set encoding=utf-8
    set clipboard=unnamed
    set ts=4
    set mouse=a        "启用鼠标"

    " set the runtime path to include Vundle and initialize
    set rtp+=~/.vim/bundle/Vundle.vim
    call vundle#begin()

    " alternatively, pass a path where Vundle should install plugins
    "call vundle#begin('~/some/path/here')

    " let Vundle manage Vundle, required
    Plugin 'gmarik/Vundle.vim'
    Plugin 'majutsushi/tagbar'
    Plugin 'scrooloose/nerdtree'
    Plugin 'Valloric/YouCompleteMe'
    Plugin 'vim-airline/vim-airline'
    Plugin 'vim-airline/vim-airline-themes'
    Plugin 'kien/ctrlp.vim'
    Plugin 'tmhedberg/SimpylFold'
    Plugin 'scrooloose/syntastic'
    Plugin 'nvie/vim-flake8'
    Bundle 'klen/python-mode'
    Bundle 'Lokaltog/powerline', {'rtp': 'powerline/bindings/vim/'}

    " Add all your plugins here (note older versions of Vundle used Bundle instead of Plugin)
    " All of your Plugins must be added before the following line
    call vundle#end()            " required
    filetype plugin indent on    " required

    " *********************************************
    " " 分割布局相关
    " " *********************************************
    " set splitbelow
    " set splitright
    " "快捷键，ctrl+l切换到左边布局，ctrl+h切换到右边布局
    " "ctrl+k切换到上面布局，ctrl+j切换到下面布局
    nnoremap <C-J> <C-W><C-J>
    nnoremap <C-K> <C-W><C-K>
    nnoremap <C-L> <C-W><C-L>
    nnoremap <C-H> <C-W><C-H>



    " *********************************************
    " " Tomorrow主题配置
    " " *********************************************
    set t_Co=256
    set background=dark
    "colorscheme Tomorrow-Night

    " 开启代码折叠功能
    " 根据当前代码行的缩进来进行代码折叠
    set foldmethod=indent
    set foldlevel=99
    " 将折叠za快捷键映射到space空格键上
    nnoremap <space> za
    let g:SimpylFold_docstring_preview=1
    " *********************************************
    " NERD插件属性
    " *********************************************
    au vimenter * NERDTree   " 开启vim的时候默认开启NERDTree
    map <F2> :NERDTreeToggle<CR>  " 设置F2为开启NERDTree的快捷键
    " *********************************************
    " YCM插件相关
    " *********************************************
    let g:ycm_autoclose_preview_window_after_completion=1
    " 跳转到定义处
    map <leader>g  :YcmCompleter GoToDefinitionElseDeclaration<CR>
    " 默认tab、s-tab和自动补全冲突
    let g:ycm_key_list_select_completion = ['<TAB>', '<c-n>', '<Down>']
    let g:ycm_key_list_previous_completion = ['<S-TAB>', '<c-p>', '<Up>']
    let g:ycm_auto_trigger = 1


    " 启动时自动focus
    map <F4> :TagbarToggle<CR>
    let g:tagbar_auto_faocus =1
    " 启动指定文件时自动开启tagbar
    autocmd BufReadPost *.py,*.pyc,*.cpp,*.c,*.h,*.hpp,*.cc,*.cxx call tagbar#autoopen()

    " *********************************************
    " vim-airline
    " *********************************************
    " 开启powerline字体
    let g:airline_powerline_fonts = 1
    " 使用powerline包装过的字体
    set guifont=Source\ Code\ Pro\ for\ Powerline:h14

    " *********************************************
    " ctrlp
    " *********************************************
    let g:ctrlp_map = '<c-p>'
    let g:ctrlp_cmd = 'CtrlP'
    " 设置过滤不进行查找的后缀名
    let g:ctrlp_custom_ignore = '\v[\/]\.(git|hg|svn|pyc)$'


    " *********************************************
    " python代码风格PEP8
    " *********************************************
    au BufNewFile,BufRead *.py set tabstop=4 |set softtabstop=4|set shiftwidth=4|set textwidth=79|set noexpandtab|set autoindent|set fileformat=unix
    au BufNewFile,BufRead *.js, *.html, *.css set tabstop=2|set softtabstop=2|set shiftwidth=2

    " 多余空格
    "au BufRead,BufNewFile *.py,*.pyw,*.c,*.h match BadWhitespace /\s\+$/
    "
    "





    " Python-mode
    " Activate rope
    " Keys: 按键：
    " K             Show python docs 显示Python文档
    " <Ctrl-Space>  Rope autocomplete  使用Rope进行自动补全
    " <Ctrl-c>g     Rope goto definition  跳转到定义处
    " <Ctrl-c>d     Rope show documentation  显示文档
    " <Ctrl-c>f     Rope find occurrences  寻找该对象出现的地方
    " <Leader>b     Set, unset breakpoint (g:pymode_breakpoint enabled) 断点
    " [[            Jump on previous class or function (normal, visual, operator modes)
    " ]]            Jump on next class or function (normal, visual, operator modes)
    "            跳转到前一个/后一个类或函数
    " [M            Jump on previous class or method (normal, visual, operator modes)
    " ]M            Jump on next class or method (normal, visual, operator modes)
    "              跳转到前一个/后一个类或方法
    let g:pymode_rope = 1

    " Documentation 显示文档
    let g:pymode_doc = 1
    let g:pymode_doc_key = 'K'

    "Linting 代码查错，=1为启用
    let g:pymode_lint = 1
    let g:pymode_lint_checker = "pyflakes,pep8"
    " Auto check on save
    let g:pymode_lint_write = 1

    " Support virtualenv
    let g:pymode_virtualenv = 1

    " Enable breakpoints plugin
    let g:pymode_breakpoint = 1
    let g:pymode_breakpoint_bind = '<leader>b'

    " syntax highlighting 高亮形式
    let g:pymode_syntax = 1
    let g:pymode_syntax_all = 1
    let g:pymode_syntax_indent_errors = g:pymode_syntax_all
    let g:pymode_syntax_space_errors = g:pymode_syntax_all

    " Don't autofold code 禁用自动代码折叠
    let g:pymode_folding = 0
```


## 常见问题
1. ycmd server SHUT DOWN <br>
**A:** 在`~/.vim/bundle/youcompleteme`执行`./install.sh`;(https://github.com/Valloric/YouCompleteMe/issues/914)
2. Your C++ compiler does NOT support C++11 <br>
**A:** 升级gcc编译器到7.3版本；安装**rhel-server-rhscl-7-rpms**:`yum-config-manager --enable rhel-server-rhscl-7-rpms; yum install devtoolset-7 -y`;(https://github.com/Valloric/YouCompleteMe/issues/2596)


## 参考列表
1. [Vim与Python真乃天作之合：打造强大的Python开发环境
](https://segmentfault.com/a/1190000003962806)
2. [Mac下打造vim+Python开发环境 备忘.vimrc](https://www.cnblogs.com/liujianzuo888/articles/7127992.html)

