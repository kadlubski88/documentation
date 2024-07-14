# Basic snippets

## Run command on host and print output
~~~rust
use std::process::{Command, Output};
fn main() {
    println!("Hello, process!");
    let output: Result<std::process::Output, std::io::Error> = Command::new("cat")
        .args(["/etc/hostname"])
        .output();
    let result: Output = output.unwrap();
    let stdout: Vec<u8> = result.stdout;
    println!("{}", String::from_utf8(stdout).unwrap());
}
~~~