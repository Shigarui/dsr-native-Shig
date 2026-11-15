# AGENTS.md

Guidance for AI coding agents (Claude Code, Gemini CLI, Codex) working in this repo.

## Math checks with ucas (shaders and floating point)
For shader math, floating-point accuracy, integer overflow or bit-level tricks, check the math with the `ucas` MCP server ([scarletnx/ucas](https://github.com/scarletnx/ucas)) instead of guessing:
- `error` / `fit`: measure the max error of an approximation against the reference function, or find the best magic constant.
- `wrap`: find where integer math overflows and which cases are undefined behavior in C.
- `range`, `find`, `gates`: value ranges and cheaper equivalent expressions or lookup tables.
- GLSL/SPIR-V and fp64-emulation commands: for shaders on mobile GPUs without double precision, and for matching the original console's float behavior.
Record what was checked (function, domain, max error) in HANDOFF.md or the commit message. If the ucas server is not connected, say so and carry on - do not block on it.
