# rust-ytd
[![Build status](https://github.com/jebediah47/rust-ytd/actions/workflows/rust.yml/badge.svg)](https://github.com/jebediah47/rust-ytd/actions)
[![docs.rs](https://docs.rs/ytd-rs/badge.svg)](https://docs.rs/ytd-rs)

This is a simple wrapper for [yt-dlp](https://github.com/yt-dlp/yt-dlp) in rust.

```rust
use rust_ytd::{YoutubeDL, Arg};
use std::path::PathBuf;
use std::error::Error;
fn main() -> Result<(), Box<dyn Error>> {
    // youtube-dl arguments quietly run process and to format the output
    // one doesn't take any input and is an option, the other takes the desired output format as input
    let args = vec![Arg::new("--quiet"), Arg::new_with_arg("--output", "%(title).90s.%(ext)s")];
    let link = "https://www.youtube.com/watch?v=dQw4w9WgXcQ";
    let path = PathBuf::from("./path/to/download/directory");
    let ytd_path = PathBuf::from("/path/to/youtube-dl");
    let ytd = YoutubeDL::new(&path, args, link, &ytd_path)?;

    // start download
    let download = ytd.download()?;

    // check what the result is and print out the path to the download or the error
    println!("Your download: {}", download.output_dir().to_string_lossy());
    Ok(())
}
```
