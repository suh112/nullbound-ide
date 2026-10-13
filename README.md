# nullbound-ide
NullBound IDE — A Python/PySide6 desktop IDE for visual FiveM development, Lua code generation, resource building, and framework integrations.  Copy description


# NullBound IDE

**A Visual Development Environment for FiveM Resources**

NullBound IDE is a Windows-focused desktop development environment designed to simplify FiveM resource creation through visual programming, Lua code generation, project management, and integrated development tools.

Built around Python and PySide6, NullBound IDE aims to make FiveM development more accessible to beginners while providing experienced developers with a structured environment for building, editing, validating, and exporting resources.

> **Project status:** Under development. Features and integrations may change between releases.

---

## Overview

Traditional FiveM development requires knowledge of Lua, FiveM natives, resource manifests, framework APIs, and server-side dependencies.

NullBound IDE aims to bring these workflows together in one desktop application.

The project is designed around two complementary development modes:

* **Block Mode** — Build scripts using visual programming blocks without writing Lua manually.
* **Code Mode** — Inspect and edit the generated Lua source directly.

The long-term goal is to support switching between both modes while preserving project data through an internal representation of the program.

## Planned Features

### Visual Programming

* Visual event and command builders.
* Player, vehicle, inventory, and UI blocks.
* Logic, conditions, loops, and variables.
* Custom block definitions.
* Function and callback builders.
* Client, server, and shared execution contexts.
* Searchable block categories.
* Advanced Lua blocks for unsupported or custom logic.

### Lua Development

* Generated Lua source code.
* Integrated code editor.
* Syntax highlighting and code navigation.
* Autocomplete for supported FiveM APIs.
* Search and replace.
* Indentation and formatting tools.
* Diagnostics and validation.
* Block-to-code and code-to-block workflows where supported.

### FiveM Resource Builder

Create and manage FiveM resource projects with configurable files and resource settings.

Planned capabilities include:

* `fxmanifest.lua` generation.
* Client and server script management.
* Shared scripts and configuration files.
* Dependency declarations.
* Project templates.
* Resource validation.
* Resource folder export.
* Optional ZIP packaging.

### Integrations

NullBound IDE is designed to support integrations with selected FiveM resources and libraries.

| Integration  | Planned capabilities                                                  |
| ------------ | --------------------------------------------------------------------- |
| FiveM        | Events, commands, natives, and resource development                   |
| ox_lib       | Notifications, dialogs, progress interfaces, callbacks, and utilities |
| ox_inventory | Inventory operations and item metadata                                |
| nbmysql      | Database operations based on the repository's documented API          |
| nb-dispatch  | Dispatch functionality based on the repository's documented API       |
| MySQL        | Visual query construction and database-related code generation        |

Integration availability depends on implementation status, the installed server resources, and compatibility with the relevant upstream APIs.

### Project Management

* Create and open projects.
* Save and load project settings.
* Store visual programming data.
* Manage project files and dependencies.
* Organize client, server, and shared logic.
* Use a dedicated project format with a `.myfivem` extension, if enabled in the released implementation.

### Validation and Diagnostics

Planned validation features include:

* Block configuration checks.
* Client/server compatibility checks.
* Missing dependency warnings.
* Resource manifest validation.
* Lua syntax diagnostics.
* Integration-specific validation where supported.
* Build error reporting.

### Built-in Documentation

The planned documentation system covers:

* Getting started with FiveM resources.
* Events and commands.
* Client-side and server-side execution.
* Network events and callbacks.
* Lua programming concepts.
* ox_lib and ox_inventory.
* Database integrations.
* nbmysql and nb-dispatch.
* Example projects and common development workflows.

---

## Technology Stack

NullBound IDE is designed around the following technologies:

| Technology           | Purpose                                     |
| -------------------- | ------------------------------------------- |
| Python               | Application logic and tooling               |
| PySide6 / Qt         | Native desktop user interface               |
| Lua                  | Generated FiveM scripts                     |
| JSON                 | Project data and intermediate serialization |
| PyInstaller          | Windows executable packaging                |
| Python testing tools | Automated testing and validation            |

The desktop application is intended to run independently of a FiveM server. Generated Lua resources are intended to be installed and executed by the FiveM server environment.

---

## Architecture

NullBound IDE follows a modular architecture intended to separate the desktop application from the resources it generates.

The core development pipeline is designed around the following flow:

```text
Visual Blocks
     |
     v
Internal Program Representation
     |
     v
Lua Code Generator
     |
     v
Generated FiveM Resource
     |
     v
Validation and Export
```

