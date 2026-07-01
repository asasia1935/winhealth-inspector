# AGENTS.md

## Project

WinHealth Inspector is an open-source Windows diagnostics and maintenance tool built with C# and WPF.

## Current Stage

The repository is currently in the product definition and architecture design stage.

Do not add implementation code until the user explicitly starts the implementation phase.

## Product Principles

- Explain every diagnosis with evidence.
- Distinguish system problems from diagnostic failures.
- Do not exaggerate performance or security risks.
- Do not modify the system without explicit user confirmation.
- Prefer read-only diagnostics before maintenance actions.
- Use the least privilege required.
- Do not send system or user information to external servers.
- Do not implement registry cleaning or aggressive system tuning.
- Distinguish storage cleanup from actual performance improvement.

## Architecture Principles

- Keep WPF UI separate from Windows-specific infrastructure.
- Separate data collection from diagnostic evaluation.
- Separate diagnostic checks from maintenance actions.
- Keep diagnostic rules testable without calling real Windows APIs.
- Keep `WinHealth.Core` independent from WPF and Windows-specific APIs.
- Do not expose Windows API objects directly from the infrastructure layer.
- Convert platform-specific values into project-owned snapshot models before evaluation.
- Follow the documented project reference direction.
- Do not introduce circular project references.
- One failed diagnostic must not stop the entire diagnostic run.
- Avoid unnecessary abstractions and premature plugin systems.
- Treat `Unknown` and `NotApplicable` as first-class states.

## Development Rules

- Work on one diagnostic or maintenance action at a time.
- Before modifying code, inspect the current repository and describe the plan.
- List expected files to create or modify.
- Do not make unrelated changes.
- Do not add features outside the current phase.
- Do not add or replace external packages without explaining the need and impact first.
- Run relevant builds and tests after changes.
- Report failures honestly.
- Do not silently swallow exceptions.
- Do not treat an unknown result as healthy.
- Handle expected platform limitations inside each diagnostic.
- Let the diagnostic runner handle unhandled exceptions, timeouts, and common execution failures.
- Preserve cancellation and timeout behavior for long-running operations.
- Update documentation when a design decision or scope changes.

## WPF Rules

- Use MVVM for user interactions.
- Use commands rather than button click handlers where practical.
- Keep code-behind limited to view-specific behavior.
- Do not access Windows APIs directly from ViewModels.
- Use bindings and data templates for diagnostic result presentation.
- Do not use color as the only way to communicate status.
- Keep UI state explicit for idle, running, completed, failed, cancelled, and partially completed flows.

## Safety Rules

- Never delete files outside explicitly allowed locations.
- Show a preview before destructive actions.
- Require separate confirmation for irreversible actions.
- Do not delete recent or currently used temporary files.
- Do not follow symbolic links or reparse points unless the behavior is explicitly reviewed and tested.
- Treat cancellation of destructive work as best-effort cancellation.
- Do not claim that completed changes were rolled back unless rollback actually occurred.
- Report completed, skipped, failed, and unprocessed items separately after cancellation.
- Only execute explicitly allowed external commands and arguments.
- Do not concatenate user input into shell commands.
- Prefer launching executable files with structured arguments instead of using a command shell.
- Do not implement registry cleanup.
- Do not disable Windows services automatically.
- Do not change DNS servers, TCP settings, page files, or power plans automatically.
- Do not delete browser cookies, login data, user documents, downloads, or desktop files.

## Documentation Rules

When a significant design decision changes:

- update the relevant documentation;
- explain why the decision changed;
- keep the MVP scope and exclusions synchronized;
- do not describe unimplemented features as complete.
