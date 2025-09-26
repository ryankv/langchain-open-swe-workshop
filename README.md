# Building with LangChain Open SWE: The Future of Agentic Engineering
## Workshop Guide for Global AI AgentCon Boston

### Workshop Overview
**Format:** Interactive hands-on workshop  
**Prerequisites:** Basic Git/GitHub knowledge
**What you'll build:** A working Open SWE setup with live agent demonstrations

---

## Learning Objectives

By the end of this workshop, you will:
- Understand the architecture and capabilities of autonomous coding agents
- Set up and configure LangChain Open SWE locally and in the cloud
- Execute real-time code generation and modification tasks
- Analyze agent decision-making processes and output quality
- Implement best practices for integrating agentic engineering into development workflows

---

## Pre-Workshop Setup

### Required Accounts & Keys
Participants should have ready:
- GitHub account with admin access to at least one repository
- Anthropic API key (Claude)/ OpenAI / Gemni API
- Basic development environment (Node.js, Yarn)

### Quick Setup Checklist
- [ ] GitHub account verified
- [ ] LLM API key obtained
- [ ] Node.js (v18+) and Yarn installed
- [ ] Code editor ready

---

## Module 1: Understanding Open SWE Architecture

### The Shift from Copilots to Agents

**Interactive Discussion:** "What's the difference between GitHub Copilot and Open SWE?"

Key distinctions:
- **Copilots:** Real-time, IDE-based, line-level suggestions
- **Agents:** Asynchronous, repository-wide, complete task execution

### Multi-Agent Architecture Deep Dive

Open SWE employs four specialized agents:

1. **Manager Agent**
   - Entry point for all tasks
   - Handles user interactions and routing
   - Initializes state management

2. **Planner Agent**
   - Analyzes codebase and requirements
   - Creates detailed execution strategies
   - Requires human approval by default

3. **Programmer Agent**
   - Executes the approved plan
   - Writes code, runs tests, installs dependencies
   - Iterates based on feedback

4. **Reviewer Agent**
   - Quality assurance and error checking
   - Ensures code correctness before PR creation
   - Provides feedback for improvements

### Hands-On Activity: Architecture Mapping
Participants work in pairs to:
1. Map out a typical development workflow
2. Identify where each Open SWE agent would intervene
3. Discuss potential failure points and human oversight needs

---

## Module 2: Local Development Environment (45 minutes)

### Why Focus on Local Development?

Advantages of local setup:
- Full customization control
- Private repository access
- Cost optimization
- Development and testing flexibility
- Complete control over the development environment

### Complete Local Installation

#### Repository Setup
```bash
# Clone the Open SWE repository
git clone https://github.com/langchain-ai/open-swe.git
cd open-swe

# Install dependencies
yarn install
```

#### Environment Configuration

**Agent Configuration (.env file):**
```bash
# Copy example files
cp ./apps/open-swe/.env.example ./apps/open-swe/.env
cp ./apps/web/.env.example ./apps/web/.env
```

**Required Environment Variables:**
```env
# LangSmith tracing
LANGCHAIN_PROJECT="open-swe-workshop"
LANGCHAIN_API_KEY="your-langsmith-key"
LANGCHAIN_TRACING_V2=true

# Model API keys
ANTHROPIC_API_KEY="your-anthropic-key"
OPENAI_API_KEY="your-openai-key" # Optional
GOOGLE_API_KEY="your-google-key" # Optional

# Daytona sandbox
DAYTONA_API_KEY="your-daytona-key"
```

#### GitHub App Creation
1. Navigate to GitHub Developer Settings
2. Create new GitHub App with permissions:
   - Contents: Read & Write
   - Metadata: Read & Write
   - Pull requests: Read & Write
   - Issues: Read & Write

3. Configure OAuth settings
4. Generate private key and client secrets

### Hands-On Lab: Local Setup
Participants complete:
1. Full local installation
2. Environment variable configuration
3. GitHub App creation and setup
4. First local agent run

### Verification and Testing
```bash
# Start the web server
cd apps/web && yarn dev

# Start the agent server (in new terminal)
cd apps/open-swe && yarn dev

# Access the application
# http://localhost:3000
```

---

## Module 3: Live Agent Demonstration

### Real-Time Code Generation

**Scenario 1: Bug Fix Challenge**
- Task: "Fix the authentication error in the login component"
- Watch the agent analyze, plan, and implement the fix
- Observe the decision-making process through logs

**Scenario 2: Feature Implementation**
- Task: "Add user profile picture upload functionality"
- Multi-file changes across frontend and backend
- Database schema modifications

**Scenario 3: Code Refactoring**
- Task: "Refactor the payment processing module for better error handling"
- Complex logic analysis and improvement

### Interactive Monitoring

Participants learn to monitor:
- Agent logs and decision trees
- Sandbox execution environment
- Code quality metrics
- Test execution results

### Hands-On Exercise: Guided Agent Run
Each participant:
1. Selects a task from provided examples
2. Configures and launches their agent
3. Monitors the execution process
4. Reviews the generated pull request

