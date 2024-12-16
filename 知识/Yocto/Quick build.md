
# P1-Too many open files

## Description
```
ERROR: rust-native-1.79.0-r0 do_patch: Applying patch 'rust-oe-selftest.patch' on target directory '/home/lxh/workspace/yocto/poky/build/tmp/work/x86_64-linux/rust-native/1.79.0/rustc-1.79.0-src'
CmdError('quilt --quiltrc /home/lxh/workspace/yocto/poky/build/tmp/work/x86_64-linux/rust-native/1.79.0/recipe-sysroot-native/etc/quiltrc push', 0, "stdout: Applying patch rust-oe-selftest.patch
patching file compiler/rustc_errors/src/markdown/tests/term.rs
patching file compiler/rustc_interface/src/tests.rs
patching file library/test/src/stats/tests.rs
patching file library/std/src/io/buffered/tests.rs
patching file library/std/src/io/stdio/tests.rs
patching file library/std/src/sync/mpsc/sync_tests.rs
patching file library/std/src/sync/mpsc/tests.rs
patching file library/std/src/sync/mutex/tests.rs
patching file library/std/src/sync/rwlock/tests.rs
patching file library/std/src/sys/pal/unix/process/process_unix/tests.rs
patching file library/std/src/thread/tests.rs
patching file library/alloc/src/slice/tests.rs
patching file library/test/src/tests.rs
patching file library/std/src/sync/mutex/tests.rs
patch: **** Can't create temporary file library/std/src/sync/mutex/tests.rs.oekZrCL : Too many open files
Patch rust-oe-selftest.patch does not apply (enforce with -f)

```

## FIX
### 1. 解决“Too many open files”错误

这个错误通常发生在系统打开的文件句柄数量超过了系统允许的最大值。在Linux系统中，可以通过以下步骤解决这个问题：

- **临时解决方案**：增加系统允许打开的文件句柄数量。可以通过`ulimit -n`查看当前的限制，并使用`ulimit -n <新的限制>`来增加这个限制。

- **永久解决方案**：编辑`/etc/security/limits.conf`文件，添加或修改以下行来永久增加限制：
  ```
  * soft nofile <新的限制>
  * hard nofile <新的限制>
  ```
  其中`<新的限制>`是你希望设置的文件句柄数量。

- **检查并关闭不必要的文件句柄**：检查你的程序或系统中是否有文件句柄泄漏，即程序中打开的文件没有被正确关闭。这可能需要代码审查或使用工具来监控文件句柄的使用情况。




---


# P2 容易下载失败


## Description

```
Fetch errors
WARNING: json-c-0.17-r0 do_fetch: Failed to fetch URL https://s3.amazonaws.com/json-c_releases/releases/json-c-0.17.tar.gz, attempting MIRRORS if available
WARNING: orc-0.4.40-r0 do_fetch: Failed to fetch URL http://gstreamer.freedesktop.org/src/orc/orc-0.4.40.tar.xz, attempting MIRRORS if available

```

## FIX

![[Pasted image 20241216112435.png]]


