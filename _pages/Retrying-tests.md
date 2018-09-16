---
layout: post
title:  "Automatically Retry Tests on Failure"
category: wiki
section: "7 - Other"
order: 16
---
If you find yourself with a stubborn test which fails very infrequently but
breaks the build when it does then Frameworkium has a solution.

Add the following to your `@Test` annotation and if the test fails it will be
marked as `SKIP` and then retried (up to `maxRetryCount` or a default of once).

```java
public class MyTest extends BaseUITest {
    
    @Test(retryAnalyzer = RetryFlakyTest.class)
    public void test_which_fails_less_than_1_per_cent() {
        // ...
    }
}
```

If your test is failing more than about 1% of the time, you should look to
improve its robustness before moving on. If you don't, or if you abuse the above
annotation, or if you are just lazy, then on your head be it!
