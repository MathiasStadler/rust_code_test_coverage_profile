# Rust Code Test Coverage Profile

- this project give a short overview rust code coverage and profile

## My project platform

```bash
cat /etc/os-release 
PRETTY_NAME="Ubuntu 22.04.4 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.4 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```

## My rust version at creation this project

```bash
rustup show
Default host: x86_64-unknown-linux-gnu
rustup home:  /home/trapapa/.rustup

installed toolchains
--------------------

stable-x86_64-unknown-linux-gnu
nightly-x86_64-unknown-linux-gnu (default)

active toolchain
----------------

stable-x86_64-unknown-linux-gnu (directory override for '/home/trapapa/rust_code_test_coverage_profile')
rustc 1.78.0 (9b00956e5 2024-04-29)
```

## I'm use microsoft vscode version

```bash
code --version
1.89.1
dc96b837cf6bb4af9cd736aa3af08cf8279f7685
x64
```

## I'm used this vscode extension special for this project

```bash
code --list-extensions |grep coverage
ryanluker.vscode-coverage-gutters
```

## Project setup

> [!NOTE]
> [Project Setup From Here](https://github.com/MathiasStadler/repo_template/blob/main/includes/extract_scripts_from_markdown.md)

&nbsp;

> [!TIP]
> [How to set json with comment in MS Video Studio Code](https://github.com/MathiasStadler/repo_template/blob/main/includes/update_rust_add_crates_to_last_version.md)

&nbsp;

> [!NOTE]
> [Update rust to latest stable version](https://github.com/MathiasStadler/repo_template/blob/main/includes/update_rust_add_crates_to_last_version.md)

## Instal crates to be used in this project

- I'm use [cargo edit](https://crates.io/crates/cargo-edit), show my [tutorial](https://github.com/MathiasStadler/repo_template/blob/main/includes/update_rust_add_crates_to_last_version.md#install-cargo-edit) for install additional package

```bash
# update all project crates
cargo update
# install cargo-tarpaulin
cargo add cargo-tarpaulin
# /w features
cargo add --features vendored-openssl cargo-tarpaulin
# install flamegraph
cargo add flamegraph
# show version of dependencies and current version vs. akt. version
cargo update --verbose
```

## first testcase

```rust
#!/usr/bin/env bash
export EXAMPLE_SCRIPT_FILE="01_first_testcase.rs"
export EXAMPLE_SCRIPT_DIR="examples/"
cat << EoF > ./$EXAMPLE_SCRIPT_DIR/$EXAMPLE_SCRIPT_FILE
// FROM HERE
// https://github.com/MathiasStadler/repo_template/blob/main/includes/dummy_small_rust_codeblock.md
pub fn main(){

    println!("Hello, world!");
}

#[cfg(test)]
mod test {

    use super::*;

    #[test]
    fn test_main() {
        assert_eq!(main(), ());
    }
}


/*
export FILE_NAME=$EXAMPLE_SCRIPT_FILE
export FILE_DIR_NAME=$EXAMPLE_SCRIPT_DIR
echo "build prg => \$(echo \$FILE_NAME | cut -d . -f 1)";
cargo build --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "run PRG => \$(echo \$FILE_NAME | cut -d . -f 1)";
cargo run --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "";
echo "run TEST => \$(echo \$FILE_NAME | cut -d . -f 1)"
cargo test --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
# cargo test --jobs 4 --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "ReturnCode => \$?"
*/
EoF
```

- [Speed up Rust CI pipelines that use Tarpaulin](https://identeco.de/en/blog/speed-up-rust-ci-pipelines-that-use-tarpaulin/)

## use simple test coverage

> [!TIP]
> a toolchain/build target its own target directory ``` --target-dir ```
> avoid project new compiling for each new test run after small change inside test

```bash
--target-dir target/tarpaulin-target/
```

## run all test inside the examples folder

- add ```--example```

```bash
cargo tarpaulin --ignore-tests --target-dir target/tarpaulin-target/ --skip-clean --out Lcov --example
```

- output

```bash
100.00% coverage, 2/2 lines covered, +0.00% change in coverage
```

## I'm use

```markdown
![image](data:image/png;base64,<BASE64_HERE>)
```

![image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEYAAAAUCAAAAAAVAxSkAAABrUlEQVQ4y+3TPUvDQBgH8OdDOGa+oUMgk2MpdHIIgpSUiqC0OKirgxYX8QVFRQRpBRF8KShqLbgIYkUEteCgFVuqUEVxEIkvJFhae3m8S2KbSkcFBw9yHP88+eXucgH8kQZ/jSm4VDaIy9RKCpKac9NKgU4uEJNwhHhK3qvPBVO8rxRWmFXPF+NSM1KVMbwriAMwhDgVcrxeMZm85GR0PhvGJAAmyozJsbsxgNEir4iEjIK0SYqGd8sOR3rJAGN2BCEkOxhxMhpd8Mk0CXtZacxi1hr20mI/rzgnxayoidevcGuHXTC/q6QuYSMt1jC+gBIiMg12v2vb5NlklChiWnhmFZpwvxDGzuUzV8kOg+N8UUvNBp64vy9q3UN7gDXhwWLY2nMC3zRDibfsY7wjEkY79CdMZhrxSqqzxf4ZRPXwzWJirMicDa5KwiPeARygHXKNMQHEy3rMopDR20XNZGbJzUtrwDC/KshlLDWyqdmhxZzCsdYmf2fWZPoxCEDyfIvdtNQH0PRkH6Q51g8rFO3Qzxh2LbItcDCOpmuOsV7ntNaERe3v/lP/zO8yn4N+yNPrekmPAAAAAElFTkSuQmCC)

convert ./test_pictures.png -resize 33% ./out.png
base64 ./out.png