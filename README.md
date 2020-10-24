# assertj-reactor
AssertJ extensions for Mono and Flux.

[ ![Download](https://api.bintray.com/packages/jacek-rzrz/assertj-reactor/assertj-reactor/images/download.svg) ](https://bintray.com/jacek-rzrz/assertj-reactor/assertj-reactor/_latestVersion)

## Getting started
Assertions extend from AssertJ core 
so a single import statement is enough
to get both standard AssertJ methods as well
as the reactive additions:

``` java
import static pl.rzrz.assertj.reactor.Assertions.assertThat;
```

### Check for an error signal
``` java
Mono<Void> mono = Mono.error(new Exception());

assertThat(mono).sendsError();
```

Inspect the exception:
``` java
Mono<Void> mono = Mono.error(new RuntimeException("oops"));

assertThat(mono).sendsError(error -> {
    assertThat(error).isInstanceOf(RuntimeException.class);
    assertThat(error).hasMessage("oops");
});
```

### Check successful completion
``` java
Mono<Void> mono = Mono.just("this");

assertThat(mono).completes();
```

### Count items
``` java
Flux<String> flux = Flux.just("one", "two", "three");

assertThat(flux).sendsItems(3);
```

