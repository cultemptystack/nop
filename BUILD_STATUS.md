# v0.1.0 build status

Prepared with Go 1.27.1, `CGO_ENABLED=0`, no third-party modules, and network
access disabled during compilation. Release files include this record.

| Target | Compiled | Runtime validation |
| --- | --- | --- |
| Windows amd64 | Yes | Core tests and native hidden-console integration tests passed; packaged executable CLI checks passed |
| Windows arm64 | Yes | Compiled only; not executed on ARM hardware |
| Linux amd64 | Yes | Core tests, native PTY tests, and packaged executable CLI/interactive checks passed in Ubuntu on WSL2 (x86-64) |
| Linux arm64 | Yes | Compiled only; not executed on ARM hardware |

The native tests cover normal completion, Ctrl+C / Enter / Space, immediate
emergency exit, handled termination, and an injected output failure. Windows
tests verify the original screen contents, cursor visibility, and input/output
modes; Linux tests verify termios restoration, silent typing, and screen/cursor
restoration sequences. Deterministic tests check message expiry, virtual-cycle
arithmetic, escape timing, fixed deadlines, and the 10 Hz refresh limit.
The packaged Linux executable also passed completion, emergency exit, and a
real OS-delivered SIGTERM, including final text, exit codes, and restoration.

`go vet ./...` passed for Windows amd64 and Linux amd64. All four binary
architecture headers, archive contents, and SHA-256 checksums were verified.
The binaries are approximately 1.6–1.8 MiB each (archives under 1 MiB).

Windows testing used an isolated native console, not a manual Windows Terminal
session. Linux testing used a real PTY under WSL2, not a standalone Linux
desktop. ARM runtime testing and the GitHub workflows have not been run.
The archives are prepared locally; no GitHub release has been published.
