# emacs-dsh-host-bridge

A DSH Host bundle that lets the [emacs-dsh](https://github.com/wowhxj/emacs-dsh) Emacs package discover and authenticate to the already running local DSH Web Host. The Host bundle and Emacs package are installed and updated independently.

## Install

1. On macOS, ensure the DSH home directory is private: `chmod 700 "${DSH_HOME:-$HOME/.dsh}"`. The bridge writes a bearer launch URL there with `0600` file permissions. On Windows, the URL is protected with DPAPI for the current user.
2. In **DSH Desktop → Plugins → Install**, enter `github:wowhxj/emacs-dsh-host-bridge` and enable the bundle. Restart the App and Host if the plugin manager requests it. Desktop owns its profile; install through its Plugins page.
3. For an independent `dsh web` Host, run `dsh plugin --profile web add github:wowhxj/emacs-dsh-host-bridge`, then restart that Host.
4. Check that `~/.dsh/emacs-dsh-bridge.json` exists on macOS, or `%USERPROFILE%\.dsh\emacs-dsh-bridge.json` on Windows. Never print or share this file: it contains an authentication credential.

The Emacs client reads this file automatically. It does not require an extra username or password prompt. The Host must remain running while Emacs connects. A custom `DSH_HOME` must point to the same directory for the Host and Emacs.

## Development

Run `node --test tests.mjs`. The POSIX permission checks and Windows DPAPI behavior should be tested on their respective platforms.
