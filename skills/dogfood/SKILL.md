# Dogfood — Exploratory QA of Web Apps

## Concept
Use Hermes browser agent to explore and find bugs in web apps. Think "I want to break this" — probe for edge cases, error states, and unexpected behavior.

## When to Use
- Before shipping a feature
- Testing a competitor's product
- Finding bugs in your own app

## Bug Severity
- **P0**: Data loss, security vulnerability, crashes
- **P1**: Major feature broken, workaround exists
- **P2**: Minor UI glitch, cosmetic issue, poor UX

## Focus Areas

### 1. Input Validation
- Submit empty forms
- Try very long inputs
- Try special characters: `' " < > & ; | $`
- Try SQL injection: `' OR 1=1 --`
- Try XSS: `<script>alert('xss')</script>`
- Try negative numbers, zero, non-numeric in numeric fields
- Try past dates for "future only" fields

### 2. Error Handling
- Disconnect internet mid-action
- Submit while server is down
- Try to access deleted items
- Try expired sessions
- Force 404 pages

### 3. State Bugs
- Double-click submit buttons
- Refresh mid-process
- Use browser back button
- Open same page in two tabs
- Scroll while loading

### 4. Authorization
- Try accessing other users' data
- Try accessing admin as regular user
- Try modifying readonly fields

### 5. Accessibility
- Navigate with keyboard only
- Try with JavaScript disabled
- Check color contrast
