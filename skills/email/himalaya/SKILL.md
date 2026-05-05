# Email — Himalaya CLI for Terminal Email

## Concept
Himalaya is a CLI email client for IMAP/SMTP. It's a single binary — no config files, just environment variables.

## Setup

### 1. Install
```bash
cargo install himalaya
# or
brew install himalaya
```

### 2. Configure credentials
```bash
export HIMALAYA_USERNAME="your@email.com"
export HIMALAYA_PASSWORD="your-password"
export HIMALAYA_SMTP_HOST="smtp.gmail.com"
export HIMALAYA_SMTP_PORT="587"
export HIMALAYA_IMAP_HOST="imap.gmail.com"
export HIMALAYA_IMAP_PORT="993"
```

### 3. Add to `~/.bashrc` or `~/.zshrc`
```bash
source ~/.env.himalaya  # your credentials file
```

## Common Commands

### List emails
```bash
himalaya list                      # inbox
himalaya list --folder sent       # sent
himalaya list --folder INBOX/work # specific folder
```

### Read email
```bash
himalaya read <email-id>
```

### Send email
```bash
himalaya send --from "your@email.com" --to "recipient@email.com" --subject "Subject" --body "Body text"
```

### Attachments
```bash
himalaya attach /path/to/file.txt
```

### Search
```bash
himalaya search "from:someone@gmail.com"
himalaya search "subject:urgent"
```

### Folders
```bash
himalaya folder list
himalaya folder create "INBOX/work"
```

## Gmail-specific
For Gmail with 2FA, use an App Password:
1. Google Account → Security → 2-Step Verification → App Passwords
2. Generate a new app password for "Mail"
3. Use that 16-char password instead of your regular password

## Aliases for Quick Use
```bash
alias him='himalaya'
alias himl='himalaya list'
alias himr='himalaya read'
alias hims='himalaya send'
```