**Example Tasks:**
- Add unit tests to an existing function
- Update dependencies and fix compatibility issues
- Implement a new API endpoint with documentation

---

## Module 4: Agent Decision Analysis

### Understanding Agent Reasoning

**Code Walkthrough:** Examining agent decision logs

Key analysis points:
- How agents parse requirements
- Codebase understanding strategies
- Error handling and recovery
- Quality assurance processes

### Output Quality Assessment

**Framework for Evaluation:**
1. **Code Quality Metrics**
   - Adherence to style guidelines
   - Test coverage implementation
   - Documentation completeness

2. **Functional Correctness**
   - Requirement fulfillment
   - Edge case handling
   - Integration compatibility

3. **Review Process Effectiveness**
   - Error detection rate
   - Improvement suggestions
   - Code optimization

### Interactive Analysis Session
Small groups analyze different agent outputs:
1. Compare approaches to the same task
2. Identify strengths and weaknesses
3. Discuss potential improvements

### Performance Optimization

Techniques for better agent performance:
- Task description clarity
- Repository structure optimization
- Context window management
- Human feedback integration

---

## Module 5: Integration Best Practices

### Workflow Integration Strategies

#### GitHub-Native Approach
```yaml
# Example workflow integration
name: Open SWE Auto-Assignment
on:
  issues:
    types: [labeled]

jobs:
  auto-assign:
    if: contains(github.event.label.name, 'open-swe-auto')
    runs-on: ubuntu-latest
    # ... configuration
```

#### Team Collaboration Patterns
- Task assignment protocols
- Review responsibilities
- Quality gates and approvals
- Rollback procedures

### Cost Management

**Resource Optimization:**
- Task complexity assessment
- Parallel execution limits
- Sandbox usage monitoring
- API cost tracking

### Security Considerations

Critical security practices:
- Repository access controls
- API key management
- Sandbox isolation verification
- Code review requirements

### Hands-On: Workflow Design
Teams design integration workflows for:
1. Bug triage and assignment
2. Feature request processing
3. Code maintenance tasks
4. Documentation updates

---

## Module 6: Advanced Features and Customization

### Human-in-the-Loop Controls

Advanced control features:
- **Mid-task Interruption:** Stop and redirect agent execution
- **Plan Editing:** Modify execution strategies before implementation
- **Double Texting:** Send new instructions during execution
- **Real-time Feedback:** Guide agent behavior dynamically

### Label-Based Automation

**GitHub Label System:**
- `open-swe`: Standard execution with human approval
- `open-swe-auto`: Automatic plan approval
- `open-swe-max`: Enhanced performance with Claude Opus
- `open-swe-max-auto`: Fully automated high-performance mode

### Custom Prompt Engineering

Techniques for better task descriptions:
```markdown
# Effective Task Description Template

## Objective
Clear, specific goal statement

## Context
Relevant background information

## Constraints
Technical limitations and requirements

## Success Criteria
Measurable outcomes and quality standards

## Additional Notes
Edge cases, preferences, and considerations
```

### Hands-On: Customization Challenge

Participants customize their setup:
1. Create custom labels for their workflow
2. Design effective task descriptions
3. Configure human approval thresholds

---

## Module 7: Troubleshooting and Optimization

### Common Issues and Solutions

**Setup Problems:**
- Authentication failures
- Permission errors
- Network connectivity issues
- Environment variable misconfigurations

**Runtime Issues:**
- Agent timeout errors
- Sandbox resource limitations
- API rate limiting
- Code execution failures

**Quality Problems:**
- Incomplete implementations
- Test failures
- Integration conflicts
- Performance degradation

### Debugging Strategies

**Systematic Approach:**
1. Check agent logs for error patterns
2. Verify environment configurations
3. Test API connectivity
4. Review task descriptions for clarity
5. Examine repository structure compatibility

### Performance Tuning

Optimization techniques:
- Task scoping strategies
- Context window optimization
- Resource allocation tuning
- Feedback loop improvements

---

## Wrap-Up and Q&A

### Workshop Recap

Key takeaways:
- Open SWE represents a paradigm shift toward autonomous development
- Multi-agent architecture provides robust, reviewable code generation
- Integration requires thoughtful workflow design
- Human oversight remains critical for quality assurance

### Community Resources

- **GitHub Repository:** https://github.com/langchain-ai/open-swe
- **Documentation:** https://docs.langchain.com/labs/swe  
- **Demo Platform:** https://swe.langchain.com
- **Slack Community:** https://www.langchain.com/join-community
- **Blog Updates:** https://blog.langchain.com

---

## Appendix: Resources and References

### Documentation Links
- [Open SWE GitHub Repository](https://github.com/langchain-ai/open-swe)
- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- [LangChain Platform Guide](https://docs.langchain.com/langchain-platform)

### Support Channels
- GitHub Issues for bug reports
- Slack for community support
