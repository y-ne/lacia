# The value of an object is determined by the form and function that humans give to it.

<img src="docs/lacia.webp" alt="Lacia" width="512">

## Introduction

**Lacia** is a personal, documented recreation of `Yy`’s old design of the same name, which originally served as the skeleton for his other creation.

The old Lacia was written in `Go`, and I will try to rewrite it in `Rust`.

I may explain it in a single `README` or split it across multiple files. We’ll see.

## Origin

I was a C developer, and working as a web developer forced me to interact with the browser through `JavaScript`. The problem was that I was a bit old-school, and the idea of `throw err` propagating an error up the call stack felt strange to me. Given my experience with other languages at the time, `Go` felt a bit like home. The idea of returning errors as values just made more sense to me. And let’s just say that, to me, `Go` felt much faster than `JavaScript` while being less complicated than `Rust`.

Frameworks are also a no-go for me, since they tend to be quite opinionated and can sometimes be hard to mix and match with other libraries without ending up with weird bindings.

So, after the constraints and requirements were clear, I began researching and designing the skeleton of my project and ended up with `net/http`, `chi`, and `pgx`.

Q?: Yes, I used a library for routing because, if I’m not mistaken, the standard `net/http` library didn’t have a built-in router back then. Some time later, Go added one, so I removed `chi` altogether.

I used this architecture for several years, and it felt fantastic. The performance satisfied my needs, with low resource usage while maintaining high throughput. Since this architecture is basically just the language’s standard library and a database driver, it gave me much more control and allowed me to mix and match whatever tools I needed.

The drawback is that it’s kind of tiring to write, since you’re basically building everything from scratch. But hey, for me, it was a price worth paying to have more control over what I was doing, so I didn’t care.

## Concept

**DISCLAIMER**: Like I said in the beginning, this is just personal documentation, and web development wasn’t exactly my strong suit. So, if you have a better perspective on it or ideas that could help improve it, simply reach out to me. I’m happy to learn from you.

#### &lt;BLACK MONOLITH&gt;

Ever heard that a monolith is bad and that you need to design a microservices architecture so your system can scale?

In my opinion, most of the time, a monolith is more than enough. Rather than running multiple services built with resource-hungry languages or frameworks, why not just build one that achieves the same thing while consuming far fewer resources?

I designed Lacia primarily as a monolith, but I kept it decoupled and stateless. So, if you want to deploy it as a cluster and distribute the load across multiple nodes, you can. But in many cases, that doesn’t really matter. You may end up hitting the limits of your load balancer or other infrastructure before you actually need to scale Lacia itself.

#### &lt;STANDALONE&gt;

Lacia has no external service dependencies other than the database itself. It is designed to keep running even if the database becomes temporarily unavailable. Instead of exiting, it will continue serving requests and attempt to re-establish database connections as needed. This avoids the annoyance of manually restarting a container just because Postgres was in a bad mood for a couple of seconds.

#### &lt;MINIMALISTIC&gt;

At its core, Lacia uses Postgres as its sole source of truth. Additional components are avoided unless absolutely necessary, since they add operational complexity and can introduce data desynchronization or distributed race conditions.
