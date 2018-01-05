### Unix `grep`

`grep` stands for "globally search for a regular expression and print" --- [here](https://en.wikipedia.org/wiki/Grep).

`grep` can be invoked on files, or even a stream of data using a pipe.

```
> printf "ab\nbc\ncd\nff\n" | grep b
ab
bc
>
```

Sometimes the regular expression is quoted but this is not necessary here.  Using`"b"` above gives the same result.

#### Search each line of a file:

```
> printf "ab\nbc\ncd\nff\n" > x.txt
> grep b x.txt 
ab
bc
> grep b < x.txt 
ab
bc
>
```

Notice the pattern is first and the file path second

    grep <pattern> <file>

```
> grep -r -n "stuff" ~/Github/MyUnix/ 
..MyUnix/basics/sphinx.rst:81:It can happen that partially built stuff..
>
```

File then pattern does not work:

```
> grep ~/Github/MyUnix "stuff"
grep: stuff: No such file or directory
>
```

#### Filter the output from `find`

Here we compare `-name` option to `find` with `find | grep`, and we use the `-n` option (to `grep`) to get the line number of the result:

```
> find . -name ".txt"
>
> find . -name "*.txt" | head -n 2
./generator notes.txt
./generator specs.txt
>
```

```
> find . | grep -n ".txt" | head -n 2
4:./generator notes.txt
5:./generator specs.txt
>
```

The wild card `*` is required for `find` but not `grep`.

#### Useful options for `grep`

* ``-A`` print A lines of context after each match
* ``-B`` print B lines of context before each match
* ``-C`` print C lines of context before and after each match

* ``-a`` process binary as if it were text
* ``-b`` print the offset in bytes
* ``-c`` print a count of number of matching lines
* ``-f`` obtain patterns from file, one per line

* ``-i`` ignore case
* ``-n`` print line numbers for matches
* ``-r`` recursive (also ``-R``)

```
..
/Users/telliott/Github/MyUnix//Setup.txt-works
/Users/telliott/Github/MyUnix//Setup.txt-
/Users/telliott/Github/MyUnix//Setup.txt-
/Users/telliott/Github/MyUnix//Setup.txt:RNA folding stuff
/Users/telliott/Github/MyUnix//Setup.txt-http://www.tbi.univie.ac.at/RNA/
/Users/telliott/Github/MyUnix//Setup.txt-
/Users/telliott/Github/MyUnix//Setup.txt-standalone BLAST
..
```

#### Regular expressions

The patterns that `grep` searches for are called regular expressions, or regex for short.  regex is a language defining descriptions of search patterns that are not necessarily exact matches.

Some simple regex symbols and patterns are:

* ``*`` wildcard
* ``\d`` matches a digit [0-9]
* ``\D`` matches a non-digit
* ``\s`` matches whitespace
* ``^`` match only at the beginning of the string
* ``$`` match only at the end of the string
* ``[abc]`` match any of a,b,c
* ``[a-d]`` match any of a,b,c,d

#### A first regular expression:

Two very simple RE's

```
> grep b$ x.txt
ab
> grep ^b x.txt
bc
>
```

#### Printing man pages

`grep` is a classic example of where you might want to print out a copy of the man pages to a file.

```
> man grep > grep.txt
> wc -l grep.txt
     301 grep.txt
>
```

301 lines!  If you do this, you'll find that ``man`` stutters.  Try this instead:

```
> man grep | col -b > grep.txt
>
```
