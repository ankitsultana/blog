---
---

So I was working on my [dotfiles](https://github.com/bk2dcradle/dotfiles)
project on GitHub, where I needed to iterate over all git submodules of the
project in a shell script. Basically, we want to know the `url` and
`relative-path` for each submodule.

Firstly, according to [git-scm](https://git-scm.com/docs/git-submodule) or
`git submodule --help`, the key to each submodule url is `submodule.$name.url`.
But how do we get `$name`?

We will use `git submodule status`, which prints the SHA1 checksum and the
submodule name. Doing `git submodule status` gives:

{% highlight shell %}
-a2d664f67ec734cf920f5d28c7fccfffb9983aac iterm/colors/base16-iterm2
-6cc9d539783716c8e614364562cce8709be2957f iterm/fzf
-84b152753e773baa491fa2524644bc7eadbb5032 utilities/subtitle-downloader
-12272b34e580e80afa0815fdbeeeea1a7e57a4bb utilities/tools-osx
{% endhighlight %}

Furthermore, there is a thing called `--get` which gets the value for a given
key. We know that the key is `submodule.'iterm/fzf'.url` or `submodule.'iterm/fzf'.path`

`git config` checks for git configuration files. We can use different to check or set
configuration options. Example:

git config --get user.name

git config -f .gitmodules --get submodule.'tools-osx'.path
