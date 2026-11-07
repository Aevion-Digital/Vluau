# VLuau

**VLuau** is Voxelgia's implementation of the Luau programming language, developed and maintained by the Voxel Team for the Voxelgia game creation platform.

VLuau is based on the official open-source [Luau](https://github.com/luau-lang/luau) programming language. It provides a fast, safe, gradually typed scripting environment designed for creating interactive experiences in Voxelgia.

VLuau replaces VXLua as Voxelgia's primary scripting language beginning with **Voxelgia 1.2.0 "Do More."**

Unlike VXLua, VLuau uses the actual Luau compiler, virtual machine, and language implementation. This allows Voxelgia to benefit from upstream language improvements without independently recreating language functionality.

## Overview

VLuau is designed around three primary goals:

- **Compatibility:** Preserve Luau's syntax, language behavior, and supported standard libraries.
- **Integration:** Provide direct access to Voxelgia's game objects, events, properties, and scripting APIs.
- **Consistency:** Use a shared scripting architecture across single-player and multiplayer environments.

VLuau is not a new programming language or a recreation of Luau. It is an integration of the existing Luau language with Voxelgia-specific functionality.

The underlying language is derived from Lua 5.1 and includes additional features such as type annotations, type inference, and performance improvements.

For general language documentation, visit [luau.org](https://luau.org/).

## VLuau and Voxelgia

VLuau provides the scripting foundation for Voxelgia experiences.

Scripts can interact with the game world through APIs provided by Voxelgia.

These APIs are responsible for connecting Luau code to the underlying Godot engine.

Planned and supported functionality may include:

- Accessing and modifying game objects.
- Reading and changing object properties.
- Responding to events.
- Working with players and characters.
- Managing world interactions.
- Executing functions and scheduled tasks.
- Interacting with supported game services.

The availability of individual APIs depends on the Voxelgia version and execution environment.

VLuau does not automatically include Roblox's game APIs. Although both platforms use Luau, Voxelgia provides its own object model and engine bindings.

## Execution environments

VLuau is designed to provide consistent scripting behavior across Voxelgia's supported environments.

### Single-player

In single-player experiences, gameplay scripts execute locally.

The client manages the local world and processes script-driven gameplay behavior.

### Multiplayer

In multiplayer experiences, authoritative gameplay scripts execute on the dedicated server.

The server manages authoritative world state and replicates relevant changes to connected clients.

This preserves Voxelgia's server-authoritative multiplayer architecture.

### Shared runtime

Both environments use the same underlying Luau language implementation and Voxelgia scripting interfaces.

The objective is to minimize behavioral differences between single-player and multiplayer.

Execution permissions and authority may differ between environments, but the underlying language behavior remains consistent.

## Legacy Scripts

Before VLuau, Voxelgia used a custom scripting language called VXLua.

Beginning with Voxelgia 1.2.0, VXLua is classified as **Legacy Scripts**.

Legacy Scripts remain available for compatibility with existing experiences.

- Existing VXLua scripts continue functioning.
- Creators can continue editing Legacy Scripts.
- New Legacy Scripts can still be created.
- Existing projects do not require conversion.
- Legacy Scripts no longer receive regular feature updates.

VLuau is recommended for all new scripting projects.

Documentation for VXLua is maintained separately in the Legacy Scripts section of the Voxelgia documentation.

## Architecture

VLuau uses the official Luau compiler and virtual machine.

The scripting system is integrated with Voxelgia through a shared runtime interface.

The architecture consists of:

| Component | Purpose |
|---|---|
| Luau Compiler | Compiles Luau source code into bytecode |
| Luau VM | Executes compiled scripts |
| Voxelgia Bindings | Connects scripts to game functionality |
| Script Manager | Manages script loading and lifecycle |
| Event System | Handles script events and callbacks |
| Execution Context | Controls permissions and authority |
| Legacy Runtime | Preserves compatibility with VXLua |

VLuau uses native Luau execution rather than translating Luau code into GDScript or Python.

## Building VLuau

VLuau is based on the upstream Luau source code.

The initial integration baseline is **Luau 0.746**.

Luau is implemented primarily in C++ and uses CMake for building.

### Requirements

- CMake
- A compatible C++ compiler
- C++17 support for compiler and analysis components
- Godot 4.6 development environment for Voxelgia integration

### Building the upstream Luau tools

From the Luau source directory:

```sh
cmake -S . -B build -DCMAKE_BUILD_TYPE=RelWithDebInfo
cmake --build build --target Luau.Repl.CLI --config RelWithDebInfo
cmake --build build --target Luau.Analyze.CLI --config RelWithDebInfo
```

These commands build the upstream Luau command-line tools.

They do not independently build the complete Voxelgia runtime integration.

### Embedding Luau

The VLuau integration uses Luau's native embedding API.

At minimum, an application embedding Luau typically requires:

- `Luau.Compiler`
- `Luau.VM`

Source code is compiled into Luau bytecode and loaded into the VM for execution.

For implementation details, see the [Luau C API documentation](https://luau.org/api).

## Security

VLuau is intended to execute user-authored scripts within controlled environments.

The integration should use Luau's supported sandboxing mechanisms and restrict access to unsafe host functionality.

Security considerations include:

- Isolated script environments.
- Restricted operating-system access.
- Controlled game API permissions.
- Script execution limits.
- Memory management.
- Server-authoritative multiplayer execution.
- Safe error handling.

The Luau VM provides language-level sandboxing features, while Voxelgia is responsible for enforcing its own engine and multiplayer security boundaries.

## Testing

VLuau development should include testing for:

- Language compatibility.
- Script compilation and execution.
- Engine API bindings.
- Single-player behavior.
- Multiplayer behavior.
- Legacy Script compatibility.
- Runtime stability.
- Windows and macOS integration.
- Dedicated server execution.

The upstream Luau project provides its own compiler, analysis, and VM conformance test suites.

Voxelgia-specific integrations require additional testing.

## Compatibility with upstream Luau

VLuau aims to remain compatible with the official Luau language.

Voxelgia-specific functionality should be implemented primarily through host API bindings rather than unnecessary modifications to the language itself.

This approach simplifies upstream updates and reduces maintenance requirements.

Upstream Luau language changes are not automatically included in VLuau. They must be incorporated and tested against Voxelgia's integration.

## Documentation

- [Official Luau Documentation](https://luau.org/)
- [Luau GitHub Repository](https://github.com/luau-lang/luau)
- [Luau C API](https://luau.org/api)
- [Luau Type Checking](https://luau.org/typecheck)
- [Luau Compatibility](https://luau.org/compatibility)
- [Luau RFCs](https://github.com/luau-lang/rfcs)

Voxelgia-specific scripting documentation is provided through the Voxelgia developer documentation.

## License and attribution

VLuau is based on the open-source Luau programming language.

Luau is developed by Roblox and its open-source contributors and is distributed under the **MIT License**.

Luau itself is derived from Lua 5.x, which is also distributed under the MIT License.

Voxelgia and the Voxel Team acknowledge the original Luau developers and contributors.

The original Luau license and copyright notices must be preserved in distributions containing Luau source code or binaries, as required by the applicable license.

Original project: https://github.com/luau-lang/luau

Copyright and trademarks associated with Roblox and Luau remain the property of their respective owners.

VLuau is an independent Voxelgia integration and is not an official Roblox product.
