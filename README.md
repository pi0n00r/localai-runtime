# LocalAI runtime images

Reproducible LocalAI runtime images pinned to exact upstream and maintained
backend source identities.

The current build combines upstream LocalAI `v4.12.1` with the maintained
`pi0n00r/llama.cpp` backend for Linux amd64, ROCm 7.2.1, and `gfx1151`.
See [`v4.12.1-llama-latest/README.md`](v4.12.1-llama-latest/README.md) and its
machine-readable `SOURCE.lock`.

Builds publish to `ghcr.io/pi0n00r/localai`. Friendly tags are aliases to
digest-addressed images; production promotion is deliberately separate.
