---
type: project
created: 2026-10-22
status: active
priority: high
tags:
  - project
  - python
  - android
  - cli
---

## Cross-Platform Android Application Debugging CLI

**Project Brief and Technical Blueprint**

**Version:** 0.1  
**Status:** Proposed / Initial Development  
**Target Platforms:** Windows, Linux, macOS  
**Primary Target:** Android applications  
**Language:** Python

---

## 1. Executive Summary

**DroidLens** is a cross-platform, terminal-based Android application debugging and observability tool designed to simplify the process of inspecting and diagnosing running Android applications.

It provides a unified command-line interface for discovering connected devices, identifying installed applications, attaching to running processes, streaming application-specific logs, and diagnosing common debugging environment issues.

Instead of requiring developers to manually execute multiple Android Debug Bridge (ADB) commands, DroidLens offers a structured, consistent, and extensible debugging experience.

### Core vision

> A lens into what's happening inside your Android application.

DroidLens aims to evolve from a lightweight Android debugging CLI into a unified debugging and observability platform with capabilities for application logs, crash detection, network inspection, performance monitoring, and framework-specific diagnostics.

---

## 2. Problem Statement

Android developers frequently rely on ADB and multiple development tools to investigate application behavior.

Typical manual workflow:

```bash
adb devices
adb shell pm list packages
adb shell pidof com.example.app
adb logcat --pid=12345
```

This workflow introduces several challenges:

- Repetitive command execution.
    
- Manual process and package identification.
    
- Difficulty filtering useful logs from noisy output.
    
- Inconsistent debugging workflows across projects.
    
- Limited integration between logs and debugging sessions.
    
- Lack of a unified terminal-based debugging experience.
    

DroidLens addresses these issues by combining common debugging operations into a single CLI.

### Proposed solution

```bash
droidlens attach com.example.app
```

This command should:

1. Detect connected Android devices.
    
2. Select the appropriate device.
    
3. Verify that the specified package exists.
    
4. Identify the application's running process.
    
5. Establish a debugging session.
    
6. Stream relevant application logs.
    
7. Display logs in a readable terminal interface.
    

---

## 3. Goals and Non-Goals

### Project goals

- Build a cross-platform CLI compatible with Windows, Linux, and macOS.
    
- Simplify Android application debugging.
    
- Provide reliable ADB integration.
    
- Stream application-specific logs in real time.
    
- Introduce structured debugging sessions.
    
- Maintain a modular architecture for future capabilities.
    
- Support automation and machine-readable output in future releases.
    
- Provide a straightforward installation and setup experience.
    

### Initial non-goals

The first release will not attempt to:

- Intercept HTTPS traffic.
    
- Replace Android Studio or Flutter DevTools.
    
- Debug iOS applications.
    
- Perform advanced memory profiling.
    
- Provide a graphical user interface.
    
- Automatically diagnose every application exception.
    
- Modify application binaries or bypass Android security restrictions.
    

Keeping these limitations explicit helps prevent scope expansion during MVP development.

---

## 4. Target Users

DroidLens is intended for:

- Android developers.
    
- Flutter developers.
    
- React Native developers working with Android.
    
- Mobile QA engineers.
    
- Backend engineers investigating mobile API-related errors through application logs.
    
- Developers who prefer terminal-based workflows.
    

The initial target audience is developers who already have Android SDK platform tools installed and use ADB regularly.

---

## 5. Cross-Platform Compatibility

Cross-platform support is a foundational requirement, not a later enhancement.

### Supported host operating systems

|Operating system|Support|
|---|---|
|Windows 10/11|Planned|
|Linux|Planned|
|macOS|Planned|

The debugging target remains Android regardless of the host operating system.

### Architecture

```text
          Windows
             |
          Linux
             |
           macOS
             |
             v
      +--------------+
      |  DroidLens   |
      |     CLI      |
      +--------------+
             |
      +--------------+
      |  Core Layer  |
      +--------------+
             |
      +--------------+
      | ADB Adapter  |
      +--------------+
             |
      +--------------+
      | Android ADB  |
      +--------------+
             |
      +--------------+
      | Android App  |
      +--------------+
```

### Cross-platform design principles

**1. Avoid OS-specific business logic**

Application services should not contain Windows, Linux, or macOS-specific branches.

**2. Use platform-independent process execution**

