
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

### 2. 补丁应用失败的问题

根据错误信息，补丁`rust-oe-selftest.patch`在应用时遇到了问题。这可能是由于以下原因：

- **补丁与代码版本不匹配**：确保补丁是基于你当前正在使用的Rust代码版本创建的。如果版本不匹配，补丁可能无法正确应用。

- **文件路径问题**：检查补丁中的文件路径是否与你的代码库中的文件路径一致。如果不一致，可能需要调整文件路径或使用`git mv`命令移动文件到正确的位置。

- **手动解决冲突**：如果补丁应用过程中出现冲突，可能需要手动编辑冲突的文件，解决冲突后再次尝试应用补丁。

- **使用`-f`强制应用补丁**：如果确定补丁应该可以应用，但出现了错误，可以尝试使用`-f`选项强制应用补丁，但这可能会导致更多的问题，因此不推荐作为首选解决方案。

综上所述，解决这个问题需要你检查系统文件句柄限制，并确保补丁与代码版本匹配，同时检查文件路径是否正确。如果问题仍然存在，可能需要更详细的错误日志来进一步诊断问题。



---

