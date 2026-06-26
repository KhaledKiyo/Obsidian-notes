#programing #backend
## setup

download rust

```bash
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

check rust version

```bash
rustc --version
```

update rust

```bash
rustup update
```

check cargo version

```bash
cargo --version
```

---

## project

create a new project

```bash
cargo new <name>
```

turn an existing directory into a project

```bash
cargo init
```

then move your files into the `src` folder

add a package

```bash
cargo add <package_name>
```

---

## running code

check your code without building

```bash
cargo check
```

compile a single file

```bash
rustc main.rs
```

then run the output

```bash
./main
```

build the project

```bash
cargo build
```

build and run in one step

```bash
cargo run
```

---

## basics

the entry point of every rust program

```rust
fn main() {
}
```

print to the console

```rust
println!("hello");
// without newline
print!("hello");
```