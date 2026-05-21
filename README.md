# PSADT v4 Snippets for Visual Studio Code

A small, opinionated set of PowerShell snippets for **[PSAppDeployToolkit v4](https://psappdeploytoolkit.com/)** (PSADT) — the de-facto framework for packaging Windows applications for Intune, ConfigMgr / SCCM, and other enterprise deployment tools.

## Why use these snippets

Packaging a Win32 app with PSADT means writing the same handful of patterns over and over: install/uninstall calls, file & folder cleanup, registry edits, shortcut creation, per-user profile actions. The cmdlet names are long and the parameter orders are easy to misremember — which leads to either copy-pasting from old packages (and inheriting their bugs) or burning time looking up syntax in the docs.

These snippets give you:

- **Correct PSADT v4 cmdlet calls out of the box.** Every snippet uses the current `*-ADT*` cmdlets, not the v3 `Execute-*` aliases.
- **Tab-stop placeholders** for the values that actually change between packages (paths, names, value data), so you fill in only what's variable.
- **Proper escaping of PowerShell variables inside snippet bodies.** PSADT exposes session variables like `$envCommonStartMenuPrograms`, `$envWinDir`, and `$($adtSession.DirSupportFiles)` — these are escaped so VS Code treats them as literal PowerShell variables instead of snippet tabstops.
- **A consistent `psadt-<verb>-<noun>` prefix scheme** that mirrors PowerShell's own verb-noun convention. Typing `psadt-` filters the IntelliSense list to just these snippets; typing `psadt-remove-` narrows to removal operations; and so on.

If you package more than two or three apps a year with PSADT, these will save you time and reduce silly mistakes.

## Installation

### Option 1 — User snippets (recommended)

User snippets are stored in your VS Code profile and work in every workspace.

1. In VS Code, open the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`).
2. Run **`Snippets: Configure Snippets`**.
3. Pick **`powershell.json`** (creating it if prompted).
4. Replace its contents with the contents of [`powershell.json`](./powershell.json) from this repo, or merge the entries into your existing file.

The file location on disk:

| OS | Path |
|---|---|
| Windows | `%APPDATA%\Code\User\snippets\powershell.json` |
| macOS | `~/Library/Application Support/Code/User/snippets/powershell.json` |
| Linux | `~/.config/Code/User/snippets/powershell.json` |


## Usage

Open any `.ps1` file (typically `Invoke-AppDeployToolkit.ps1` in a PSADT v4 package), start typing a prefix (e.g. `psadt-install-exe`), and press `Tab` or `Enter` to expand. Use `Tab` to walk through the placeholders.

## Available snippets

| Prefix | What it does |
|---|---|
| `psadt-install-exe` | Install EXE application via `Start-ADTProcess` |
| `psadt-install-msi` | Install MSI application via `Start-ADTMsiProcess` |
| `psadt-uninstall-app` | Uninstall application by display name (exact match) |
| `psadt-new-folder` | Create a folder with `New-ADTFolder` |
| `psadt-new-shortcut` | Create a Start Menu shortcut with `New-ADTShortcut` |
| `psadt-remove-file` | Remove a file with `Remove-ADTFile` |
| `psadt-remove-folder` | Remove a folder with `Remove-ADTFolder` |
| `psadt-remove-startmenu` | Remove a file from the All Users Start Menu |
| `psadt-remove-desktop` | Remove a file from the Public Desktop |
| `psadt-remove-envvar` | Remove a machine-level environment variable |
| `psadt-copy-file` | Copy a file with `Copy-ADTFile` |
| `psadt-copy-folder` | Copy a folder recursively from `$adtSession.DirFiles` |
| `psadt-get-userprofiles` | Collect all user profile paths into `$ProfilePaths` |
| `psadt-foreach-userprofile` | Query all user profiles and `foreach` over them |
| `psadt-copy-userprofiles` | Copy a file to every user's `AppData\Roaming` |
| `psadt-remove-file-userprofiles` | Remove a file from every user's `AppData\Roaming` |
| `psadt-remove-folder-userprofiles` | Recursively remove a folder from every user's `AppData\Local` |
| `psadt-set-hkcu-allusers` | Set an `HKCU` registry value for all current and future users |
| `psadt-remove-regkey` | Delete an entire registry key (and all values under it) |
| `psadt-remove-regvalue` | Delete a single named value from a registry key |
| `psadt-update-desktop` | Refresh Explorer shell after env or registry changes |
| `psadt-log` | Write a custom log entry with a severity dropdown (1=Info, 2=Warning, 3=Error) |
| `psadt-try-catch` | `try`/`catch` block that logs the error via `Write-ADTLogEntry` |
| `psadt-if-testpath` | `if (Test-Path …) { … }` block |


## License

[MIT](./LICENSE) — use freely, attribution appreciated but not required.
