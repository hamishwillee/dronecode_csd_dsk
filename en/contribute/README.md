# Contributing

Pull-requests are accepted on GitHub. Make sure to check coding style with the
provided script in tools/checkpatch, check for memory leaks with *valgrind* and
test on real hardware.

### Valgrind

In order to avoid seeing a lot of *glib* and *gstreamer* false positives memory leaks it is recommended to run *valgrind* using the following command:
```
GDEBUG=gc-friendly G_SLICE=always-malloc valgrind --suppressions=valgrind.supp --leak-check=full --track-origins=yes --show-possibly-lost=no --num-callers=20 ./csd
```