Use Python's subprocess APIs with argument arrays instead of shell command strings.

**3. Use pathlib for filesystem operations**

Avoid manually constructing paths using OS-specific separators.

**4. Handle process lifecycle differences**

Account for different process termination, signal, and terminal behavior.

**5. Detect ADB dynamically**

Do not assume that ADB exists in a particular installation directory.

**6. Validate through automated testing**

Run the same test suite across all three host operating systems.

The goal is to make the application layer OS-independent and isolate any necessary platform-specific behavior in infrastructure.

---

## 6. Recommended Technology Stack

|Component|Technology|Purpose|
|---|---|---|
|Language|Python 3.12+|Core implementation|
|CLI framework|Typer|Commands and argument parsing|
|Terminal UI|Rich|Tables, formatting, live output|
|Async runtime|asyncio|Process and log streaming|
|Android communication|ADB|Device and process operations|
|Project management|uv|Dependencies and environments|
|Testing|pytest|Unit and integration testing|
|Mocking|pytest-mock|Isolated testing|
|CI/CD|GitHub Actions|Cross-platform validation|
|Packaging|PyPI|Python package distribution|
|Documentation|Markdown|Project documentation|

### Technology selection rationale

Python provides strong subprocess support, convenient asynchronous programming, mature testing tools, and a low barrier to installation.

Typer and Rich make it possible to create a professional CLI without building a terminal interface from scratch.

ADB is the established communication mechanism for Android debugging and provides the necessary device, package, process, and log operations.

---

## 7. System Architecture

DroidLens will follow a layered architecture with clear separation between the command interface, application services, domain models, and infrastructure.

### High-level architecture

```text
+--------------------------------+
|          CLI Layer             |
|                                |
| Typer Commands                 |
| Rich Renderer                  |
+---------------+----------------+
                |
+---------------v----------------+
|        Application Layer       |
|                                |
| DebugSessionService            |
| DeviceService                  |
| LogService                     |
| DiagnosticService              |
+---------------+----------------+
                |
+---------------v----------------+
|          Core Layer            |
|                                |
| Domain Models                  |
| Interfaces                     |
| Events                         |
| Exceptions                     |
+---------------+----------------+
                |
+---------------v----------------+
|       Infrastructure Layer     |
|                                |
| ADB Client                     |
| Process Runner                 |
| ADB Locator                    |
| Configuration                 |
+---------------+----------------+
                |
+---------------v----------------+
|          Android ADB           |
+--------------------------------+
```

### Architectural responsibilities

**CLI layer**

- Parse user commands.
    
- Validate command input.
    
- Invoke application services.
    
- Render output.
    
- Handle interactive terminal behavior.
    

**Application layer**

- Coordinate debugging operations.
    
- Manage session lifecycles.
    
- Coordinate device discovery and log streaming.
    
- Translate infrastructure results into application-level outcomes.
    

**Core layer**

- Define domain models.
    
- Define interfaces.
    
- Represent debugging events.
    
- Define application-level exceptions.
    
- Avoid dependencies on operating systems and ADB implementation details.
    

**Infrastructure layer**

- Execute ADB commands.
    
- Discover ADB installations.
    
- Manage operating-system processes.
    
- Parse command output.
    
- Handle external command failures.
    

---

## 8. Repository Structure

Proposed project structure:

```text
droidlens/
|
+-- src/
|   |
|   +-- droidlens/
|       |
|       +-- __init__.py
|       +-- main.py
|       |
|       +-- cli/
|       |   +-- commands/
|       |   |   +-- devices.py
|       |   |   +-- attach.py
|       |   |   +-- logs.py
|       |   |   +-- doctor.py
|       |   |
|       |   +-- renderer.py
|       |
|       +-- core/
|       |   |
|       |   +-- models/
|       |   |   +-- device.py
|       |   |   +-- app_process.py
|       |   |   +-- log_event.py
|       |   |
|       |   +-- interfaces/
|       |   |   +-- adb_client.py
|       |   |   +-- process_runner.py
|       |   |
|       |   +-- services/
|       |       +-- debug_session.py
|       |       +-- device_service.py
|       |       +-- log_service.py
|       |
|       +-- infrastructure/
|       |   |
|       |   +-- adb/
|       |   |   +-- client.py
|       |   |   +-- locator.py
|       |   |   +-- parser.py
|       |   |
|       |   +-- process/
|       |   |   +-- runner.py
|       |   |
|       |   +-- config/
|       |       +-- settings.py
|       |
|       +-- exceptions.py
|
+-- tests/
|   +-- unit/
|   +-- integration/
|   +-- fixtures/
|
+-- docs/
|
+-- .github/
|   +-- workflows/
|       +-- ci.yml
|
+-- pyproject.toml
+-- README.md
+-- LICENSE
+-- .gitignore
```

