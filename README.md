# Batchsmith

Edit, check and run Windows batch files (.bat and .cmd) in JetBrains IDEs.

This page holds documentation and the issue list. The plugin itself is installed from JetBrains Marketplace.

## What it checks

| Mistake | Example | Why it matters |
|---|---|---|
| Variable read too early in a block | `if 1==1 ( set V=new & echo %V% )` | cmd.exe replaces `%V%` before the block runs, so the old value is used |
| `%ERRORLEVEL%` in a block | `( pip install x`, then `if %ERRORLEVEL% neq 0 exit 1 )` | A failure is not noticed |
| Space before `=` | `set NAME = value` | Creates a variable named `NAME ` with a space |
| `else` on its own line | `)` then `else (` | cmd.exe runs `else` as a command |
| `)` in text inside a block | `echo done (ok)` | Ends the block early |
| `::` comment before `)` | | Syntax error |
| Single `%` in a loop | `for %i in (1 2) do echo %i` | Works only when typed at the prompt |
| Indented command after `^` | `ver && ^` then `  dir` | The space becomes part of the command name |
| Missing label | `goto nowhere` | The script stops |
| LF line endings | | cmd.exe can miss a label, depending on its position |
| Byte order mark | | The first line fails |

## Report a problem

Please include your IDE version, the smallest script that shows the problem, and what you expected.

## Privacy

Batchsmith works offline. It collects no personal data, sends no statistics and makes no network connections.

## License

See [EULA.md](EULA.md).
