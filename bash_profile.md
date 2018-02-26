It occurred to me that I haven't explained the Terminal prompt that I use:

     >
 
If you have a stock install of macOS and open the Terminal, you'll see something like this:

    Toms-MacBook-Air-2:Desktop telliott$
    
Ugly. 

My `.bash_profile` has a number of things I haven't thought about in several years.

```
> cat ~/.bash_profile 
PS1="> "

alias te='open -a TextEdit'
alias oh='open -a Safari _build/html/index.html'
alias ts='python typeset/scripts/script.py'

p0=$HOME/bin
p1=$HOME/Library/Python/2.7/bin
p2=$HOME/Library/Python/3.6/bin
export PATH=$p0:$p1:$p2:$PATH
>
```

But the one that matters here is

    PS1="> "

if you put that in a file `.bash_profile` in your home directory, you'll get a simple prompt too.