This is a proposed structure. It should evolve based on actual complexity rather than creating unnecessary abstractions prematurely.

---

## 9. MVP Features — Version 0.1

The first release focuses on four primary commands.

### 9.1 Device discovery

Command:

```bash
droidlens devices
```

Responsibilities:

- Discover connected Android devices.
    
- Identify device IDs.
    
- Show device connection states.
    
- Handle no-device scenarios.
    
- Handle multiple connected devices.
    

Example:

```text
DroidLens

Connected Devices

DEVICE             STATUS
Pixel 7            connected
Samsung A54        connected

2 devices found.
```

### 9.2 Application attachment

Command:

```bash
droidlens attach com.example.app
```

Responsibilities:

- Validate the package ID.
    
- Identify the target device.
    
- Verify package installation.
    
- Resolve the running process.
    
- Create a debugging session.
    
- Start process-specific log streaming.
    

Example:

```text
DroidLens
────────────────────────────────────

Device       Pixel 7
Package      com.example.app
PID          18342
Status       Attached

────────────────────────────────────

09:58:21 INFO   Flutter engine started
09:58:22 INFO   Application resumed
09:58:24 ERROR  API request failed

Listening for application events...
```

An important implementation detail: attaching to an application does not necessarily start the app. The first release should clearly distinguish between an installed package and a currently running process.

### 9.3 Log streaming

Command:

```bash
droidlens logs com.example.app
```

Responsibilities:

- Stream logs from the target process.
    
- Format timestamps and severity levels.
    
- Support basic filtering.
    
- Handle process termination.
    
- Stop cleanly when interrupted.
    

Planned filters:

```bash
droidlens logs com.example.app --level error
droidlens logs com.example.app --level warning
```

### 9.4 Environment diagnostics

Command:

```bash
droidlens doctor
```

Responsibilities:

- Check Python runtime compatibility.
    
- Locate ADB.
    
- Verify ADB execution.
    
- Check connected devices.
    
- Identify common environment configuration problems.
    
- Provide actionable error messages.
    

Example:

```text
DroidLens Doctor

[✓] Python runtime
[✓] ADB detected
[✓] ADB executable
[✓] Android device connected
[!] Multiple devices detected

Diagnostic completed.
```

---

## 10. Core Interfaces

The central design principle is to keep ADB details outside the application services.

### ProcessRunner

Responsible for external process execution.

```python
from typing import Protocol

class ProcessRunner(Protocol):

    async def run(
        self,
        command: list[str],
    ):
        ...

    async def stream(
        self,
        command: list[str],
    ):
        ...
```

The actual implementation must define structured return types, timeouts, exit codes, output handling, and process cleanup.

### AdbClient

Responsible for Android communication.

```python
class AdbClient:

    async def devices(self):
        ...

    async def packages(
        self,
        device_id: str,
    ):
        ...

    async def get_pid(
        self,
        device_id: str,
        package_id: str,
    ):
        ...

    async def logcat(
        self,
        device_id: str,
        pid: int,
    ):
        ...
```

### DebugSessionService

Responsible for orchestrating debugging sessions.

```python
class DebugSessionService:

    async def attach(
        self,
        package_id: str,
        device_id: str | None = None,
    ):
        ...

    async def detach(self):
        ...
```

These are conceptual interfaces. Production implementations should use typed results, explicit lifecycle states, and well-defined error handling.

---

## 11. Cross-Platform Compatibility Strategy

Cross-platform support must be verified at multiple levels.

### Process execution

Use argument arrays:

```python
await asyncio.create_subprocess_exec(
    adb_path,
    "devices",
    "-l",
    stdout=asyncio.subprocess.PIPE,
    stderr=asyncio.subprocess.PIPE,
)
```

Avoid shell-based command construction.

This prevents dependence on shell syntax and reduces command injection risks.

### ADB discovery

Search for ADB in the following order:

