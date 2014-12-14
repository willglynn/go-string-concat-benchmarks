go-string-concat-benchmarks
===========================

Benchmarks to compare the different string concatenation methods in Go. For all the details, see [stringconcat_test.go](<stringconcat_test.go>).

There is also a [blog post detailing the methodology and results](http://herman.asia/efficient-string-concatenation-in-go).

In summary, for very few concatenations of short strings (fewer than hundred, length shorter than 10) using naive string appending is just fine. For more heavy-duty cases where efficiency is important, bytes.Buffer is the best choice out of the methods evaluated. strings.Join is a good choice when you already have a string slice that just needs to be concatenated into one string.

Here are how the methods tested stack up:

![Comparison of string concatenation methods in Go](http://img.svbtle.com/rlmmrxjtthkg.png)

And here are the raw results (also including a benchmark for byte slices):

```
BenchmarkNaiveConcat10     1000000         2112 ns/op          416 B/op      21 allocs/op
BenchmarkNaiveConcat100      20000        66753 ns/op        26945 B/op     201 allocs/op
BenchmarkNaiveConcat1000       300      4172921 ns/op      2699892 B/op    2001 allocs/op
BenchmarkNaiveConcat10000       10    143638603 ns/op    271745678 B/op   20001 allocs/op
BenchmarkByteSlice10       1000000         2231 ns/op          368 B/op      27 allocs/op
BenchmarkByteSlice100       100000        18285 ns/op         3152 B/op     210 allocs/op
BenchmarkByteSlice1000       10000       172194 ns/op        42132 B/op    2016 allocs/op
BenchmarkByteSlice10000       1000      1342907 ns/op       443680 B/op   20024 allocs/op
BenchmarkJoin10             500000         2928 ns/op          704 B/op      19 allocs/op
BenchmarkJoin100            100000        22067 ns/op         5664 B/op     112 allocs/op
BenchmarkJoin1000            10000       145021 ns/op        48864 B/op    1015 allocs/op
BenchmarkJoin10000            1000      1757030 ns/op       995183 B/op   10024 allocs/op
BenchmarkJoinSize10        1000000         2042 ns/op          368 B/op      15 allocs/op
BenchmarkJoinSize100        100000        14963 ns/op         3248 B/op     105 allocs/op
BenchmarkJoinSize1000        10000       117709 ns/op        32498 B/op    1005 allocs/op
BenchmarkJoinSize10000        2000      1069986 ns/op       331888 B/op   10005 allocs/op
BenchmarkBufferString10     500000         2833 ns/op          456 B/op      18 allocs/op
BenchmarkBufferString100    100000        15465 ns/op         2905 B/op     111 allocs/op
BenchmarkBufferString1000    10000       118501 ns/op        24230 B/op    1014 allocs/op
BenchmarkBufferString10000    2000       938581 ns/op       223520 B/op   10017 allocs/op
```
