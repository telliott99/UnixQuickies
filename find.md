### Search for files with Unix `find`

`find` lists all the files in a given file hierarchy.

From the Desktop I construct a small example directory

```
mkdir d && touch d/1
> find d
d
d/1
>
```

``find`` is recursive.  Control this with ``maxdepth``.

```
> mkdir -p x/y/z && touch x/y/z/1.txt
> find x
x
x/y
x/y/z
x/y/z/1.txt
> find x -maxdepth 1
x
x/y
>
```

Results from ``find`` are not sorted:

```
> touch a b c
> find . -maxdepth 1
.
./.DS_Store
./a
./c
./d
./x
./b
>
```

but of course, they <i>can</i> be:

```
> find . -maxdepth 1 | sort
.
./.DS_Store
./a
./b
./c
./d
./x
> 
```

#### Combine with `xargs ls` to list the resulting paths

`find` is usually combined with some other command: for example, `xargs` is used to call `ls` with each of the output file paths.

```
> find x | xargs ls -al
-rw-r--r--  1 telliott  staff  0 Jul 22 12:27 x/y

x:
total 0
drwxr-xr-x   3 telliott  staff  102 Jul 22 12:27 .
drwxr-xr-x@ 13 telliott  staff  442 Jul 22 12:31 ..
-rw-r--r--   1 telliott  staff    0 Jul 22 12:27 y
>
```

#### Combine with `grep` to filter for a pattern


```
> find ~/Music/iTunes/iTunes\ Media/Music | grep ".mp3" | wc -l
     127
>
```

#### Deal with spaces in filenames

The biggest problem here is the long directory path that contains a space.  Suppose we have the file `a\ b` in the `x` directory.  The space is escaped with `\`  from the command line:

    > touch x/a\ b
    > ls x
    a b    y  
    >
 
So if we want to enter it manually, just escape the space again
 
```
> ls x/a\ b
x/a b
```

But suppose we want to reuse the path as a variable:

```
> p=x/a\ b
```
The problem is that the variable `p` gets split on the space

```
> ls $p
ls: b: No such file or directory
ls: x/a: No such file or directory
> ls "$p"
x/a b
>
```

We fixed the problem with quotes.  An even better example:

```
> p=~/Music/iTunes/iTunes\ Media/Music
> find "$p" | grep ".m4a" | wc -l
    3212
>
```

That's a lot of songs.

#### Filter by time of modification (or access)

```
> find /usr -type f -mtime -1 
/usr/local/share/man/whatis
find: /usr/sbin/authserver: Permission denied
/usr/share/man/whatis
>
```

`sudo` allows us to look but there aren't any more hits.  Actually, this problem was created by the `texlive` install, which is stupid in some respects.

Only two files in `/usr` were modified in the previous day.

For other time frames, use `-mtime n[smhdw]`

I reinstalled `/usr/local` for a demo of Homebrew 13 days ago:

```
> find /usr -type f -mtime -2w | wc -l
find: /usr/sbin/authserver: Permission denied
   17886
>
```

Note:  if you don't want to see that error message add `2>/dev/null`

```
> find /usr -type f -mtime -2w 2>/dev/null | wc -l
   17886
>
```

#### Filter by size

```
> find ~/Video -size +1000M
/Users/telliott/Video/Video-FWW/Klausz Master1.m4v
/Users/telliott/Video/Video-FWW/Klausz Master2.m4v
>
```

#### Multiple targets

```
> find ~/Photos -name "*.jpg" -o -name "*.gif" | head -n 2
/Users/telliott/Photos/01-03 faves/guys.jpg
/Users/telliott/Photos/01-03 faves/IMG_0148_mod.jpg
>
```

#### Exclude hidden files

In this pattern:  `'*/\.*'`, we use the wildcard `*`, the file path separator `/`, and the leading symbol for a hidden file, `.`, but need to escape the last with `\.`.

    > find . | head -n 3
    .
    ./.DS_Store
    ./C.H. Becksvoort - FWW Articles.pdf
    > find . -not -path '*/\.*' | head -n 3
    .
    ./C.H. Becksvoort - FWW Articles.pdf
    ./find.rst
    >

Since the current directory `.` is not preceedied by `/`, it doesn't match.

#### Filter by user or group

    find . -user te
    find . -group admin

#### Links

- [one](https://danielmiessler.com/study/find/) 
- [two](http://content.hccfl.edu/pollock/Unix/FindCmd.htm)
