It occurred to me that I haven't explained the Terminal prompt that I use:

     >
 
If you have a stock install of macOS and open the Terminal, you'll see something like this:

    Toms-MacBook-Air-2:Desktop telliott$
    
Ugly. 

My `.bash_profile` has a number of things I haven't thought about in several years.

```
> cat ~/.bash_profile 
export PATH=/usr/local/bin:$HOME/bin:$HOME/Software/go/bin:$PATH
export RDP_JAR_PATH=$HOME/Software/rdp_classifier/rdp_classifier-2.0.jar
export BLASTMAT=$HOME/bin/blast/programs/blast-2.2.22/data
PS1="> "
alias tm='open -a TextMate'
alias oh='open -a Safari _build/html/index.html'
alias ts='python typeset/scripts/script.py'
>
```

But the one that matters here is

    PS1="> "

if you put that in a file `.bash_profile` in your home directory, you'll get a simple prompt too.