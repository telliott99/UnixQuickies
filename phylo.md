#### muscle

This guy is in a Homebrew "tap" so first

    > brew tap homebrew/science

then

`brew install`

- muscle
- fasttree

At first, `fasttree` fails because it requires `gcc`.  This thread suggests that `clang` will compile `fasttree`, but then the executable hangs.  It works properly either with the `gcc` compiler or with this flag `-DNO_SSE` to `clang`.

Instead, I just installed the Xcode Command Line Tools (which I did have, thought I had, and should've still had).

Now I have `gcc` too.