1. Explicitly configured executable path.
    
2. System PATH.
    
3. Android SDK environment variables.
    
4. Known platform-tools locations where practical.
    

The tool should report which executable it selected.

### Filesystem

Use pathlib for paths and platform-aware configuration directories.

### Terminal behavior

Use Rich for rendering and provide a plain or JSON output option for automation.

### Process lifecycle

Ensure child processes are closed when a session ends, including when users press Ctrl+C.

Account for differences between Windows and Unix-like process behavior.

### Compatibility principle

The same CLI commands and application behavior should be available across supported host operating systems, subject to platform-specific environment and Android tooling constraints.

---

## 12. Testing Strategy

Testing is a core quality requirement.

### Unit testing

Use mocked infrastructure to validate application behavior independently of Android devices.

Test cases:

- ADB executable missing.
    
- No devices connected.
    
- Multiple devices connected.
    
- Device unauthorized.
    
- Package not installed.
    
- Package installed but not running.
    
- Invalid or unavailable PID.
    
- ADB command failure.
    
- Malformed command output.
    
- Log stream termination.
    
- Unexpected process exit.
    

### Integration testing

Validate actual communication with ADB and Android devices or emulators.

Test cases:

- Device discovery.
    
- Package verification.
    
- PID resolution.
    
- Log streaming.
    
- Session interruption.
    
- Process termination handling.
    

### Cross-platform CI

GitHub Actions should run the relevant test suites on:

|Runner|Purpose|
|---|---|
|Windows|Windows compatibility|
|Ubuntu|Linux compatibility|
|macOS|macOS compatibility|

Every pull request should run the unit test suite across the supported operating systems.

Integration tests may initially run separately on a controlled Android emulator environment.

---

## 13. Packaging and Distribution

The initial distribution strategy is a Python package.

Planned installation:

```bash
uv tool install droidlens
```

The project should expose a console script:

```toml
[project.scripts]
droidlens = "droidlens.main:app"
```

The package should include:

- CLI entry point.
    
- Runtime dependencies.
    
- Version metadata.
    
- Installation instructions.
    
- Supported Python versions.
    
- Platform compatibility information.
    

Standalone executables may be considered after the Python package is stable.

Potential future distribution formats:

- Windows executable.
    
- macOS binary.
    
- Linux binary.
    
- Python package through PyPI.
    

The Android SDK and ADB remain external prerequisites unless a deliberate bundled distribution strategy is adopted.

---

## 14. Error Handling and Reliability

DroidLens should produce understandable, actionable errors.

Examples:

**ADB unavailable**

```text
Error: ADB was not found.

Install Android SDK Platform-Tools or
configure the ADB executable path.
```

**No device**

```text
Error: No Android devices detected.

Connect a device and enable USB debugging,
or start an Android emulator.
```

**Package not running**

```text
Error: Package is installed but no
running process was found.

Launch the application and try again.
```

**Multiple devices**

```text
Error: Multiple devices detected.

Specify a device using --device.
```

Reliability requirements:

- Timeouts for external commands.
    
- Structured exception types.
    
- Proper subprocess cleanup.
    
- No silent command failures.
    
- Clear distinction between recoverable and fatal errors.
    
- Useful diagnostics without exposing sensitive information.
    

---

## 15. Security and Privacy

DroidLens will operate on application logs and debugging information that may contain sensitive data.

Security considerations:

- Never log authentication tokens intentionally.
    
- Avoid automatically exporting sensitive request or application data.
    
- Do not execute user-provided shell strings.
    
- Validate package identifiers and command arguments.
    
- Avoid unnecessary elevated permissions.
    
- Clearly communicate when debugging requires USB debugging or special device access.
    
- Keep exported debugging sessions under user control.
    

The initial log viewer should not attempt to modify application behavior or bypass platform security controls.

---

## 16. Development Roadmap

### Phase 1 — Foundation

**Goal:** Establish the project and cross-platform execution layer.

Tasks:

- Initialize the Python project using uv.
    
- Configure Typer and Rich.
    
- Establish repository structure.
    
- Implement ProcessRunner.
    
- Implement ADB discovery.
    
- Add initial unit tests.
    
- Configure GitHub Actions for Windows, Linux, and macOS.
    

**Deliverable:** DroidLens can locate and execute ADB reliably across supported operating systems.

