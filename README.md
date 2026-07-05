# Rapid Prototyping with Kiro CLI

![From Idea to App with Kiro CLI](assets/from-idea-to-app.jpg)

Turn your idea into a deployed app with the [Kiro CLI](https://kiro.dev).

This repository is intended to be cloned and used right away with your ideas.

It features:
- an `intent.md` file, where you describe your idea briefly (the only thing you have to touch)
- a `.kiro/agents/` directory with agents that Kiro picks up automatically

After a few rounds of questions + answering, you'll have a project with well defined requirements, finished implementation, and ready to deploy.

## How It Works

```
intent.md  +  .kiro/agents/  +  Kiro CLI  →  deployed app
```

You describe your idea inside `intent.md`. Then, you run each agent in order through Kiro CLI.

Each agent will ask you clarifying questions, produce some markdown files, and hand off to the next agent.

The agents follow a simplified **AI Development Lifecycle (AI-DLC)** pattern:

| # | Agent | What it does |
|---|-------|--------------|
| 1 | Product Owner | Asks clarifying questions, writes precise user stories with testable acceptance criteria |
| 2 | Domain Architect | Models business logic, aggregates, commands, events, and rules |
| 3 | Technical Architect | Maps domain models to AWS services, defines API contracts and data schemas |
| 4 | Full Stack Engineer | Implements the app end-to-end using vertical slice methodology |
| 5 | Deployment Engineer | Deploys infrastructure, configures endpoints, validates everything works |

## Getting Started

### Prerequisites

- [Kiro CLI](https://kiro.dev/cli/) installed
- An AWS account (for deployment)

### 1. Clone this repo

or fork it 😉

### 2. Write your intent

Open `intent.md` and replace the placeholder content with your idea. Be specific about what you're building, who it's for, and what success looks like.

For example:

```markdown
# Open Court Finder Intent

Build a web application that helps pickleball players find open
courts nearby in real time so they can get a game without waiting.

## Target Users
Recreational pickleball players who want to find available courts
without driving around or guessing at schedules.

## Success Criteria
- Users can see a map of nearby courts with live availability status
- Court status is crowd-sourced: players check in/out when they arrive or leave
- Filter courts by distance, surface type, and whether they have lights
- Each court page shows current wait estimate and peak hour trends
- Mobile-first responsive design for on-the-go use
- This is a rapid prototype, not intended for production
```

### 3. Run the agents in order

Open your terminal in the cloned repo and run each agent sequentially. Each agent reads the output of the previous one.

**Agent 1: Product Owner** — produces user stories

```bash
kiro-cli chat --agent product-owner
```

> What to say: `Review intent.md and begin the clarification process.`

**Agent 2: Domain Architect** — produces domain models

```bash
kiro-cli chat --agent domain-architect-agent
```

> What to say: `Review the user stories in ai-dlc/{feature-name}/product-owner/user-stories.md and begin domain modeling.`

**Agent 3: Technical Architect** — produces technical specs

```bash
kiro-cli chat --agent technical-architect-agent
```

> What to say: `Review the domain stories and user stories, then begin technical architecture design.`

**Agent 4: Full Stack Engineer** — produces working code

```bash
kiro-cli chat --agent full-stack-engineer-agent
```

> What to say: `Review all artifacts in ai-dlc/{feature-name}/ and begin implementation.`

**Agent 5: Deployment Engineer** — deploys to AWS

```bash
kiro-cli chat --agent deployment-engineer-agent
```

> What to say: `Review the deployment handoff and deploy the application.`

Each agent will ask you clarifying questions before proceeding. The more specific you are in your responses, the better the result.

### 4. Review the artifacts

All agent outputs land in the `ai-dlc/` directory:

```
ai-dlc/
└── {feature-name}/
    ├── product-owner/
    │   ├── process-checklist.md
    │   ├── clarification-questions.md
    │   └── user-stories.md
    ├── domain-architect/
    │   ├── process-checklist.md
    │   └── domain-stories.md
    ├── technical-design/
    │   ├── process-checklist.md
    │   └── technical-architecture.md
    ├── code-generation/
    │   ├── process_checklist.md
    │   ├── implementation_plan.md
    │   └── deployment_handoff.md
    └── deployment/
        ├── progress-checklist.md
        └── deployment-plan.md
```

## What to Expect

Running through all five agents takes time. The agents are thorough by design.

By the time the Full Stack Engineer starts coding, every requirement is explicit, every business rule is documented, and every API contract is defined.

## Customizing the Agents

The agent JSON files in `.kiro/agents/` are fully editable. Common tweaks:

- **Change the model**: Update the `"model"` field (e.g., `claude-sonnet-4-5`)
- **Adjust file paths**: The `toolsSettings` control where agents can read and write
- **Modify prompts**: Each agent's behavior is defined in its `"prompt"` field
- **Change the tech stack**: The Technical Architect and Full Stack Engineer default to AWS CDK + Python + React, but you can adjust the prompt to target different stacks

## Repository Structure

```
.
├── README.md          ← you are here
├── intent.md          ← your idea goes here
├── assets/            ← images
└── .kiro/
    └── agents/
        ├── 1-product-owner.json
        ├── 2-domain-architect.json
        ├── 3-technical-architect.json
        ├── 4-full-stack-engineer.json
        └── 5-deployment-engineer.json
```

## Tips

- **Be opinionated in your intent.** Vague inputs produce generic outputs. If you want a dark theme, say so. If you want animations, specify them.
- **Don't skip agents.** Each one builds on the last. Skipping the Domain Architect means the Technical Architect has to guess at business rules.
- **Answer the questions thoroughly.** The Product Owner will ask 20+ questions. Each answer shapes hundreds of acceptance criteria downstream.
- **Review between agents.** Check each agent's output before moving to the next. It's easier to fix a user story than to refactor deployed code.
- **Iterate on your intent.** If the first run doesn't match your vision, refine `intent.md` and start again. The whole point is rapid iteration.

## Credits

This approach is based on a session by [Ross Myers](https://www.linkedin.com/in/ross-meyers/), Sr. Solutions Architect at AWS, presented at AWS Summit Washington, DC 2026, which seems to be inspired by [d-smith/piggy-bank-app](https://github.com/d-smith/piggy-bank-app), a savings goal tracking app.

## Help

I'd love to help if I can.

Reach out to me on [LinkedIn](https://www.linkedin.com/in/chase-grainger/) if that's you!