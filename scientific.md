#### more Python packages

`pip install`

- `numpy`
- `cython`
- `matplotlib`

``` python
>>> import matplotlib.pyplot as plt
>>> Y = [1,4,9,16]
>>> plt.scatter(range(len(Y)),Y,s=250,color='r')
<matplotlib.collections.PathCollection object at 0x10c751b90>
>>> plt.savefig('example.png')
>>>
```

[example.png](example.png)

   `open -a Preview example.png`

`pip install`

- `scipy`

``` python
>>> from scipy import stats
>>> from scipy.stats import norm
>>> norm.cdf(0)
0.5
>>> norm.cdf(2)
0.97724986805182079
>>>
```

[PyCogent](http://pycogent.org)

`pip install`

- `cogent`

``` python
>>> import cogent.maths.stats.distribution as distr
>>> distr.binomial_low(successes=5, trials=10, prob=0.5)
0.6230468749999999
>>> distr.binomial_low(successes=5, trials=10, prob=0.5)
0.6230468749999999
>>>
```

``` python
>>> from cogent.db.ncbi import EFetch
>>> seqL = ['AF411020','EU373389','AJ278451',
... 'AF411019','DQ450530','AJ002809']
>>> FH = open('/Users/telliott_admin/Desktop/seqs.txt','w')
>>> for seq in seqL:
...     ef = EFetch(id=seq)
...     FH.write(ef.read() + '\n')
... 
>>> FH.close()
>>>
```

```
>AF411020.1 Achromobacter xylosoxidans strain AU1011 16S ribosomal RNA gene, partial sequence
AGTTTGATCCTGGCTCAGATTGAACGCTAGCGGGATGCCTTACACATGCAAGTCGAACGGCAGCACGGAC
...
```

#### muscle

This guy is in a Homebrew "tap" so first

    > brew tap homebrew/science

then

`brew install`

- muscle
- fasttree

`fasttree` fails because it requires `gcc`.  This thread suggests that `clang` will compile `fasttree`, but then the executable hangs.  It works properly either with the `gcc` compiler or with this flag `-DNO_SSE` to `clang`.

I just installed the Xcode Command Line Tools (which I did have and should've still had).

Now I have `gcc` too.








