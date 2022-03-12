I searched through both with diff. Cached results to two text files with >


# BUG ONE
test-files/194.md had differing results

The test:
```
Foo*bar\]]:my_(url) 'title (with parens)'

[Foo*bar\]]
```


Official implementation got `[url]`, while my implementation got `[]`, meaning my implementation was correct for this one. The bug with the official implementation is that it doesn't check for a preceding [] before the url.


# BUG TWO
test-files/201.md had differing results

The test:
```
[foo]: <bar>(baz)

[foo]
```

Official implementation got `[baz]` , but my implementation got `[]`. My implemention was correct for this one. The bug with the official implementation is that it does not check for a pair of )[.