The internal program representation is intended to preserve block structure, variables, events, functions, project settings, and other supported program elements.

When Lua code cannot be safely represented by existing visual blocks, the intended fallback is an advanced or raw Lua representation rather than silently discarding unsupported code.

The exact level of bidirectional conversion depends on the Lua syntax and features supported by the implementation.

---

## Installation

### Download a Release

When a compiled Windows release is available:

1. Open the repository's **Releases** page.
2. Download the published Windows executable or distribution archive.
3. Extract the archive if necessary.
4. Launch the application.
5. Review the release notes and system requirements before use.

**Releases:** [View Releases](../../releases)

No Python installation should be necessary when using a properly packaged, self-contained Windows release.

### Run from Source

Source code is not distributed through this public repository.

Development builds and source-based installation instructions are available only if explicitly provided through an authorized distribution channel.

---

## Getting Started

The intended workflow is:

1. Create a new FiveM project.
2. Choose a resource template or start with an empty project.
3. Configure the resource name and dependencies.
4. Create the required events, commands, and visual logic.
5. Configure blocks and their inputs.
6. Review the generated Lua code.
7. Validate the project.
8. Build and export the resource.
9. Install the generated resource on your FiveM server.
10. Test the resource in an appropriate development environment.

The availability of individual steps depends on the application version.

---

## Dependencies and Server Setup

NullBound IDE is a development tool, not a replacement for a FiveM server or its dependencies.

Depending on the resource being developed, you may need to install and configure:

* FiveM server artifacts.
* The appropriate server framework, if required.
* ox_lib.
* ox_inventory.
* nbmysql.
* nb-dispatch.
* A compatible MySQL database and database service.
* Any additional resources required by your project.

A dependency must be installed and started in the FiveM server environment before generated code can use it.

NullBound IDE is intended to distinguish between dependency declarations in a generated resource and the actual installation of external server resources.

### External Projects

* **ox_lib:** https://github.com/overextended/ox_lib
* **ox_inventory:** https://github.com/overextended/ox_inventory
* **nbmysql:** https://github.com/suh112/nbmysql
* **nb-dispatch:** https://github.com/suh112/nb-dispatch

External APIs can change between versions. Integration compatibility should be checked against the documentation and source code of the relevant upstream project.

---

## Project Files

A generated resource may contain files such as:

```text
my_resource/
├── fxmanifest.lua
├── client.lua
├── server.lua
├── shared.lua
└── config.lua
```

Only files required by the project should be included in the final resource.

The internal project data is separate from the generated FiveM resource. This allows the development environment to preserve visual programming information and project settings without requiring those editor-specific details to be included in the deployed resource.

---

## Build and Export

The resource builder is designed to:

1. Validate project settings and visual blocks.
2. Check supported execution contexts.
3. Generate Lua source files.
4. Generate the resource manifest.
5. Report errors and warnings.
6. Export the resulting resource directory.
7. Optionally package the resource into a ZIP archive.

A successful export does not guarantee that a resource will work on every server. Runtime behavior also depends on server configuration, installed dependencies, permissions, framework versions, and the validity of the underlying game API calls.

---

## Security

NullBound IDE is intended to function as a development and code-generation application.

Generated Lua code is intended for use in the FiveM environment. The desktop application should not automatically execute arbitrary generated Lua as operating-system commands.

Users should review generated scripts before installing them on a live server.

Only install resources and dependencies from sources you trust.

---

## Privacy and Distribution

NullBound IDE is distributed as a proprietary application unless a separate license explicitly states otherwise.

The public repository does not imply that the application's source code is available.

Depending on the release, executable downloads, documentation, and release notes may be provided without exposing internal implementation details.

---

## Licensing

**All rights reserved unless otherwise stated in a separate license or written authorization.**

This repository's README does not grant permission to copy, modify, redistribute, reverse engineer, or commercially exploit proprietary application components.

Third-party dependencies remain subject to their respective licenses.

If a formal proprietary software license is published, that license takes precedence over this summary.

---

## Project Status

NullBound IDE is under active development.

The feature list describes the intended scope of the project and does not guarantee that every feature is available in every release.

Features should be considered implemented only when they are included in a published version and documented in its release notes.

---

## Support and Updates

For product announcements, supported releases, and public documentation, follow this repository.

For technical issues, include the application version, relevant error messages, and steps to reproduce the problem. Do not publish private source code, access tokens, database credentials, server secrets, or sensitive player information in issue reports.

---

**NullBound IDE — Build FiveM resources visually. Develop with confidence.**
