# ytd-rs

![crates.io](https://img.shields.io/crates/v/$CRATE.svg) ![docs.rs](https://docs.rs/ytd-rs/badge.svg)

This is a simple wrapper for [youtube-dl](https://youtube-dl.org/) in rust.

```rust
use ytd_rs::{YoutubeDL, ResultType, Arg};
use std::path::PathBuf;
use std::error::Error;
fn main() -> Result<(), Box<dyn Error>> {
    // youtube-dl arguments quietly run process and to format the output
    // one doesn't take any input and is an option, the other takes the desired output format as input
    let args = vec![Arg::new("--quiet"), Arg::new_with_arg("--output", "%(title).90s.%(ext)s")];
    let link = "https://www.youtube.com/watch?v=uTO0KnDsVH0";
    let path = PathBuf::from("./path/to/download/directory");
    let ytd = YoutubeDL::new(&path, args, link)?;

    // start download
    let download = ytd.download();

    // check what the result is and print out the path to the download or the error
    match download.result_type() {
        ResultType::SUCCESS => println!("Your download: {}", download.output_dir().to_string_lossy()),
        ResultType::IOERROR | ResultType::FAILURE =>
                println!("Couldn't start download: {}", download.output()),
    };
Ok(())
}
```
