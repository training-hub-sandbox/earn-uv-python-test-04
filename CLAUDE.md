# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a **GitHub Skills** (skills.github.com) exercise template repository that uses GitHub Actions to deliver interactive, step-by-step learning experiences. The exercise content is delivered through automated GitHub Issues, with workflows that validate learner progress and advance them through each step.

### Template Repository Setup

This repository must be configured as a GitHub template repository:
1. Navigate to repository Settings
2. Check "Template repository" option
3. Learners will copy this exercise using the "Use this template" button
4. Each learner gets their own copy with the same structure, branches, and files

**Important**: Actions are not enabled by default in forks. Learners must use "Use this template" (not fork) to ensure workflows run automatically.

### GitHub Skills Platform Context

This template is designed for the GitHub Skills learning platform (skills.github.com):
- **Purpose**: Create interactive, self-paced coding exercises hosted on GitHub
- **Distribution**: Exercises are typically linked from skills.github.com with a "Use this template" badge
- **Learning Model**: Hands-on practice in real GitHub repositories with automated feedback
- **Common Topics**: Git workflows, GitHub features, CI/CD, coding practices

## Architecture

### Exercise Delivery System

The exercise is orchestrated through a multi-step workflow system:

1. **Initialization (Step 0)**: When a learner copies the template using "Use this template", the `0-start-exercise.yml` workflow:
   - Creates a welcome issue that tracks the learner's progress
   - Posts the first step's content as a comment
   - Enables the Step 1 workflow

2. **Step Progression (Steps 1-N)**: Each step has its own workflow that:
   - Triggers on learner actions (push, pull_request, etc.)
   - Finds the exercise tracking issue
   - Validates the learner's work (optional grading)
   - Posts completion feedback and next step content
   - Enables the next workflow and disables itself

3. **Completion (Final Step)**: The last step workflow posts review content and closes the exercise

**Learner Experience**: Learners follow instructions posted in their issue, complete activities in their repository, and receive automated feedback as they progress through each step.

### Key Components

- **Workflows** (`.github/workflows/`): GitHub Actions that automate exercise progression
  - `0-start-exercise.yml`: Initializes the exercise and creates the tracking issue
  - `1-step.yml`, `2-step.yml`: Individual step workflows (add more as needed)
  - `3-last-step.yml`: Final step that concludes the exercise

- **Step Content** (`.github/steps/`): Markdown files containing learning material
  - `1-step.md`, `2-step.md`, `3-step.md`: Theory and activity instructions for each step
  - `x-review.md`: Final review and next steps content

- **Exercise Toolkit**: External reusable workflows from `skills/exercise-toolkit@v0.7.0` that provide:
  - Reusable workflows: `start-exercise.yml`, `find-exercise-issue.yml`, `finish-exercise.yml`
  - Markdown templates for consistent feedback (step-finished, checking-work, watching-for-progress)
  - Comment posting functionality with variable replacement
  - Validation actions for file existence and keyphrase checking

## Workflow Patterns

### Step Workflow Structure

Each step workflow follows this pattern:

1. **Find Exercise**: Locate the exercise tracking issue
2. **Check Work** (optional): Validate learner's changes using actions like:
   - `skills/exercise-toolkit/actions/file-exists`: Check if files exist
   - `skills/action-keyphrase-checker`: Check for specific text in files
3. **Post Content**: Comment on the issue with:
   - Step completion message
   - Next step content
   - Progress tracking message
4. **Workflow Management**: Disable current workflow, enable next one

### Event Triggers

Workflows are triggered by:
- `workflow_dispatch`: Manual triggering (always enabled for testing)
- Conditional triggers (commented by default): `push`, `pull_request`, `issues`, `issue_comment`
  - Add appropriate triggers based on what learners need to do in each step

## Customization Guide

### Adding a New Step

1. Create step content file: `.github/steps/N-step.md`
2. Create workflow file: `.github/workflows/N-step.yml`
3. Update previous step to point to new step:
   - Change `STEP_N_FILE` environment variable
   - Update `next_step_number` in step-finished comment
   - Update workflow enable command
4. Add event trigger matching the step's required action

### Configuring Grading

To add validation for a step:

1. Add `check_step_work` job to the step's workflow
2. Use validation actions from exercise-toolkit or custom checks
3. Update `post_next_step_content` needs to include `check_step_work`
4. Add check results to the results table in step feedback

### Template Placeholders

When customizing a new exercise, replace all instances of:
- `(replace-me: Exercise title)`
- `(replace-me: Brief one line introduction message)`
- `(replace-me: Target audience description)`
- Step-specific placeholders in each `.github/steps/*.md` file

### README Badge Setup

Update the README.md badge URL to point to your template:
- Replace `template_owner` with your GitHub username or organization
- Replace `template_name` with your repository name
- Update the `name` and `description` parameters for the new repository

## Best Practices

### Exercise Design
- Keep steps focused and achievable (each step should take 5-15 minutes)
- Provide clear, actionable instructions in the activity sections
- Include troubleshooting tips for common issues
- Use the Theory section sparingly - focus on learning by doing

### Workflow Configuration
- Start with simple event triggers (`push` to main branch)
- Only add grading when validation adds clear value
- Test workflows thoroughly before publishing
- Use descriptive workflow and job names for clarity in the Actions tab

### Content Guidelines
- Write for the target audience's skill level
- Use GitHub-styled notifications (NOTE, TIP, WARNING) for important information
- Keep markdown formatting consistent across all step files
- Link to official documentation for deeper learning

## Permissions

Workflows require these permissions:
- `contents: write` - For steps that need to modify repository files
- `actions: write` - For enabling/disabling workflows
- `issues: write` - For posting comments to exercise issue

## Testing

To test exercise progression:
1. **Initial Development**: Do not enable the `push` trigger on `0-start-exercise.yml` until the template is ready
2. **Manual Testing**: Use `workflow_dispatch` to manually trigger each step workflow
3. **End-to-End Testing**:
   - Use "Use this template" to create a personal copy
   - Run through the complete exercise as a learner would
   - **Do not fork** - Actions are not enabled by default in forks
4. **Verification**: Ensure each workflow correctly:
   - Posts appropriate comments to the exercise issue
   - Enables the next workflow
   - Disables itself after completion
   - Validates learner work (if grading is configured)

## Dependencies

- `skills/exercise-toolkit@v0.7.0`: Core exercise infrastructure
- `actions/checkout@v5`: Repository checkout
- `GrantBirki/comment@v2.1.1`: GitHub issue commenting
- `peter-evans/find-comment@v3`: Comment location (for grading steps)
- `skills/action-keyphrase-checker@v1`: Text validation in files
