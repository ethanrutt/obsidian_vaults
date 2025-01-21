# Getting Started
## Install
- Since I use arch (btw), i'll install with `pacman`
```sh
sudo pacman -S rustup
rustup default stable
```
- update
```sh
rustup update
```
- uninstall
```sh
rustup self uninstall
```
- RTFM (opens locally in your browser)
```sh
rustup doc
```
## Hello World
- `.rs` files are rust files
- snake case convention
- classic hello world code in rust
```rust
fn main() {
	println!("Hello world!");
}
```
- compile
```sh
rustc main.rs
./main
```
- very similar to c in compilation and execution
- rust has a `main` function which is the entry point
- **Note**: the `!` means it is a *macro*
## Cargo
- Rust's built system and package manager.
- creating new project with cargo
```sh
cargo new <project_name>
```
- creates `Cargo.toml`, `src` directory, and also initializes a new `git` repo **if** it's not already inside of a git repo
- Cargo uses TOML for configuration
	- `Cargo.toml` has `[package]` as the first section, which defines the name of the project, version of the project, and edition (covered in Appendix E)
	- The next section is the `[dependencies]`  section which is where you can list dependencies
	- other sections are available, covered later
- Cargo assumes that your code is in the `src` directory. Top level is for `README.md` and other stuff
- while in top level build with `cargo build`
- output in `target/debug` (since it's debug build by default)
- **NOTE**: can also to build and run all in one command which is the standard way with
```sh
cargo run
```
- `cargo check` also does all compilation checks but doesn't produce an executable
- When you're ready for the release build, run `cargo build --release`
