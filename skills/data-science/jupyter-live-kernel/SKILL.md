# Data Science — Interactive Python via Live Jupyter Kernel

## Concept
Use a persistent Jupyter kernel (`hamelcho`) for iterative Python work. Kernel survives across calls — variables, imports, and state persist.

## Available Tools

### jupyter_live_kernel
```
skill_view(name='jupyter-live-kernel')
```

**In the skill file:**
- `connect_info`: how to connect to the kernel
- `kernel_name`: name of the kernel to use
- `usage_examples`: common patterns

### execute_code tool
Standard Python REPL with access to:
- `read_file`, `write_file`, `terminal` via `hermes_tools`
- All standard library: json, re, math, csv, datetime, collections
- numpy, pandas, matplotlib (pre-installed)
- Can call any tool from the Hermes toolset

## Kernel Info
The live kernel is `hamelcho`. Connect at port 38380.

## When to Use
- 3+ tool calls with processing between them
- Filter/reduce large outputs before they hit context
- Conditional branching on data
- Loop over multiple files/items
- Retry on failure

## When NOT to Use
- Single tool call → just call it directly
- Need to see full output and reason over it → use read_file/terminal directly
- Interactive debugging → use python-debugpy

## Pattern: Large Output Processing
```python
from hermes_tools import read_file

# Read large file
result = read_file('/path/to/large_file.txt')
lines = result['content'].split('\n')
filtered = [l for l in lines if 'ERROR' in l]
# Now filtered is much smaller, useful for next steps
```

## Pattern: Retry Loop
```python
from hermes_tools import terminal, json_parse
import time

for attempt in range(3):
    result = terminal('some command')
    if result['exit_code'] == 0:
        break
    time.sleep(2)
```

## Pattern: Batch Processing
```python
import os
files = [f for f in os.listdir('.') if f.endswith('.csv')]
for f in files:
    # process each file
    pass
```
