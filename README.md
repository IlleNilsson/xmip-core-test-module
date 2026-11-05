# xmip-core-test-module

An external module: a content contract built by itself, in Rust here, and
loaded over the ABI rather than linked. ADR-0012 makes `include/xmip_module.h`
in xmip-core-abi the boundary it conforms to; an external module or assembly
handles its own compilation, not Xmip (ADR-0042, amendment 2026-11-05). It is
what the runtime's loader is tested against, so it mounts beside the
Essentials, under `test/core`.

What it claims today: well-formedness is bytes, every Stream is read to its end
and held (ADR-0042 decision 1). A descriptor a Location binds is kept and
answered by `implies`. A contract with a real standard replaces the one
judgment function and nothing else; the entrypoint, the table and the lifecycle
are done.

## Verification

xgit builds and tests it with cargo like any crate. The runtime's
`ffi::loaded_contract` tests then open the built library through the host's
loader and hold it to the contract table (ADR-0057).
