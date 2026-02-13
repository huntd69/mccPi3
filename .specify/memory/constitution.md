<!--
SYNC IMPACT REPORT
==================
Version Change: TEMPLATE → 1.0.0
Constitution Type: Initial ratification (bare minimum for embedded deployment)

Modified Principles:
- Added: I. Hardware Compatibility (Pi Zero 2W specific constraints)
- Added: II. Idempotent Deployment (safe re-run capability)
- Added: III. Simple Error Handling (clear failures for remote debugging)
- Removed: Principles 4-5 (not applicable for single-script deployment)

Added Sections:
- Deployment Requirements (GitHub-based, offline-capable post-install)
- Testing Standards (hardware-specific manual testing)

Templates Requiring Updates:
- ✅ plan-template.md: Compatible (single project structure applies)
- ✅ spec-template.md: Compatible (user stories work for feature additions)
- ✅ tasks-template.md: Compatible (Phase structure applies to script modules)

Follow-up TODOs: None - all placeholders resolved

Commit Message: docs: ratify constitution v1.0.0 (Pi Zero 2W packet radio configurator)
-->

# mccPi3 Ham Radio Configurator Constitution

## Core Principles

### I. Hardware Compatibility

All code MUST run on Raspberry Pi Zero 2W (ARM v7 32-bit architecture). Resource constraints (512MB RAM, single-core CPU) must be respected in all operations. Driver and kernel module compatibility MUST be verified against Raspberry Pi OS Lite. Hardware detection failures MUST halt execution with clear error messages.

**Rationale**: The Zero 2W has limited resources and specific hardware capabilities. Code that works on desktop or Pi 4 may fail or perform poorly on Zero 2W. Early validation prevents deployment failures.

### II. Idempotent Deployment

Configuration script MUST be safely re-runnable without corrupting or duplicating existing setup. All operations MUST check current system state before making modifications. Existing working configurations MUST be preserved unless explicitly flagged for replacement. Partial deployments MUST be resumable.

**Rationale**: Remote ham radio deployments require reliable updates and recovery. Operators need to re-run setup after system updates or partial failures without manual cleanup.

### III. Simple Error Handling

All error conditions MUST produce clear, actionable messages indicating what failed and why. Script MUST exit with non-zero status codes on any failure. Critical failures (driver loading, hardware interface detection, kernel module issues) MUST halt execution immediately. Non-critical warnings may be logged but must not stop deployment.

**Rationale**: Remote debugging over cell phone interfaces requires clear diagnostic output. Operators may not be Linux experts and need actionable guidance.

## Deployment Requirements

Script initiated via GitHub repository clone or direct download mechanism. Initial internet connectivity REQUIRED for downloading dependencies and drivers. Post-deployment operation MUST work completely offline. Deployment consists of single Python script or minimal file structure (max 5 files including configs). Python standard library preferred; external dependencies justified and minimized.

## Testing Standards

Manual testing REQUIRED on actual Raspberry Pi Zero 2W hardware before any release. Minimum test scenarios: (1) fresh OS install deployment, (2) re-run on already-configured system, (3) recovery from interrupted deployment. Test results and hardware validation MUST be documented in release notes. Virtual testing (QEMU) acceptable for development but not sufficient for release.

## Governance

Constitution tracked in git repository history. Breaking changes to core principles require MAJOR version bump. Script changes affecting radio operation or hardware compatibility require re-validation. All deployments MUST comply with FCC Part 97 regulations for amateur packet radio operation (1200 baud, identification requirements, frequency usage).

**Version**: 1.0.0 | **Ratified**: 2026-02-13 | **Last Amended**: 2026-02-13
