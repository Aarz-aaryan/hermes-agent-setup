# Apple — Apple Notes, Reminders, FindMy, iMessage

## Concept
Use native Apple apps via CLI tools. These are for personal automation on macOS/iOS.

## Apple Notes

### Setup
```bash
pip install apple-notes-cli
# or
brew install apple-notes-cli
```

### Usage
```bash
apple-notes list                    # List all notes
apple-notes list --folder "Work"    # List notes in folder
apple-notes read "Note Title"      # Read a note
apple-notes create --title "Title" --body "Content"  # Create note
apple-notes delete "Note Title"    # Delete note
apple-notes search "keyword"        # Search notes
```

## Apple Reminders

### Setup
```bash
pip install apple-reminders-cli
```

### Usage
```bash
apple-reminders list                        # List all reminders
apple-reminders list --list "Shopping"     # List reminders in specific list
apple-reminders add "Buy milk" --list "Shopping"  # Add reminder
apple-reminders complete "Buy milk"         # Mark as complete
apple-reminders delete "Buy milk"           # Delete reminder
apple-reminders list --due today           # Reminders due today
```

## FindMy (Find My Device)

### Setup
```bash
pip install findmy-cli
```

### Usage
```bash
findmy list                        # List all devices
findmy location "iPhone"          # Get device location
findmy status "AirPods"          # Battery and status
```

## iMessage

### Setup
```bash
pip install imessage-cli
```

### Usage
```bash
imessage send "+1234567890" "Hello!"     # Send message
imessage list conversations              # List recent conversations
imessage read "John" --limit 10         # Read recent messages
imessage attachments "John"              # List attachments in conversation
imessage search "keyword"                # Search messages
```

## Limitations
- All these tools require macOS
- Some require Shortcuts app enabled
- iMessage requires Continuity/Messages iCloud setup
- FindMy requires Apple ID and Find My enabled on device

## Note on Privacy
These tools access your personal data. Make sure you trust any scripts that use them.
