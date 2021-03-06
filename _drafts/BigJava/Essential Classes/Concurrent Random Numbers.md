
# Concurrent Random Numbers

In JDK 7, 
[`java.util.concurrent`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html) includes a convenience class, 
[`ThreadLocalRandom`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadLocalRandom.html), for applications that expect to use random numbers from multiple threads or `ForkJoinTask`s.

For concurrent access, using `ThreadLocalRandom` instead of `Math.random()` results in less contention and, ultimately, better performance.

All you need to do is call `ThreadLocalRandom.current()`, then call one of its methods to retrieve a random number. Here is one example:

```

int r = ThreadLocalRandom.current() .nextInt(4, 77);

```
