# The value of an object is determined by the form and function that humans give to it.

<img src="docs/lacia.webp" alt="Lacia" width="512">

## Introduction

`Lacia`, based on the same name, is a documented recreation of `Yy`’s old design, which originally served as the skeleton for his other creation.

I’ll potentially explain it in a single `README` or split it across multiple files. We’ll see.

## Origin

I was a C developer, and working as a web developer forced me to interact with the browser through `JavaScript`. The problem was, I was a bit old-school, and the idea of `throw err` propagating an error up the call stack kind of weirded me out. Given my experience with other languages at the time, `Go` felt a bit like home. The idea of returning errors as values just made more sense to me. And let's just say that `Go`'s performance felt much better than `JavaScript`'s to me, while not being as complicated as `Rust`.

Frameworks are also a no-go for me, since they tend to be quite opinionated and can sometimes be hard to mix and match with other libraries without ending up with weird bindings.

So, after the constraints and requirements were clear, I began researching and designing the skeleton of my project, and ended up with: `net/http`, `chi`, and `pgx`.

Q?: Yes, I used a library for routing because, if I'm not mistaken, the standard `net/http` library didn't have a built-in router back then. Some time later, Go added one, so I removed `chi` altogether.

I used this architecture for several years, and it felt fantastic. The performance satisfied my needs, with low resource usage while maintaining high throughput. Since this architecture is basically just the language's standard library and a database driver, it gave me much more control and allowed me to mix and match whatever tools I needed.

The drawback is that it's kinda tiring to write since you're basically building everything from scratch. But hey, for me, it was a price worth paying for having more control over what I was doing, so I didn't care.
