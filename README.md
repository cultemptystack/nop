# nop

**Do nothing. Properly.**

A tiny, offline stillness timer from **c∅s — Cult of the Empty Stack**.

```sh
nop             # 60 seconds
nop 30s         # 30 seconds
nop 5m          # five minutes
nop --help
nop --version
```

`STILLNESS INITIALIZED.` appears for a moment. The terminal becomes almost
entirely blank. A small counter at the bottom records elapsed **virtual cycles**.
Your existing terminal colors remain in use. The requested timer starts when
the alternate screen opens, after the brief initialization.

The rate is fictional: **1,000,000,000 virtual cycles per second**. The count is
elapsed monotonic time in nanoseconds, capped at the session duration. It never
reads a hardware performance counter, measures CPU cycles, or burns CPU to
produce the number. The process blocks while waiting for input or its next
deadline; the screen updates at most ten times per second. Clock adjustments do
not affect the timer. System sleep follows the platform's monotonic clock;
this is not a wall-clock alarm.

| Input | Response |
| --- | --- |
| Ctrl+C | `INTERRUPT RECEIVED. NOTHING CHANGED.` |
| Enter | `THERE IS NOTHING TO SUBMIT.` |
| Space | `NOTHING REQUIRES YOUR INPUT.` |

Each response disappears after about two seconds. New responses replace old
ones. The timer keeps running. Other keys do not echo.

**Emergency exit: press Escape three times within two seconds.**
The original screen and input settings return, followed by:

```text
STILLNESS ABANDONED.
```

On normal completion, the original screen and input settings return, followed by:

```text
0 OPERATIONS COMPLETED SUCCESSFULLY.

c∅s
```

The refusal to stop is theatrical. `nop` is an ordinary process: Linux
`kill -TERM <pid>` and operating-system process controls can terminate it.
Handled termination signals and errors attempt full cleanup. Force-killing a
process (`SIGKILL`, forced Task Manager termination), a terminal crash, or power
loss cannot run cleanup; if needed, restore a Linux terminal with `stty sane`
and `printf '\033[?25h\033[?1049l'`.

## Install

Download an archive for your OS and CPU from
[Releases](https://github.com/cultemptystack/nop/releases), extract it, and put
`nop` (Linux) or `nop.exe` (Windows) on your `PATH`. There is no installer or
runtime dependency. See [BUILD_STATUS.md](BUILD_STATUS.md) for the validation
record of the prepared v0.1.0 builds; a compiled target is not automatically
a tested target.

In PowerShell, run an extracted executable with `./nop.exe 30s`. On Linux,
run `./nop 30s` (the archive preserves its executable permission).

Supports Windows and Linux on amd64 and arm64. Use Windows Terminal / a modern
Windows console, or an ANSI alternate-screen terminal on Linux. Redirected and
unsupported terminals are rejected before interactive mode. Durations must be
positive; invalid arguments never change the terminal.

## Distribution

This repository provides compiled Windows and Linux downloads, usage
documentation, and release information. The development source is not
published here. Each download includes the full MIT license.

## License

[MIT](LICENSE).
