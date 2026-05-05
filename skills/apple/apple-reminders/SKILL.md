# Apple Reminders — Native Reminders via CLI

## Concept
Use Apple Reminders from the terminal. Great for scripting and integration with other tools.

## Setup
```bash
pip install apple-reminders-cli
```

## Usage

### List reminders
```bash
apple-reminders list                          # All reminders
apple-reminders list --list "Work"           # Specific list
apple-reminders list --due today             # Due today
apple-reminders list --due overdue           # Overdue
apple-reminders list --completed              # Completed
```

### Add reminder
```bash
apple-reminders add "Buy groceries" --list "Personal"
apple-reminders add "Call dentist" --due "2024-12-25" --list "Health"
apple-reminders add "Meeting" --due "tomorrow 3pm" --notes "Bring notes"
```

### Complete/delete
```bash
apple-reminders complete "Buy groceries"
apple-reminders delete "Buy groceries"
```

### Update reminder
```bash
apple-reminders update "Buy groceries" --notes "Add more items"
apple-reminders update "Buy groceries" --due "tomorrow"
```

## Siri Shortcuts Alternative
You can also use Siri Shortcuts:
```bash
shortcuts run "Add Reminder"
```

Create a shortcut in the Shortcuts app that adds a reminder.
