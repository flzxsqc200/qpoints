# qpoints
Qemu tracing plugin using SimPoints AAAA

Compiling
---
Set QEMU_DIR to point to the qemu source folder before running make.

```
$ export QEMU_DIR=/path/to/qemu
$ make
```

Running
---

$ ./qemu-aarch64 -d plugin -plugin ../../qpoints/libbbv.so,arg=<bench_name> /path/to/benchmark/

You should see two files: <bench_name>_bbv.gz and <bench_name>_pc.txt

The bbv file is processed by the SimPoints binary to create the simpoints and
weights file.

$ ./SimPoint.3.2/bin/simpoint -inputVectorsGzipped -loadFVFile <bench_name>_bbv.gz -k 10 -saveSimpoints <bench_name>.simpts  -saveSimpointWeights <bench_name>.weights

The generated simpts and weights file are used by the tracer plugin to generate
traces.

Then you run tracer to generate the traces.

$ ./qemu-aarch64 -d plugin -plugin ../../qpoints/libtracer.so,arg=<bench_name> /path/to/benchmark/

Related
---

See http://web.eece.maine.edu/~vweaver/projects/qemusim/

