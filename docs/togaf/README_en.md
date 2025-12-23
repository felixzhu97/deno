# Deno Project TOGAF Enterprise Architecture Diagrams

This document contains complete TOGAF (The Open Group Architecture Framework) enterprise architecture views based on the actual architecture of the Deno project.

## Architecture View Overview

This directory contains four TOGAF standard architecture views, drawn in PlantUML format. Each view has both Chinese and English versions:

**English Version Files:**
- `business_architecture_en.puml` - Business Architecture View
- `application_architecture_en.puml` - Application Architecture View
- `data_architecture_en.puml` - Data Architecture View
- `technology_architecture_en.puml` - Technology Architecture View

**Chinese Version Files:**
- `business_architecture.puml` - 业务架构视图
- `application_architecture.puml` - 应用架构视图
- `data_architecture.puml` - 数据架构视图
- `technology_architecture.puml` - 技术架构视图

### 1. Business Architecture View (`business_architecture_en.puml`)

Describes the business capabilities, business processes, and business services of the Deno project.

**Main Content:**
- **Business Capability Layer**: JavaScript/TypeScript runtime capability, developer tools capability, package management capability, language service capability
- **Business Process Layer**: Code execution process, module loading process, toolchain process, testing process, build process
- **Business Service Layer**: CLI service, LSP service, test service, build service, format service, lint service
- **External Stakeholders**: Developers, IDEs/editors, CI/CD systems

**Key Mappings:**
- Business capabilities support business processes
- Business processes implement business services
- Business services serve external stakeholders

### 2. Application Architecture View (`application_architecture_en.puml`)

Describes the application component structure and interaction relationships of the Deno project.

**Main Layers:**
- **CLI Application Layer** (`cli/`): Command line interface, argument parsing, tools, module loader, type checker, LSP server
- **Runtime Layer** (`runtime/`): JavaScript runtime, worker management, permission system, code cache, snapshot system
- **Extension Layer** (`ext/`):
  - Web API extensions: Fetch, WebSocket, WebGPU, Canvas, WebStorage
  - System extensions: File system, network, HTTP, crypto, process, signals
  - Node.js compatibility: Node.js API, NAPI
  - Other extensions: KV store, cron, FFI
- **Shared Library Layer** (`libs/`): Config management, Node resolver, NPM cache, NPM installer, package JSON, resolver library
- **Tool Applications**: Format, lint, test, build, doc, package management

**Key Relationships:**
- CLI layer calls runtime layer
- Runtime layer manages extension layer
- Extension layer uses shared library layer
- Tool applications depend on runtime and extensions

### 3. Data Architecture View (`data_architecture_en.puml`)

Describes the data entities, data access, and data storage of the Deno project.

**Data Entities:**
- **Module Data**: Module graph, dependencies, module metadata
- **Cache Data**: Code cache, module cache, type check cache, incremental compile cache
- **Configuration Data**: deno.json, package.json, import_map.json, tsconfig.json
- **Registry Data**: JSR registry, NPM registry, package metadata, version information
- **Runtime Data**: Permission descriptors, environment variables, workspace state

**Data Access Layer:**
- Module graph builder, cache manager, config loader, registry client, file system access

**Data Storage Layer:**
- Local file system, Deno cache directory, SQLite database, memory cache

**Data Flows:**
- Module resolve flow, cache update flow, config read flow, package download flow

### 4. Technology Architecture View (`technology_architecture_en.puml`)

Describes the technology stack and platform dependencies of the Deno project.

**Technology Layers:**
- **Application Technology Layer**: Deno CLI, Deno Runtime, extension system
- **Runtime Technology Layer**:
  - V8 JavaScript Engine: Executes JavaScript/TypeScript code
  - Rust Runtime: Provides type safety and memory safety
  - Tokio Async Runtime: Handles async I/O operations
  - deno_core: V8 bindings and extension mechanism
- **System Interface Layer**:
  - Operating system interfaces: File system, network, process, signals
  - Security layer: Permission system, sandbox mechanism, resource isolation
- **Platform Technology Layer**:
  - Compilation toolchain: Rust compiler, Cargo build system, LLVM backend
  - Network technology: HTTP client, WebSocket, TLS/SSL, DNS resolver
  - Storage technology: SQLite, file system, memory management
- **Infrastructure Layer**:
  - Operating systems: Linux, macOS, Windows
  - Hardware platforms: x86_64, ARM64

## How to Use These Architecture Diagrams

### Viewing Architecture Diagrams

1. **Online Viewing**:
   - Visit [PlantUML Online Server](http://www.plantuml.com/plantuml/uml/)
   - Copy the content of `.puml` files to the online editor
   - Or use IDE plugins that support PlantUML (such as VS Code PlantUML extension)

2. **Local Generation**:
   ```bash
   # Install PlantUML (requires Java)
   # macOS
   brew install plantuml
   
   # Generate PNG images
   plantuml docs/togaf/*.puml
   ```

3. **VS Code Plugin**:
   - Install "PlantUML" extension
   - Open `.puml` files
   - Use `Alt+D` to preview diagrams

### Architecture Diagram Usage

- **Business Architecture View**: Used to understand Deno's business value and capabilities, present project value to business decision makers
- **Application Architecture View**: Used to understand code organization structure, guide development and maintenance work
- **Data Architecture View**: Used to understand data flows and storage mechanisms, optimize caching and performance
- **Technology Architecture View**: Used to understand technology stack dependencies, evaluate technology choices and platform compatibility

## Architecture Mapping Relationships

### Code Directory to Architecture View Mapping

| Code Directory | Business Architecture | Application Architecture | Data Architecture | Technology Architecture |
|---------------|----------------------|---------------------------|-------------------|------------------------|
| `cli/` | CLI Service | CLI Application Layer | - | Deno CLI |
| `runtime/` | Runtime Capability | Runtime Layer | - | Deno Runtime |
| `ext/` | Feature Extensions | Extension Layer | - | Extension System |
| `libs/` | Shared Capabilities | Shared Library Layer | - | - |
| `cli/cache/` | - | - | Cache Data | - |
| `cli/module_loader.rs` | Module Loading Process | Module Loader | Module Data | - |
| `runtime/permissions/` | Security Service | Permission System | Permission Descriptors | Security Layer |
| V8 Engine | - | - | - | V8 JavaScript Engine |
| Rust/Tokio | - | - | - | Rust Runtime/Tokio |

## Architecture Design Principles

Based on the actual architecture of the Deno project, these views reflect the following design principles:

1. **Layered Architecture**: Clear layer division with explicit responsibilities for each layer
2. **Modular Design**: Functional modularity through extension system
3. **Security First**: Deny-by-default permission model
4. **Performance Optimization**: Multi-level caching mechanism
5. **Cross-platform Support**: Support for multiple operating systems and hardware platforms
6. **Standard Compliance**: Support for Web standards and Node.js compatibility

## Update Notes

These architecture diagrams are generated based on the current code structure of the Deno project. When the project architecture changes, these views should be updated accordingly to maintain accuracy.

## References

- [TOGAF Standard](https://www.opengroup.org/togaf)
- [PlantUML Documentation](https://plantuml.com/)
- [Deno Project Documentation](../CLAUDE.md)
- [Deno Official Documentation](https://docs.deno.com)

