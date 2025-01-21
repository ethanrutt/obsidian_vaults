# Guessing Game
- refer to [[Chapter1]] for creating a new project
- Starting with a lot of stuff, here's a code snippet
```rust
use std::io;

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {}", guess);
}
```
- line 1, brings the `io` library into scope, which is a part of the  `std` library
- "By default, Rust has a set of items defined in the standard library that it brings into the scope of every program. This set is called the prelude, and you can see everything in it in the [standard library documentation](https://doc.rust-lang.org/std/prelude/index.html)."
- `io` isn't included in this prelude. If there's something you want to use, then you have to bring it into scope like above
## Variables
- `let` declares new var. These are **immutable by default**.
- adding `mut` let's the variable be mutable
- In the code we have
```rust
let mut guess = String::new();
```
- This means that we want to create a new variable of the `String` type. the `new` is *associated* with the String type, denoted by the `::`
## IO
- now we get the input from `io::stdin()`
- **note**: if we hadn't imported in line 1 with `use std::io`, we could still call this with `std::io::stdin()`
- Next, we do the `read_line()` method and pass in `&mut guess` as an argument.
- More will be mention on this in [[Chapter4]], however for now, just now that references are immutable by default and reference the same bit of memory.
## Potential Failure
- The thing returned from `read_line()` is not just a string, but a `Result` object, which is an enumeration, and we call the different possible states of the enumeration *variants*. 
- `Result` has two variants, `Err` and `Ok`
- This is mentioned more in [[Chapter6]]
- The `Result` type has methods attached to it, and one of them is the `expect()` method. This basically checks if the `Result` is in the `Err` variant, in which case the program will crash and the error message you passed in as an argument to `expect` will print.
- If the `Result` is in the `Ok`, then it just returns the value and continues normally
- The compiler catches `Result` objects that you haven't properly handled by calling expect and will output a warning.
## Placeholders
- These are like python f-strings by default. You can either put them inside the parentheses or as a comma separated list after with empty parentheses, or combine them, i.e.
```rust
let x = 5;
let y = 10;

println!("x = {x} and y + 2 = {}", y + 2);
```
## Continuing the game, Crates and Random Numbers
- Rust doesn't provide a random type in the std library
- to add dependencies, visit `Cargo.toml` again, under the `[dependencies]` section.
- add the `rand` crate
```toml
[dependencies]
rand = "0.8.5"
```
- Cargo uses [semantic versioning](https://semver.org/), so this basically means any version above `0.8.5` but below `0.9.0`. If you don't know why that is, then RFTM bruh. Read up on semantic versioning and infer that it's for compatibility reasons.
- These dependencies are pulled from [Crates.io](https://crates.io/)
- Cargo also uses a `Cargo.lock` file the first time that you build with updated dependencies for reproducible purposes. Explicit upgrading is needed if you already have a `Cargo.lock` file. It is normally checked in to source code.
- However, you can run `cargo update` which will disregard your lock file and update stuff, but this won't upgrade you past breaking changes or API changes because of semantic versioning, just new patches.
- i.e.
	- Running `cargo build` might grab `rand 0.8.5` and create the lock file
	- `rand 0.8.6` comes out
	- `rand 0.9.0` comes out
	- `cargo build` will grab you `rand 0.8.5` since that's what is in the lock file
	- `cargo update` will grab you `rand 0.8.6` since that's newer but still compatible
	- changing `Cargo.toml` to `rand 0.9.0` and rerunning `cargo build` will explicitly upgrade you and rewrite the lock file.
	- More discussed in [[Chapter14]]
## Using Crates
- To use the `rand` crate, we need to bring it into scope
```rust
use rand::Rng;
```
- See [[Chapter10]] for more on traits, but `Rng` is a trait that the defines methods that random number generators implement
- Next, we generate the number with
```rust
let secret_number = rand::thread_rng().gen_range(1..=100);
```
- `gen_range` takes a range expression of the form `start..=end` where `start` and `end` are **inclusive**
- Using crates can be complicated, so running 
```sh
cargo doc --open
```
- will generate docs for the crates as well
## Comparing Guess and Secret Number
- adding the `match` which is kind of like a `switch`  and `Ordering` which is another enum which has variants `Less`, `Greater`, and `Equal`
```rust
use std::cmp::Ordering;

fn main() {
	// ...
	// stuff from above 
	// ...

	match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
}
```
- however, this will not compile since `guess` and `secret_number` are not of the same type
- in `let mut guess = String::new()`, Rust was able to infer that it would be a string.
- similarly with `let secret_number = rand::thread_rng().gen_range(1..=100);` it inferred that it was an integer
- By default, Rust says that integers are `i32` type, or 32 bit signed integer type
	- There is also `u32`, `i64`, `f64`, for unsigned 32 bit, signed 64 bit, float 64 bit, etc.
- We can fix this by adding
```rust
let guess: u32 = guess.trim().parse().expect("Please type a number!");
```
- There is a lot going on here.
	- Note that we have a type annotation now. the `: u32` tells Rust that this should be a unsigned 32 bit integer.
	- This annotation is also used by the `parse()` method, it will attempt to convert the string to that type.
		- You can explicitly do this by using `turbofish`, check [here](https://doc.rust-lang.org/std/primitive.str.html#method.parse)
		- `let guess = guess.trim().parse::<u32>().expect("Please type a number!");`
	- We have also already defined `guess` earlier. Rust allows for shadowing, which means that we can use the same variable name. This is nice for when we have to convert types. More on shadowing in [[Chapter3]]
## Wrapping up the game, loops and error handling
* use `loop` keyword to create an infinite loop
```rust
loop {
	// match snippet
}
```
- Now we don't have a way to exit when we win, and any non-digit input will crash the program
-  in the match statement, we can have more than just one statement by using `{}`, so let's add a `break` to the `Equal` variant
```rust
	match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => {
	        println!("You win!");
	        break;
	    },
    }
```
- **Note**: In this match we are going over the possible variants in the `Ordering` enumeration, returned by the `cmp`. We can use this same pattern to have error handling on the conversion of the user input to integer
```rust
let guess: u32 = match guess.trim().parse() {
	Ok(num) => num,
	Err(_) => continue,
};
```
- if we hit `Ok(num)`, then it will just return num, and bind that to `guess`.
- If we hit `Err(_)`, then it will just continue to the next iteration of the loop, reprompting the user. The `_` is a catchall, saying we want to match all error values