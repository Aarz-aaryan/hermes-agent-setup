# iMessage — Send/Read iMessages from Terminal

## Concept
Send and receive iMessages via the terminal. Great for notifications and automation scripts.

## Setup
```bash
pip install imessage-cli
```

## Usage

### Send message
```bash
imessage send "+1234567890" "Hello!"
imessage send "John" "Hello!"  # By contact name
```

### List conversations
```bash
imessage list conversations
# Shows recent conversations with last message
```

### Read messages
```bash
imessage read "John" --limit 20   # Last 20 messages
imessage read "+1234567890" --limit 10
```

### Search
```bash
imessage search "hello"
imessage search "hello" --limit 20
```

### Attachments
```bash
imessage attachments "John"         # List attachments
imessage attachments "John" --save ~/Downloads  # Save attachments
```

### Status
```bash
imessage status  # Show unread count, etc.
```

## Requirements
- macOS with Messages app signed into iCloud
- For sending: depends on Settings → Messages → iMessage forwarding
- Contact names must exist in Contacts app

## Limitations
- Cannot receive real-time push notifications without a daemon
- Some setups require enabling "Forwarding" in Messages settings
- Group messages may have limited support

## Privacy Note
This tool reads your actual Messages database. Be careful with who has access to this tool.
