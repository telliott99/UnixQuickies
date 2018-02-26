#### PATH environment variable

Set by

- ``/etc/paths``
- files in ``/etc/paths.d``
- ``~/.bash_profile``

#### Example

My $PATH is currently:

```
> echo $PATH | tr \: \\n
/usr/local/bin:
/Users/telliott_admin/bin
/Users/telliott_admin/Software/go/bin:
/usr/local/bin
/usr/bin
/bin
/usr/sbin
/sbin
/Library/TeX/texbin
/usr/local/MacGPG2/bin
/opt/X11/bin
/Applications/Postgres.app/Contents/Versions/latest/bin
>
```

I haven't used some of these in a long time!  So where are they set?

Some of them come from ``/etc/paths``

```
> cat /etc/paths
/usr/local/bin
/usr/bin
/bin
/usr/sbin
/sbin
>
```

Some come from ``/etc/paths.d``

```
> cd /etc/paths.d
> ls
40-XQuartz	TeX
MacGPG2		postgresapp
> 
```

```
> find . -exec cat {} \;
cat: .: Is a directory
/Library/TeX/texbin
/usr/local/MacGPG2/bin
/opt/X11/bin
/Applications/Postgres.app/Contents/Versions/latest/bin
>
```

That leaves
a second copy of ``/usr/local/bin`` and

```
/Users/telliott_admin/bin:
/Users/telliott_admin/Software/go/bin:
```

They are from ``~/.bash_profile``:

```
> cat ~/.bash_profile
export PATH=/usr/local/bin:$HOME/bin:$HOME/Software/go/bin:$PATH
PS1="> "
alias tm='open -a TextMate'
alias oh='open -a Safari _build/html/index.html'
alias ts='python typeset/scripts/script.py'
> 
```

Note some aliases set here too.  Very useful:

```
alias tm='open -a TextMate'
```
