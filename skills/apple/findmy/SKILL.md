# FindMy — Locate Apple Devices via CLI

## Concept
Find and track Apple devices using Apple's Find My network.

## Setup
```bash
pip install findmy-cli
```

## Usage

### List devices
```bash
findmy list
# Output:
# iPhone (iPhone 15 Pro) — Online — Battery: 87%
# MacBook Pro — Online — Battery: 62%
# AirPods Pro — Offline
```

### Get location
```bash
findmy location "iPhone"
# Output:
# Latitude: 37.7749
# Longitude: -122.4194
# Address: 123 Main St, San Francisco, CA
# Last updated: 5 minutes ago
```

### Get status
```bash
findmy status "MacBook Pro"
# Battery level, charging status, network status
```

### Play sound
```bash
findmy sound "iPhone"  # Will ring at full volume
```

### Lost mode
```bash
findmy lost "iPhone" --message "Lost iPhone, please call"
```

## Requirements
- Apple ID must have Find My enabled
- Device must be signed into iCloud
- Device must be online (or recently online for last known location)

## Privacy
- Requires authentication to Apple ID
- Location data is end-to-end encrypted
- Only shows devices associated with your Apple ID
