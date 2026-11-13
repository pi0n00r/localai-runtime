# Build receipt

Built 2026-11-13 on GitHub-hosted Linux amd64 builders from recipe commit
`e330f113833eca8218223cf3ab938a136f24c1ca`.

## Locked sources

- LocalAI v4.12.1: `ec9274027eadd552d56f2c6c1fe86cd9216a991a`
- pi0n00r/llama.cpp `latest` resolution: `72500667f88c6b7ed2e6ebbc308d8759a0a5afea`
- Platform: `linux/amd64`
- Backend: ROCm 7.2.1 HIP, `gfx1151`

## Published images

Backend:

- `ghcr.io/pi0n00r/localai-llama-backend:v4.12.1-llama-72500667f`
- OCI index: `sha256:e71b428ef390313d7ea2e42ba50b8f90a51d0ca84b81888c421df208cfa94ad4`
- Linux amd64 manifest: `sha256:4843d788ab1451cae5f000a87c2e2a3d613dcb4ddb4b5f8bc415becb4abc9ae4`

Runtime:

- `ghcr.io/pi0n00r/localai:v4.12.1-llama-72500667f`
- `ghcr.io/pi0n00r/localai:v4.12.1-llama-latest`
- OCI index for both tags: `sha256:4d0c5fea608069831fdcaa6de2be9dd95888b46e2f9b35812fc6de10145a0de4`
- Linux amd64 manifest: `sha256:106c64c395dc185ebb7c8a107710b955dd9e5430c1dc282b620ba5f30dc58b42`

Both OCI indexes include a BuildKit attestation manifest with provenance and
SBOM predicates. The runtime labels bind the exact LocalAI and llama.cpp
commits and `llama-cpp/hipblas/gfx1151` backend identity.

## Verification

Backend build and link completed in run
[`43374127450`](https://github.com/pi0n00r/localai-runtime/actions/runs/43374127450).
Its later runtime assembly failed only because the original Dockerfile declared
`LOCALAI_IMAGE` outside global ARG scope; no runtime image was published by that
step. The corrected runtime was assembled from the immutable backend digest and
fully verified in successful run
[`43378794232`](https://github.com/pi0n00r/localai-runtime/actions/runs/43378794232).

The successful run checked the source labels, embedded backend executable,
`/local-ai` executable, and `/local-ai --version`. Anonymous GHCR manifest
