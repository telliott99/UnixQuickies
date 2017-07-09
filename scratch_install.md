I love [Homebrew](https://brew.sh).  I have never had an issue with it, and I had plenty with Fink and some with Macports.

I decided that if I want to test (one more time) how to install Homebrew and get my computing environment working, I need to uninstall it first.  :(

#### Uninstall first

So here we go ([instructions](http://docs.brew.sh/FAQ.html)):

```bash
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
Warning: This script will remove:
/Users/telliott_admin/Library/Caches/Homebrew/
/Users/telliott_admin/Library/Logs/Homebrew/
/usr/local/Cellar/
...
/usr/local...
```

Did it.

```
==> /usr/bin/sudo /usr/bin/find /usr/local/Frameworks /usr/local/bin /usr/local/etc /usr/local/include /usr/local/lib /usr/local/opt /usr/local/sbin /usr/local/share /usr/local/var -name .DS_Store -delete
Password:
```

was a bit scary.  But the `sudo` is just to run find on `/usr/local...`.  A bit silly, if you ask me.

At the end:

``` bash
/usr/local/bin/
/usr/local/etc/
/usr/local/lib/
/usr/local/remotedesktop/
/usr/local/share/
/usr/local/texlive/
You may wish to remove them yourself.
>
```

I think I will.  (Remember we will need LaTeX again too).

    > pwd
	/usr
	> sudo rm -r local
	Password:
	>

So I guess that's it.

#### Install

First, let's make the directory `/usr/local`.

```
> sudo mkdir local
>> ls -al
drwxr-xr-x     2 root  wheel     68 Jul  9 16:30 local
...
```

Not what I want!

```
> sudo chown telliott local
> sudo chgrp staff local
> ls -al
...
drwxr-xr-x     2 telliott  staff     68 Jul  9 16:30 local
...
>
```

That looks better.

Now, for Homebrew.  [link](https://brew.sh)

```
> /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
==> This script will install:
/usr/local/bin/brew
/usr/local/share/doc/homebrew
/usr/local/share/man/man1/brew.1
/usr/local/share/zsh/site-functions/_brew
/usr/local/etc/bash_completion.d/brew
/usr/local/Homebrew
==> The following new directories will be created:
/usr/local/Cellar
/usr/local/Homebrew
/usr/local/Frameworks
/usr/local/bin
/usr/local/etc
/usr/local/include
/usr/local/lib
/usr/local/opt
/usr/local/sbin
/usr/local/share
/usr/local/share/zsh
/usr/local/share/zsh/site-functions
/usr/local/var

Press RETURN to continue or any other key to abort
```

Takes a bit and triggers LittleSnitch, but it goes.

    > brew doctor
    Your system is ready to brew.
    > 
    
Now I have to look at a list of what I used to have and decide what I want.  Here is my list

- python
- git
- libdvdcss
- sphinx
- youtube-dl

We're building Python from source, it isn't clear why, and this didn't happen three weeks ago or so.

At the end

    Pip and setuptools have been installed. To update them
    pip install --upgrade pip setuptools

Why not?

I look at Python modules with `help('modules')`, but there are so many in the default install that I can't tell what else I might want.

    `rsa`
    `pygments`

#### LaTeX

Then the last big thing is support for LaTeX.

I install Basic TeX from [here](http://www.tug.org/mactex/morepackages.html).

I check for problems with the wrong owner in `/usr/local`

```
> ls -al
...
drwxr-xr-x   3 root            wheel   102 Jun  7 12:10 texlive
...
```

Still the same problem, I wonder why.  Easily fixed with `chown` and `chgrp`.

Check for issues with LaTeX by running an example.  Looks good.
    



