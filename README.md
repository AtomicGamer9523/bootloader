# Fork of [Bootloader](https://github.com/phil-opp/blog_os)

An experimental x86 bootloader written in Rust and inline assembly.

## Configuration

The bootloader exposes a few variables which can be configured through the `Cargo.toml` of your kernel:

```toml
[package.metadata.bootloader]
# The address at which the kernel stack is placed. If not provided, the bootloader
# dynamically searches for a location.
kernel-stack-address = "0xFFFFFF8000000000"

# The size of the kernel stack, given in number of 4KiB pages. Defaults to 512.
kernel-stack-size = 128

# The virtual address offset from which physical memory is mapped, as described in
# https://os.phil-opp.com/paging-implementation/#map-the-complete-physical-memory
# Only applies if the `map_physical_memory` feature of the crate is enabled.
# If not provided, the bootloader dynamically searches for a location.
physical-memory-offset = "0xFFFF800000000000"

# The address at which the bootinfo struct will be placed. if not provided,
# the bootloader will dynamically search for a location.
boot-info-address = "0xFFFFFFFF80000000"
```

Note that the addresses **must** be given as strings (in either hex or decimal format), as [TOML](https://github.com/toml-lang/toml) does not support unsigned 64-bit integers.

## Requirements

You need a nightly [Rust](https://www.rust-lang.org) compiler and [cargo xbuild](https://github.com/rust-osdev/cargo-xbuild). You also need the `llvm-tools-preview` component, which can be installed through `rustup component add llvm-tools-preview`.
