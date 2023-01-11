# Rust out-of-tree module

This is a basic template for an out-of-tree Linux kernel module written in Rust.

Please note that:

  - The Rust support is experimental.

  - The kernel that the module is built against needs to be Rust-enabled (`CONFIG_RUST=y`).

  - The kernel tree (`KDIR`) requires the Rust metadata to be available. These are generated during the kernel build, but may not be available for installed/distributed kernels (the scripts that install/distribute kernel headers etc. for the different package systems and Linux distributions are not updated to take into account Rust support yet).

  - All Rust symbols are `EXPORT_SYMBOL_GPL`.

  - The path ".../linux-with-rust-support" is an example and needs to be replaced with the actual path to the Linux kernel source code

Example:

```sh
$ make KDIR=.../linux-with-rust-support LLVM=1
make -C .../linux-with-rust-support M=$PWD
make[1]: Entering directory '.../linux-with-rust-support'
  RUSTC [M] .../rust-out-of-tree-module/rust_out_of_tree.o
  MODPOST .../rust-out-of-tree-module/Module.symvers
  CC [M]  .../rust-out-of-tree-module/rust_out_of_tree.mod.o
  LD [M]  .../rust-out-of-tree-module/rust_out_of_tree.ko
make[1]: Leaving directory '.../linux-with-rust-support'
```
Insert the module using the following command:

```
sudo insmod .../rust-out-of-tree-module/rust_out_of_tree.ko
```

For details about the Rust support, see https://github.com/Rust-for-Linux/linux.

For details about out-of-tree modules, see https://www.kernel.org/doc/html/latest/kbuild/modules.html.
