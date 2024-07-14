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

## Make a simple GET request
~~~rust
// cargo add reqwest --features=blocking
// sudo apt install libssl-dev
use reqwest::blocking::Client;
fn main() {
    let http_client = Client::new();
    let response = http_client.get("https://httpbin.org/ip").send();
    if response.is_ok() {
        println!("{:?}", response.unwrap().text().unwrap());
    }
}
~~~
