# 0. About

`inc` is a command-line notebook for on-call engineers. It helps them collect evidence during an incident and turn it into a report with a timeline.

## 0.1 Main traits

- The tool is local-first and text-based. It runs on the engineer’s machine without a server or hosted service.
- The CLI keeps common commands short and predictable with positional arguments and sensible defaults. Use a positional argument when the subcommand makes the input clear.

# 1. Feature set

## 1.1 Managing storages

- Storages default to `~/.inc/storage`. The configuration can override this path.
- Create, view, edit, delete, and list storages.
- Select an active storage and switch between storages.
- Back up, transfer, and merge storages. For example, copy a storage from a remote host.

## 1.2 Capture modes

- Capture files, directories, and piped input.
- Capture clipboard content, including screenshots.
- Record terminal sessions.
- Open a new notebook document in an editor from within a storage.
- Add text and snippets from the CLI.
- Save captured evidence to the active storage.

## 1.3 Organizing and finding evidence

- Add tags or notes to each artifact.
- Show artifacts, tags, and notes in report mode.
- List all artifacts inside a storage.
- Search artifacts in several modes.
- Provide a terminal user interface (TUI) for working with evidence.
- Record a timestamp and source for each artifact.

## 1.4 Reports and timelines

The first version generates Markdown reports. Later versions can support other formats.

- **Header** shows the incident ID, title, status, date, and time zone.
- **Summary** describes the impact, cause, and resolution.
- **Timeline** lists events in chronological order. Each entry shows the event time, what happened, and any supporting artifact IDs.
- **Evidence** lists artifacts in capture order. Each entry shows the artifact ID, capture time, filename, source, tags, and notes.
- **Follow-up** lists actions to take after the incident.

See the [example Markdown report](2_1_report_example.md).

## 1.5 AI and agents

- Let agents capture and manage evidence.
- Provide an MCP interface.
- Let agents read a storage to help investigate an incident.

# 2. Interface

# 3. Architecture

## 3.1 Storage structure

- Any existing directory can be opened as a storage.
- Captured files go directly in the storage root.
- The tool creates only one subdirectory, `.inc`, and keeps storage metadata in `.inc/metadata.json`.
- Artifact paths in the metadata are relative to the storage root.

# 4. Implementation

- Rust

# 5. Testing

Test environment.
