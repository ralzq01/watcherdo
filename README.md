# Capasule

A two phase trigger where a watcher watches the changes and a doer reacts to the changes.

## Getting Started

Capsule is implemented by Rust. It is currently in MVP(Minium Viable Product) stage. Since Rust is a cross-platform language, this product can be used in all mainstream OS (MacOS, Linux, Unix, Windows)

### Prerequisites

* If you are going to build this project from source, you should have Rust environments, which includes `rustc` and `cargo`.

### Installing

* From Source: Under Capsule/
  ```
  $ cargo build --release
  ```
  And then modify the `config.ini` to fit your own settings.
  ```
  $ cargo run
  ```
  to start the application!

* Or you can directly get the pre-released executable program from [here](https://github.com/ralzq01/Capsule/tree/master/release). And place the `config.ini` file in same place where the downloaded program are.


## Features

### Watcher

* FileWatcher

  FileWatcher is mainly used to detect file changes (write, create, rename, remove). In `config.ini` there will be some attributes you should specify:

  * `filepath` : specify the directory you want to watch. Should use **Absolute Path** (if you in Windows filesystem, please make sure use `\\` as splitter instead of single `\`)
  * `recursive` : whether to detect folders' change recursivly.
  * `check_interval_secs`: in which interval seconds will the FileWatcher check the changed events
  * `ignore`: `None` denotes any file updates will be detected. If you want some files won't be detected, specify a name and FileWatcher will ignore all file change events where the file name appears (So if you specify `abc` then all the relevant filepath which includes `abs` won't be detected, such as `this/file/absds` or `this/abs/aaa` of `this/file/abs`).

### Doer

* RemoteSync

  RemoteSync is mainly used to sync the files from the local to the remote. In `config.ini` there will be some attributes you should specify:

  * `remote_ip_port`: the ssh connect ip-port, usually the port should be 22.
  * `user`: the user name
  * `password`: the password. (currently only support connect with password.)
  * `remote_dir`: the remote directory you want to sync. Should use **Absolute Path**

* EmailSender

  EmailSender is mainly used for sending emails. **Currently only Support Outlook Smtp**.

  * `sender`: the sender mail address. Should be xxx@outlook.com
  * `recver`: the recver mail address.
  * `password`: sender mail account password.
  * `subject`: mail subject.
  * `content`: mail content. __TODO: contents of '{}' will be replaced by the input of the Watcher__

## Running the test

Since Rust `cargo` directly supports running the unit test with `#[test]`, you can directly use
```
$ cargo test
```
to run and view the test results.

## Lookup Document API

Since Rust `cargo` directly supports viewing docs in browser, you can directly use
```
$ cargo doc
```
to run and view the documents.

## Contributions

All kinds of contributions are welcomed!

When contributing to this repository, please first discuss the change you wish to make via issue, email, or any other method with the owners of this repository before making a change.

## Architecture

Watcher - Doer

The output of the watcher will serve as the input for the Doer.

