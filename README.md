# coalmine

building blocks for web servers - not a framework

> This project is currently work in progress and the mission statement and
> inital documentation are being written. If you came here by accident and
> like what you see feel free to join the chat, send PRs and get involved.


[![Join discord chat](https://img.shields.io/badge/discord-join%20chat-blue?logo=discord&logoColor=white&style=for-the-badge)](https://discord.gg/YFmQ5Mb)

## Abstract

This project aims to provide essential functions, structures and traits which can be used to write web servers. The goal is to provide building blocks which can be used in various ways.

### Mission statement

Let’s build great building blocks with outstanding API.  
Not using them should feel like a waste of time.

### Goals

- **Building blocks** - Provide functions, structures and traits to be used
  when building web servers

- **Pick what you want** - You should be able to pick and use what you need
  and want. It is fine if you use only one single function.

- **No magic** - It is cool to hide implementation details behind clever
  macros, but if the same can be expressed with a regular line of code it
  is just for the show off and should not be part of `coalmine`.

### Non goals

- **Reinvent the wheel** - There are great libraries out there which just
  work. There is no need to reinvent `hyper`, `h2`, `tokio-postgres`, `config`
  and lots of other excellent crates.

- **Framework** - Coalmine is not supposed to become a framework of any kind.

- **Language independence** - Sorry, this project is Rust only.

- **No unsafe code** - Keep the language free of unsafe code just for the
  sake of it. Code should be correct but doesn’t necessarily have to be
  free of unsafe code.

## Extractors

An extractor is a function which takes the `Request` object as argument and
returns a value.

Other web frameworks tend to move this logic into the function signature
and use a special `FromRequest` trait of some kind. This does not fit well
with our "no magic" goal and therefore extractors in the sense of `coalmine`
are just plain functions like that:

```rust
fn get_user_agent(request: &Request) -> UserAgent {
    match request.headers.get("user-agent") {
        Some(value) => UserAgent::parse(value),
        None => None
    }
}
```

Using it is just as simple as writing it:

```rust
async fn capture_event(request: Request) -> Response {
    let ua = get_user_agent(&request);
    ...
}
```

Extractors usually live in the `coalmine::extractors` module unless there
is another module which is specific to one use case.

## Routing

TBD

## Sessions

TBD

## Pooling

TBD

## Config

TBD
