---
layout: post
---
If you have switched to [Standard](http://github.com/feross/standard) style Javascript and you use Vim, just put these lines in your `vimrc`

{% highlight vim %}
autocmd FileType javascript set tabstop=2
autocmd FileType javascript set expandtab
autocmd FileType javascript set shiftwidth=2
autocmd FileType javascript retab
{% endhighlight %}

Here `autocmd FileType javascript` means that the command that follows will be executed once Vim sets the *FileType* of the current buffer to *javascript*.

* The first line sets the tab length that is equivalent to 2 spaces.
* The second line means that each tab that you hit will be converted into equivalent number of spaces.
* The third line means that if you were to shift a line or a group of lines using `<` in Normal mode, it will shift them by 2 spaces.
* The fourth line converts any existing tabs in the *Javascript* file that you open into equivalent number of spaces.
