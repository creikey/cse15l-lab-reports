I searched through both with diff. Cached results to two text files with >


# BUG ONE
test-files/194.md had differing results

The test:
```
Foo*bar\]]:my_(url) 'title (with parens)'

[Foo*bar\]]
```


Official implementation got `[url]`, while my implementation got `[]`, meaning my implementation was correct for this one. The bug with the official implementation is that it doesn't check if the next `[` is before the closing bracket. This could be fixed by changing line 79 from this
```java
if(nextOpenBracket == -1 || nextCloseBracket == -1
                  || closeParen == -1 || openParen == -1) {
                return toReturn;
```

To this
```java
if(nextOpenBracket == -1 || nextCloseBracket == -1
                  || closeParen == -1 || openParen == -1 || nextOpenBracket > openParen) {
                return toReturn;
```



# BUG TWO
test-files/201.md had differing results

The test:
```
[foo]: <bar>(baz)

[foo]
```

Official implementation got `[baz]` , but my implementation got `[]`. My implemention was correct for this one. The bug with the official implementation is that it does not check for a pair of )[. This could be fixed by changing line 64 from this
```java
            int nextCloseBracket = markdown.indexOf("]", nextOpenBracket);
            int openParen = markdown.indexOf("(", nextCloseBracket);
```

To this
```java
            int nextCloseOpenParenth = markdown.indexOf("](", nextOpenBracket);
```
and other code that used that variable to make it work