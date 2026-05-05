# TouchDesigner MCP — Control TouchDesigner via MCP

## Concept
Use a Model Context Protocol (MCP) server to connect an AI agent to TouchDesigner, enabling text-to-TouchDesigner-operator generation and live control.

## Setup

### 1. Install TouchDesigner
Download from [derivative.ca](https://derivative.ca/product)

### 2. Install the MCP server
```bash
cd twozero-mcp-server
pip install -e .
```

### 3. Configure Hermes MCP
Add to your `config.yaml`:
```yaml
mcp_servers:
  touchdesigner:
    command: python
    args:
      - -m
      - twozero_mcp_server.touchdesigner
    env:
      TOUCH_DESIGNER_PATH: /Applications/TouchDesigner.app/Contents/Resources/bin/TouchDesigner
```

### 4. Connect in TouchDesigner
In TouchDesigner, open the MCP extension:
1. Open TouchDesigner
2. Go to → Windows → Other → Param Dialog
3. Load the MCP extension tox
4. The MCP server will start automatically

## Available Tools

### generate_and_connect
Generate TouchDesigner operators from text prompts and connect them in your network.

```json
{
  "prompt": "Create a constant color CHOP connected to a trail CHOP, then to a null CHOP",
  "network_path": "/project1",
  "auto_connect": true
}
```

### list_networks
List all networks in the current TouchDesigner file.

### describe_network
Get a description of operators in a network.

### generate_network
Generate a complete network from a prompt.

### execute_command
Execute a TouchDesigner command (Python script in TD).

### generate_network_export_code
Export the generated network as Python code or a tox file.

## Common Use Cases

### Generate a color ramp
```json
{
  "prompt": "constant CHOP with value 0.5, ramp CHOP from 0 to 1, connected to out1",
  "network_path": "/project1/geo1",
  "auto_connect": true
}
```

### Create an audio-reactive network
```json
{
  "prompt": "Audio analyzer CHOP reading mic input, driving a hue shift on a constant TOP",
  "network_path": "/project1",
  "auto_connect": true
}
```

### Generate a particle system
```json
{
  "prompt": "Particle system with 10000 particles, emitting from a sphere, falling with gravity, connected to a phong-lit sphere",
  "network_path": "/project1/sim1",
  "auto_connect": true
}
```

## Limitations
- TouchDesigner must be running with the MCP extension loaded
- The MCP server connects to a running TD instance, not a headless one
- Complex operators may require manual tweaking after generation
- Not all TouchDesigner operators are exposed via MCP yet

## Workspace Path
User's TouchDesigner files: `~/TouchDesigner/`
MCP extension tox: included in `twozero-mcp-server` package
