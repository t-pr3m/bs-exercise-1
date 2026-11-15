# Feedback Arc Set

A compact systems programming project in C, focused on coordination between independent processes. A supervisor and multiple generators exchange results through POSIX shared memory, using named semaphores to synchronize access to a bounded circular buffer. The programs also handle signals and clean up shared operating-system resources on shutdown.

The generators use randomized vertex orderings to produce candidate solutions; the supervisor tracks the best one received.

## Build

```sh
make
```

To remove the generated binaries and object files:

```sh
make clean
```

## Run

Start the supervisor first, then start one or more generators in other terminals:

```sh
./supervisor -n 3000
./generator 0-1 1-2 2-0
```

Each generator argument describes a directed edge from the first vertex to the second. The supervisor accepts `-n limit` to stop after reading a number of solutions, `-w delay` to wait before reading, and `-o outfile` to also write its final result to a file. Use `./supervisor -h` for the usage message.

The search is randomized, so the best result depends on the orderings tried and may vary between runs. Define `DEBUG=1` when building to enable generator diagnostics:

```sh
make clean && make DEBUG=1
```
