This page needs work!!

``cut``

```
> echo "abcd" | cut -c 2-3
bc
>
```

``-c`` flag is for character.

The ``-f`` flag uses whitespace as default delimiter.

```
> echo "a b c d" | cut -f 1-2 -d " "
b c
> 
```


```
> echo $a b c d$ | cut -f 1-2 
b c d$
>
```

Not sure about that last one, must provide delimiter otherwise ``cut`` just gave everything after $0.

CSV

```
> echo "a,b,c,d,e" | cut -f 2-4 -d ,
b,c,d
> 
```

TAB is default delimiter

-f flag for -d stuff

-b is for bytes
