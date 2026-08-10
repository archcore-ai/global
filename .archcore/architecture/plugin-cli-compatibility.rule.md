---
title: "Plugin / CLI Compatibility Across Independent Release Trains"
status: accepted
tags:
  - "architecture"
  - "product"
---

## Rule

The engine (CLI) and the runtime (plugin) ship from separate repositories on separate schedules. Any engine release meets an unknown runtime version, and any runtime release meets an unknown engine version. These obligations bind **both** sides; each repository holds its own enforcement detail.

1. The engine MUST keep the invocation surface the runtime calls — the MCP server, the hook leaves, the health command, and the version flag.
2. WHEN the engine changes an MCP tool response, the change MUST be additive. The engine MUST NOT remove or repurpose a field a released runtime already reads.
3. The engine MUST NOT change its behavior based on whether a runtime is installed.
4. WHEN `archcore hooks` receives an unrecognized host or event, the engine MUST write empty output and MUST exit successfully. Usage text on a hook's protocol channel reaches the model as session context.
5. WHEN the runtime and the project config both route one event to the engine, the engine MUST deduplicate the run.
6. WHEN the engine changes the wire protocol of an existing hook leaf, the change MUST ship in a new release, and the release notes MUST name the host and the leaf. A leaf whose protocol changed inside a version the runtime already gates on cannot be detected by that gate.
7. A version mismatch MUST produce a message and MUST NOT block the session.
8. The runtime MUST gate any dependency on a new engine capability on a minimum engine version.
9. The runtime MUST NOT write the `globals` key of `.archcore/settings.json`; that key is the consumer repository's own declaration.
10. Executable code in the runtime MUST NOT branch on an MCP response field that an older engine does not send. A prompt MAY read such a field when the absent-field path matches the behavior without it.
11. WHEN the engine ships a guardrail the runtime also implements, the runtime MUST turn its own copy into a delegator rather than keeping a second implementation.

## Rationale

An older engine meeting a newer runtime cannot be fixed from the engine side — released binaries are fixed — so the runtime closes that cell with a minimum-version gate, and the engine closes the reverse cell by making unknown calls harmless. Rules 4 and 7 are what make a newer runtime able to call a leaf an older engine lacks.

Rule 3 keeps the engine independent of another repository's install layout: detection reads a directory the runtime owns, and treating a detection miss as a behavior switch would break the engine whenever that layout changes.

Rule 5 bounds the cost of the overlap window. While an old runtime is installed, both hook entries fire; the result is duplicated advisory output, not a wrong verdict or a corrupted file.

Rule 11 is the standing consequence of `architecture/engine-runtime-boundary`: when a responsibility moves to the engine, leaving the runtime copy in place recreates the two-owner drift the boundary was drawn to end.

## Examples

**Good** — an unknown hook leaf answers with silence, so an older engine meeting a newer runtime costs nothing:

```
$ archcore hooks unknown-host session-start
$ echo $?
0
```

**Good** — the engine reports a possible double run instead of changing behavior:

```
Warning: an Archcore plugin is installed. Until it is updated, its hooks and these may both fire
and you will see duplicated context.
```

**Bad** — usage text on the protocol channel, delivering several hundred bytes of help into the model's context.

**Bad** — a runtime hook script that reads `source_kind` and takes a different branch when the field is missing, so the behavior changes silently on an older engine.

## Enforcement

- **Engine** — silent handling of unknown hosts and events, the dedup stamp, and the installed-runtime notice: `cli/.archcore/integrations/plugin-cli-compatibility.rule`.
- **Runtime** — the minimum-engine-version gate and the property check over its executable code: `plugin/.archcore/plugin/`.
- Either side changing a shared surface updates this rule first, then its own enforcement document.