### Phase 2 — Device and Package Discovery

**Goal:** Make Android device and application discovery reliable.

Tasks:

- Implement device listing.
    
- Parse device states.
    
- Support explicit device selection.
    
- Verify package installation.
    
- Resolve application processes.
    
- Handle common failure scenarios.
    

**Deliverable:** Working `devices` command and package/process discovery.

### Phase 3 — Debug Sessions and Logs

**Goal:** Deliver the first useful debugging experience.

Tasks:

- Implement DebugSessionService.
    
- Implement process-specific log streaming.
    
- Add readable terminal output.
    
- Add basic log-level filtering.
    
- Implement graceful interruption and cleanup.
    

**Deliverable:** Working `attach` and `logs` commands.

### Phase 4 — Diagnostics and Stabilization

**Goal:** Improve usability and reliability.

Tasks:

- Implement `doctor`.
    
- Improve error reporting.
    
- Expand unit tests.
    
- Validate behavior on all supported operating systems.
    
- Document setup and troubleshooting.
    

**Deliverable:** A usable v0.1 release candidate.

### Phase 5 — Future Capabilities

Potential future versions:

|Version|Capability|
|---|---|
|v0.2|Crash and exception detection|
|v0.3|Flutter and Dart diagnostics|
|v0.4|Network and API inspection|
|v0.5|Performance monitoring|
|v0.6|Session recording and export|
|v1.0|Unified Android debugging platform|

These milestones are tentative and depend on validating the MVP and prioritizing actual developer needs.

---

## 17. Definition of Done for v0.1

The first release is complete when:

-  DroidLens installs using the documented Python package workflow.
    
-  The CLI runs on Windows, Linux, and macOS.
    
-  ADB is discovered reliably or a clear error is reported.
    
-  Connected devices are listed correctly.
    
-  Multiple-device selection works.
    
-  Installed packages can be verified.
    
-  Running processes can be identified.
    
-  Process-specific logs stream correctly.
    
-  Ctrl+C stops the session cleanly.
    
-  Common failure cases produce actionable messages.
    
-  Unit tests pass on all three operating systems.
    
-  Integration tests pass in the supported Android environment.
    
-  README and installation documentation are complete.
    

---

## 18. Long-Term Vision

DroidLens should grow through modular debugging capabilities instead of accumulating unrelated CLI commands.

Potential future architecture:

```text
                  DroidLens
                      |
             Unified Debug Session
                      |
       +--------------+--------------+
       |              |              |
       v              v              v
     Logs          Network       Diagnostics
       |              |              |
       v              v              v
    Crashes       API Tracing    Performance
       |              |              |
       +--------------+--------------+
                      |
                Event Pipeline
                      |
             +--------+--------+
             |        |        |
             v        v        v
            CLI     Export   Integrations
```

A common event pipeline could eventually correlate application logs, network failures, process lifecycle events, and diagnostics.

For example:

```text
09:42:15

POST /api/payment
Status: 500
Duration: 823ms

Application error:
PaymentRepository.create()

Session:
com.example.app
PID: 18342
```

This is a future capability, not something the first release can guarantee. Reliable correlation may require additional instrumentation or application-specific information.

---

## 19. Key Engineering Decisions

|Decision|Rationale|
|---|---|
|Python as the core language|Strong tooling ecosystem and existing development expertise|
|Android-only initial target|Keeps the first release focused|
|Cross-platform host support from day one|Prevents OS-specific assumptions from spreading|
|ADB as the communication mechanism|Uses established Android debugging infrastructure|
|Layered architecture|Separates CLI, business logic, and infrastructure|
|Async process handling|Supports continuous streams and session management|
|Rich for presentation|Professional terminal output with less custom code|
|Automated cross-platform CI|Makes compatibility verifiable|
|Incremental roadmap|Controls scope and reduces premature complexity|

---

## 20. Conclusion

DroidLens is designed to make Android debugging more accessible, consistent, and efficient from the command line.

The immediate objective is deliberately narrow:

**Given an Android package ID, reliably identify its running process and stream its logs across Windows, Linux, and macOS.**

Achieving this with clean interfaces, dependable process management, robust error handling, and automated cross-platform testing establishes the foundation for future debugging and observability features.

The success of DroidLens v0.1 should be measured by reliability and usability, not by the number of features it contains.

**DroidLens: See what your Android application is doing.**