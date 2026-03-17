# 🤖 Agent System Guide

A comprehensive guide for newcomers on how to use the agent coordination system (Gui, Alice, Bob, Charlie, Frank).

---

## 📋 Table of Contents

1. [Introduction](#introduction)
2. [Agent Roles](#agent-roles)
3. [How Agents Work Together](#how-agents-work-together)
4. [Getting Started](#getting-started)
5. [Common Workflows](#common-workflows)
6. [Configuration](#configuration)
7. [Best Practices](#best-practices)
8. [Troubleshooting](#troubleshooting)

---

## 🎯 Introduction

This agent system provides a structured approach to software development by coordinating specialized agents for different roles:

- **Gui** (You - Coordinator): Orchestrates the workflow, communicates with user
- **Alice** (Product Manager): Creates requirements, specifications, and user stories
- **Bob** (Developer): Implements features, fixes bugs, writes code
- **Frank** (Code Reviewer): Reviews code for quality, security, and maintainability
- **Charlie** (QA Specialist): Tests code, finds issues, validates solutions

### Why Use This System?

✅ **Clear separation of concerns** - Each agent has a specific expertise
✅ **Better quality** - QA validates code before completion
✅ **Structured process** - Requirements → Implementation → Testing
✅ **Visibility** - Real-time status updates on what each agent is doing
✅ **Scalability** - Easy to add more specialized agents

---

## 👥 Agent Roles

### 🎩 Alice - Product Manager

**Purpose**: Creates detailed requirements and specifications

**When to use**:

- Starting a new feature or project
- Need to define user stories and acceptance criteria
- Creating specifications for complex features
- Documenting business requirements

**Alice will**:

- Analyze your needs and requirements
- Create detailed product requirement documents (PRD)
- Define user stories with acceptance criteria
- Specify business rules and edge cases
- Provide clear implementation guidance

**Output**: Requirement documents, user stories, specifications

---

### 💻 Bob - Developer

**Purpose**: Implements features, fixes bugs, writes code

**When to use**:

- Implementing a feature (after Alice creates requirements)
- Fixing bugs identified by Charlie
- Refactoring code
- Writing unit tests
- Implementing code changes

**Bob will**:

- Read and understand the codebase
- Follow existing code conventions
- Implement features according to specifications
- Write clean, maintainable code
- Run tests and lint checks

**Output**: Code files, patches, implementation summaries

---

### 🎭 Frank - Code Reviewer

**Purpose**: Reviews code quality, ensures best practices, validates code before QA

**When to use**:

- After Bob completes any code implementation
- Before Charlie tests code
- When code quality is in question
- For all code changes (new features, bug fixes, refactoring)

**Frank will**:

- Perform comprehensive code reviews
- Check code style and conventions
- Identify security vulnerabilities
- Assess performance implications
- Verify maintainability and readability
- Classify issues by severity (critical, major, minor)
- Provide detailed review reports with specific recommendations
- Approve code for testing OR request revisions

**Frank outputs**:

- Detailed code review reports
- Issue categorization by severity (critical, major, minor)
- Specific file and line references for issues
- Actionable recommendations for improvements
- Approval decision (APPROVED / NEEDS REVISION)

**Example Frank review**:

```
🔄 Frank is working on... reviewing User Login code quality
- Analyzing authentication security
- Checking password hashing implementation
- Reviewing error handling patterns
- Verifying input validation
```

After completion:

```
✅ Frank finished code review!
- Issues found: 5 (critical: 1, major: 2, minor: 2)
- Review report created: user_login_review.md
- Status: NEEDS REVISION
```

**Output**: Code review reports, issue categorization, approval/rejection status

---

### 🔍 Charlie - QA Specialist

**Purpose**: Tests code, finds issues, validates solutions

**When to use**:

- Before completing a feature implementation
- After Bob finishes code changes
- Investigating reported bugs
- Validating fixes
- Testing edge cases

**Charlie will**:

- Review code for bugs and issues
- Test functionality thoroughly
- Check edge cases
- Validate that requirements are met
- Provide detailed bug reports with reproduction steps

**Output**: Test reports, bug reports, verification summaries

---

### 🎬 Gui - Coordinator (You)

**Purpose**: Orchestrates agents, communicates with user

**Responsibilities**:

- Launch appropriate agents for each task
- Provide real-time status updates to user
- Coordinate between agents
- NEVER write code directly
- Summarize findings and results

**Golden Rule**:

> **DO NOT WRITE CODE YOURSELF!** Always launch Bob to implement code changes.

---

## 🔄 How Agents Work Together

### Typical Workflow

```
┌─────────────────────────────────────────────────────────────┐
│                    USER REQUEST                             │
│                 "Add a login feature"                       │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  🎩 GUI (Coordinator)                                        │
│  - Understands the request                                    │
│  - Launches Alice to create requirements                     │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  🔄 Alice is working on... creating requirements for login  │
│     - Defining user stories                                   │
│     - Specifying authentication flow                          │
│     - Creating acceptance criteria                            │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  ✅ Alice finished creating requirements!                    │
│     - User stories defined                                    │
│     - Login/logout flow specified                             │
│     - 2FA requirements added                                   │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  🎩 GUI (Coordinator)                                        │
│  - Reviews requirements                                        │
│  - Launches Bob to implement the feature                      │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  🔄 Bob is working on... implementing User Login feature    │
│     - Creating login form component                           │
│     - Setting up authentication logic                         │
│     - Integrating with backend API                            │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  ✅ Bob finished implementing User Login!                    │
│     - LoginForm.tsx created                                   │
│     - Auth logic implemented                                   │
│     - API integration complete                                │
└────────────────────────┬────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  🎩 GUI (Coordinator)                                        │
│  - Launches Frank to review code quality                      │
└────────────────────────┬────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  🔄 Frank is working on... reviewing User Login code quality │
│     - Checking code style and conventions                     │
│     - Analyzing security vulnerabilities                      │
│     - Reviewing performance considerations                    │
│     - Verifying maintainability                                │
└────────────────────────┬────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  ✅ Frank finished code review!                             │
│     - Issues found: 3 (critical: 0, major: 1, minor: 2)      │
│     - Review report created: user_login_review.md             │
│     - Status: APPROVED                                       │
└────────────────────────┬────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  🎩 GUI (Coordinator)                                        │
│  - Launches Charlie to validate the implementation           │
└────────────────────────┬────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  🔄 Charlie is working on... testing User Login feature     │
│     - Verifying login flow works                               │
│     - Testing error scenarios                                 │
│     - Checking security requirements                           │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  ✅ Charlie finished testing User Login!                   │
│     - All scenarios tested ✓                                 │
│     - Edge cases handled ✓                                    │
│     - Security verified ✓                                     │
│     - Ready for production ✓                                  │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  🎉 User Login feature complete!                              │
│     Total time: 15 minutes                                     │
│     Next: Deploy to staging                                    │
└─────────────────────────────────────────────────────────────┘
```

---

## 📁 File Structure

The agent system is organized into three main locations:

### 1. Agent Definitions (`~/.config/opencode/agents/`)

Each agent is defined as a markdown file with the following structure:

| Agent   | File                | Identifier    | Mode            | Role |
| ------- | ------------------- | ------------- | --------------- | ---- |
| Gui     | `supervisor-gui.md` | N/A (primary) | Coordinator     |
| Alice   | `pm-alice.md`       | `pm`          | Product Manager |
| Bob     | `dev-bob.md`        | `dev`         | Developer       |
| Frank   | `review-frank.md`   | `review`      | Code Reviewer   |
| Charlie | `qa-charlie.md`     | `qa`          | QA Specialist   |

**Agent Definition Format** (example for Frank):

```markdown
---
description: Code reviewer agent who ensures code quality...
mode: subagent
identifier: review
tools:
  read: true
  write: false
  edit: false
  bash: false
  webfetch: true
---

You are Frank, an experienced code reviewer...
```

### 2. Coordination Rules (`~/.opencode-config`)

Contains system-wide configuration:

- **Agent Communication Preferences**: How to format status updates
- **Status Update Formats**: 🔄/✅ templates for each agent
- **Workflow Rules**: Order of operations (Alice → Bob → Frank → Charlie)
- **Core Rules**: Gui's responsibilities and constraints

**Key Configuration Sections:**

- Real-time status update format requirements
- Individual agent status templates
- Workflow rules with agent sequencing
- Golden rule: "DO NOT WRITE CODE YOURSELF!"


## 🚀 Getting Started

### Prerequisites

1. **Access to agents**: Ensure Alice, Bob, Frank, and Charlie agents are available in your system
2. **Configuration**: Have `~/.opencode-config` set up (see [Configuration](#configuration))
3. **Communication style**: Follow the status update format defined in configuration

### Basic Usage

#### 1. Bug Report Workflow

```
User: "The login page crashes when I enter an invalid email"

→ Gui launches Charlie to investigate
→ Charlie identifies the bug
→ Gui launches Bob to fix it
→ Bob implements the fix
→ Gui launches Frank to review the fix
→ Frank approves the code
→ Gui launches Charlie to verify
→ Feature complete
```

#### 2. Feature Development Workflow

```
User: "Add a dark mode toggle"

→ Gui launches Alice to create requirements
→ Alice creates specs
→ Gui launches Bob to implement
→ Bob builds the feature
→ Gui launches Frank to review the code
→ Frank approves the code
→ Gui launches Charlie to test
→ Charlie validates
→ Feature complete
```

---

## 📚 Common Workflows

### Workflow 1: Fix a Bug

```
1. User reports bug
2. 🎩 Gui: Launch Charlie to investigate
3. 🔍 Charlie: Tests and identifies root cause
4. 🎩 Gui: Review Charlie's findings, launch Bob
5. 💻 Bob: Implements fix based on Charlie's report
6. 🎩 Gui: Launch Frank to review the fix
7. 🎭 Frank: Reviews code quality and security
8. 🎩 Gui: Launch Charlie to verify the fix
9. ✅ Charlie: Tests and confirms fix works
10. 🎉 Bug resolved!
```

### Workflow 2: Add New Feature

```
1. User requests new feature
2. 🎩 Gui: Launch Alice to create requirements
3. 🎩 Alice: Creates detailed PRD with user stories
4. 🎩 Gui: Launch Bob to implement
5. 💻 Bob: Builds feature according to specs
6. 🎩 Gui: Launch Frank to review the code
7. 🎭 Frank: Reviews code quality and security
8. 🎩 Gui: Launch Charlie to test
9. 🔍 Charlie: Validates all requirements met
10. 🎉 Feature complete!
```

### Workflow 3: Refactor Code

```
1. User identifies code to refactor
2. 🎩 Gui: Launch Alice to define refactoring goals
3. 🎩 Alice: Creates refactoring plan
4. 🎩 Gui: Launch Bob to refactor
5. 💻 Bob: Refactors code while preserving functionality
6. 🎩 Gui: Launch Frank to review the refactoring
7. 🎭 Frank: Reviews code quality and maintainability
8. 🎩 Gui: Launch Charlie to test
9. 🔍 Charlie: Ensures no regressions
10. 🎉 Refactoring complete!
```

---

## ⚙️ Configuration

### Setup Global Config

The configuration is stored in `~/.opencode-config`:

```
# Agent Communication Preferences

## Core Rule (IMPORTANT!)

**DO NOT WRITE CODE YOURSELF!** You are a coordinator only.

When issues are found or features are needed:
1. **Launch Charlie (QA)** to investigate the issue
2. **Launch Alice (PM)** to create requirements/specifications if needed
3. **Launch Bob (Developer)** to implement fixes or features
4. **Launch Frank (Code Reviewer)** to review code quality BEFORE Charlie tests
```

### Status Update Format

When launching agents, always provide:

```
🔄 [Agent Name] is working on... [specific task description]
- [sub-task 1]
- [sub-task 2]
- [sub-task 3]
```

When agent completes:

```
✅ [Agent Name] finished [task]!
- [result 1]
- [result 2]
```

---

## 💡 Best Practices

### For Gui (Coordinator)

✅ **DO**:

- Always provide clear status updates
- Explain what each agent will do before launching
- Summarize results after each agent completes
- Launch agents in the correct order
- Use Read/Grep/Glob tools to understand codebase for coordination only

❌ **DON'T**:

- Write code yourself (NEVER!)
- Make assumptions about what agents should do
- Skip the QA step
- Launch multiple agents simultaneously when they have dependencies

### For Users

✅ **DO**:

- Provide clear requirements when asking for features
- Share error messages and console output for bug reports
- Be patient as agents complete their work
- Review the status updates to understand progress

❌ **DON'T**:

- Expect instant results - agents take time
- Skip steps in the workflow
- Ask for code changes without proper requirements

---

## 🔧 Troubleshooting

### Issue: "Agent doesn't respond"

**Solution**:

- Check if the agent is available in your system
- Verify the task description is clear and specific
- Try launching the agent with a simpler task first

### Issue: "Bug keeps coming back"

**Solution**:

- This may indicate the root cause wasn't found
- Ask Charlie to do a deeper investigation
- Consider having Alice review the requirements

### Issue: "Feature doesn't match expectations"

**Solution**:

- Check if Alice's requirements were clear enough
- Review Bob's implementation against Alice's specs
- Have Charlie verify that acceptance criteria are met

---

## 📖 Additional Resources

### Agent Capabilities

Each agent has specialized capabilities:

**Alice (PM)** can:

- Create PRDs and specifications
- Define user stories
- Create acceptance criteria
- Document business requirements

**Bob (Developer)** can:

- Read and understand codebases
- Implement features
- Fix bugs
- Write tests
- Refactor code

**Charlie (QA)** can:

- Test functionality
- Find bugs
- Validate requirements
- Check edge cases
- Verify fixes

**Frank (Code Reviewer)** can:

- Perform comprehensive code reviews
- Check code style and conventions
- Identify security vulnerabilities
- Assess performance implications
- Verify maintainability and readability
- Classify issues by severity (critical, major, minor)
- Provide detailed review reports with recommendations

---

## 🎓 Quick Reference

| Task                | Launch                        | When                     |
| ------------------- | ----------------------------- | ------------------------ |
| Create requirements | Alice                         | Starting new feature     |
| Implement code      | Bob                           | After requirements       |
| Review code         | Frank                         | After Bob implements     |
| Test/Validate       | Charlie                       | After Frank reviews      |
| Investigate bug     | Charlie                       | Bug reported             |
| Fix bug             | Bob                           | After Charlie identifies |
| Refactor code       | Alice → Bob → Frank → Charlie | Code cleanup needed      |

---

## 📞 Getting Help

If you need help with the agent system:

1. Check this guide first
2. Review the configuration in `~/.opencode-config`
3. Look at status updates to understand what's happening
4. Ask questions if unsure about the workflow

---

## 🎯 Summary

The agent system provides a structured, quality-focused approach to software development:

- **Alice** ensures you build the right thing
- **Bob** ensures you build it correctly
- **Frank** ensures code quality and security
- **Charlie** ensures it actually works
- **Gui** ensures everything stays on track

By following this system, you'll get better quality code, clearer processes, and more predictable outcomes.

**Remember: Always let the agents do their jobs, and never write code yourself!**

---

_Last updated: 2025_
