<div align="center">

<img src="https://res.cloudinary.com/ddyc1es5v/image/upload/v1768054074/gh-repos/applock-macos/apple.png" alt="logo" width="80" height="80"/>
<img src="https://res.cloudinary.com/ddyc1es5v/image/upload/v1768054076/gh-repos/applock-macos/touchid.png" alt="logo" width="80" height="80"/>
<img src="https://res.cloudinary.com/ddyc1es5v/image/upload/v1768054074/gh-repos/applock-macos/terminal.png" alt="logo" width="80" height="80"/>

<h1 align="center">shelllock-macos</h1>
<p align="center"><i><b>Protect any shell command behind Touch ID 🔐</b></i></p>

[![Github][github]][github-url]
[![Homebrew][homebrew]][homebrew-url]

</div>

<br/>

## Table of Contents

<ol>
    <a href="#about">📝 About</a><br/>
    <a href="#install">💻 Install</a><br/>
    <a href="#usage">🚀 Usage</a><br/>
    <a href="#roadmap">🗺️ Roadmap</a><br/>
    <a href="#tools-used">🔧 Tools used</a><br/>
    <a href="#contact">👤 Contact</a>
</ol>

<br/>

## 📝About

Gate any shell command or script behind biometric auth. **AI agents cannot bypass this** - they can't physically touch your fingerprint sensor.

```
you type: shelllock ./deploy.sh
           ↓
Touch ID prompt appears
           ↓
✓ authenticated → script runs
✗ failed → nothing happens
```

**Use cases:**
- Protect deploy scripts from eager AI agents (Cursor, Copilot)
- Gate destructive commands (`rm -rf`, `git push --force`)
- Secure sensitive operations (DB migrations, prod access)
- Any command you want locked

<br/>

## 💻Install

```bash
brew tap vdutts7/tap
brew install shelllock
```

### From source (optional)

```bash
git clone https://github.com/vdutts7/shelllock-macos.git
cd shelllock-macos
make install
```

> Builds universal binary (Intel + Apple Silicon) automatically.

<details>
<summary>Build from source</summary>

```bash
# Requires Xcode
make build

# Or manually
swiftc -O -o shelllock Sources/shelllock.swift
```

**Troubleshooting SDK mismatch:**

If you get "failed to build module 'CoreFoundation'" error:

```bash
# Option 1: Reinstall Command Line Tools
sudo rm -rf /Library/Developer/CommandLineTools
xcode-select --install

# Option 2: Point to Xcode SDK
sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
```
</details>

<br/>

## 🚀Usage

```bash
# Basic - run script behind Touch ID
shelllock ./deploy.sh

# Custom prompt message
shelllock -m "Deploy to production?" ./deploy.sh

# Inline command
shelllock -c "npm run build && npm test"

# Any command with args
shelllock make install PREFIX=/usr/local
```

### Self-protecting scripts

Add to the top of any script to require Touch ID:

```bash
#!/bin/bash
if [[ "${SHELLLOCK_VERIFIED:-}" != "1" ]]; then
    exec env SHELLLOCK_VERIFIED=1 shelllock -m "Run this script?" "$0" "$@"
fi
# ... rest of script
```

<br/>

## 🗺️Roadmap

- [x] Touch ID biometric authentication
- [x] Custom prompt messages
- [x] Inline command mode (`-c`)
- [x] Homebrew formula
- [ ] Config file for protected commands list
- [ ] Allowlist by username
- [ ] Audit logging

<br/>

## 🔧Tools Used

[![Swift][swift]][swift-url]
[![macOS][macos]][macos-url]

<br/>

## 👤Contact

[![Email][email]][email-url]
[![Twitter][twitter]][twitter-url]

<!-- BADGES -->
[github]: https://img.shields.io/badge/💻_shelllock--macos-000000?style=for-the-badge
[github-url]: https://github.com/vdutts7/shelllock-macos
[homebrew]: https://img.shields.io/badge/Homebrew-vdutts7/tap-FBB040?style=for-the-badge&logo=homebrew&logoColor=white
[homebrew-url]: https://github.com/vdutts7/homebrew-tap
[swift]: https://img.shields.io/badge/Swift-FA7343?style=for-the-badge&logo=swift&logoColor=white
[swift-url]: https://swift.org/
[macos]: https://img.shields.io/badge/macOS_LocalAuthentication-000000?style=for-the-badge&logo=apple&logoColor=white
[macos-url]: https://developer.apple.com/documentation/localauthentication
[email]: https://img.shields.io/badge/Email-000000?style=for-the-badge&logo=Gmail&logoColor=white
[email-url]: mailto:me@vd7.io
[twitter]: https://img.shields.io/badge/Twitter-000000?style=for-the-badge&logo=Twitter&logoColor=white
[twitter-url]: https://x.com/vdutts7
