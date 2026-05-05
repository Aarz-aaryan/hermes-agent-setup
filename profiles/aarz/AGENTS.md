# AGENTS.md - Aarz Profile Agent Definitions

## Primary Agent

**Name:** Aarz-Primary  
**Model:** Claude Sonnet 4.5  
**Role:** Primary assistant and task executor

### Capabilities
- Full tool access via Composio integrations
- Code development and review
- Research and information synthesis
- Task automation and workflow creation
- Multi-step project management

### Configuration
```yaml
max_iterations: 100
timeout: 120
temperature: 0.7
tools:
  - github (full access)
  - gmail
  - google_calendar
  - notion
  - filesystem
  - terminal
```

## Sub-Agents

### Research Agent
- Web search and information gathering
- Document synthesis
- Citation management

### Code Agent
- Code review and generation
- Testing and debugging
- Documentation

### DevOps Agent
- CI/CD pipeline management
- Infrastructure automation
- Monitoring and alerting
