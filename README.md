# Antigravity YOLO-Mode Config

A configuration template for Google's Antigravity IDE/Agent to bypass all tool execution permission prompts, similar to Claude Code's `--dangerously-skip-permissions` flag.

## ⚠️ Warning

> [!WARNING]
> **Use at your own risk!**
> This configuration disables all safety confirmation prompts (YOLO mode). When active, the agent can execute commands, write files, perform network requests, and execute arbitrary code without prompting you for permission.
> It is strongly recommended to run the agent in a sandboxed/containerized environment when this configuration is active.

## Installation

1. Copy the contents of `config.json` from this repository.
2. Locate your Antigravity global configuration file:
   - **Windows**: `C:\Users\<your-username>\.gemini\config\config.json`
   - **macOS/Linux**: `~/.gemini/config/config.json` (or equivalent)
3. Open the file in your editor and merge/replace the `"globalPermissionGrants"` section under `"userSettings"`. Make sure to replace `<your-username>` with your actual operating system username.
4. Save the file. Ensure the file is encoded in **UTF-8 without BOM** (Byte Order Mark), as the Antigravity parser throws a syntax error if a BOM is present.
5. Restart your Antigravity session.

## Configuration Details

This configuration adds the following catch-all allow rules at the top of the `"allow"` permission chain:

*   **`read_file(C:\)` & `write_file(C:\)`**: Automatically allows file reads and writes on the `C:` drive.
*   **`read_file(D:\)` & `write_file(D:\)`**: Automatically allows file reads and writes on the `D:` drive.
*   **`command(*)` & `unsandboxed(*)`**: Automatically allows executing all commands inside and outside the sandbox.
*   **`read_url(*)` & `execute_url(*)`**: Automatically allows reading URLs and executing network requests.
*   **`mcp(*)`**: Automatically allows all Model Context Protocol tool execution.
*   **`custom(*)`**: Automatically allows any custom-defined action prompts.

These are placed at the beginning of the `allow` array to intercept all tool calls before the default permission prompts are triggered.