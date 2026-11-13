# LocalAI v4.12.1 with maintained llama.cpp

This recipe produces a Linux amd64 LocalAI image with the maintained
`pi0n00r/llama.cpp` backend installed as a system backend.

`latest` is resolved once at preparation time. `SOURCE.lock` records the exact
LocalAI source, upstream runtime image, llama.cpp source, ROCm base, gRPC builder,
platform, and GPU target used by the build. The floating source branch is never
consulted during the build.

LocalAI v4.12.1 carries a score-task patch for its llama.cpp backend. Current
llama.cpp changed the checkpoint container and renamed the logits predicate, so
this recipe installs the source-equivalent rebased patch recorded in
`SOURCE.lock`. The patch is hash-checked before the backend build; it is not a
runtime modification.

The old LocalAI TTS patch is also hash-checked and then removed. Its feature set
is native in the pinned llama.cpp ancestry through commit `5c0b49a23`; applying
the pre-upstream patch again would reverse or duplicate that implementation.
The backend compile remains the joined compatibility gate for LocalAI's gRPC
wrapper and these native llama.cpp APIs.

Published tags:

- `ghcr.io/pi0n00r/localai:v4.12.1-llama-72500667f`
- `ghcr.io/pi0n00r/localai:v4.12.1-llama-latest`

The second tag is a convenience alias for the same immutable image digest. It
does not make the build floating or automatically update production.

The image targets ROCm 7.2.1 and `gfx1151`. The backend lives at
`/var/lib/local-ai/backends/llama-cpp`, leaving `/backends` available for
operator-managed backends. User-installed backends retain LocalAI's normal
precedence over the embedded system backend.

This is a build artifact, not a production promotion. Promotion still requires
the established full-context, LocalAI routing, tool-call, structured-output,
authentication, dual-stack, and running-hash gates on the target host.
