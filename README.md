# :evergreen_tree: Conifer

<a href="https://docs.rs/conifer"><img src="https://img.shields.io/badge/docs-latest-blue.svg?style=flat-square" alt="docs.rs docs" /></a>

A simple framebuffer game engine for PinePhone, Raspberry Pi, and other devices with touch screens.

- [x] make games without X11!
- [x] auto detect virtual terminal framebuffer
- [x] auto detect touch screen input
- [x] works on pinephone, raspbery pi, desktop
- [x] image support
- [ ] layers
- [ ] text drawing
- [ ] sprites
- [ ] sound
- [ ] web assembly support

```toml
[dependencies]
conifer = "0.1"
```
## Before You Start

Make sure your user is a part of `video` and `input` group

```bash
sudo addusr video richard 
sudo addusr input richard
# Logout and login
```

To bring up a virtual terminal that isn't being used for X11, you can usually get to it by typing:

```
ctrl + alt + f2 # or f3,f4...
```

Sometimes this can only be done from a login screen.

## Hello World

```rust
use conifer::prelude::*;

fn main() {
    let white = color_from_rgb(255, 255, 255);
    run(move |canvas, event| {
        // if the user swiped, exit
        if let Event::Swipe(s) = event {
            // if the users finger released, exit
            if s.finished {
                return Ok(RunResponse::Exit);
            }
            // draw something where finger is
            for p in s.points {
                canvas.set_pixel(p.x as usize, p.y as usize, white);
            }
        }
        // let conifer know we want to push framebuffer pixels to screen
        Ok(RunResponse::Draw)
    })
    .expect("something went wrong")
}
```

# License

This project is licensed under either of

 * Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or
   http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or
   http://opensource.org/licenses/MIT)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in `conifer` by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.
