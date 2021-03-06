# vim-aha
Mine Vim Conf

## hack syntastic check 'on fly'

> vim+syntastic+pylint+vim-auto-save

因为没找到```syntastic```在写代码过程中自动检查可配操作，只能通过Vim ```:w```手动保存脚本时来触发syntastic. Oh, sad.

But, 很自然的，我们可以退而求其次去实现Vim自动保存。

Vim本身可以配置自动保存，不过要设置一些参数；懒癌发作找到一个封装好的插件，vim-auto-save，可以通过Vundle安装, 亲测可用, insert模式一切换会自动run syntastic check，算半自动吧。

下面是简要步骤:

0. get the Vim, syntastic, pylint ready to go
1. install Vundle to Vim
2. add ```Plugin '907th/vim-auto-save'``` between the ```call vundle#begin()``` and ```call vundle#end() ``` lines in .vimrc
3. run ```vim +PluginInstall +qall ``` in command line
4. add ```let g:auto_save = 1``` to .vimrc, to enable the AutoSave on Vim startup
5. open a python in Vim to test

最后建议修改vim-auto-save的监听事件，默认是```InsertLeave```和```TextChange```两种，可以再加一个```CursorHoldI```, 这样在插入模式下coding停顿时会自动保存并触发语法检查。修改位置在默认安装后的```~/.vim/bundle/vim-auto-save/plugin/AutoSave.vim```第29行，```let g:auto_save_events = ["InsertLeave", "TextChanged", "CursorHoldI"]

Link
* syntastic: https://github.com/vim-syntastic/syntastic
* Vundle: https://github.com/VundleVim/Vundle.vim
* vim-auto-save: https://github.com/907th/vim-auto-save.vim
