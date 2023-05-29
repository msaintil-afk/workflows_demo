# GitHub Actions Usage Guide

![GitHub Actions](https://github.githubassets.com/images/modules/site/features/actions-hero.png)

This README.md provides a comprehensive guide on how to use GitHub Actions, a powerful workflow automation and CI/CD (Continuous Integration/Continuous Deployment) tool provided by GitHub. GitHub Actions allow you to automate various tasks, such as building, testing, and deploying your projects.

## Table of Contents
- [What are GitHub Actions?](#what-are-github-actions)
- [Getting Started](#getting-started)
- [Creating a Workflow](#creating-a-workflow)
- [Workflow Syntax](#workflow-syntax)
- [Workflow Triggers](#workflow-triggers)
- [Workflow Steps](#workflow-steps)
- [Workflow Outputs](#workflow-outputs)
- [Workflow Events](#workflow-events)
- [Workflow Environment Variables](#workflow-environment-variables)
- [Workflow Secrets](#workflow-secrets)
- [Using Actions from the Marketplace](#using-actions-from-the-marketplace)
- [Conclusion](#conclusion)

## What are GitHub Actions?

GitHub Actions are event-driven workflows that can be triggered based on various events, such as a push to a repository, the creation of a pull request, or the scheduling of a cron job. Workflows consist of one or more steps, each performing specific tasks such as running scripts, executing commands, or deploying applications.

GitHub Actions can be used for tasks like:

- Building and testing projects
- Deploying applications to servers or cloud platforms
- Publishing packages or artifacts
- Sending notifications or messages
- Running scheduled tasks

## Getting Started

To start using GitHub Actions, follow these steps:

1. Create a GitHub repository or choose an existing one.
2. Navigate to the repository's main page.
3. Click on the "Actions" tab at the top of the repository.
4. Click on the "New workflow" button or choose an existing workflow template.

## Creating a Workflow

A workflow is defined using YAML syntax. It is stored in the `.github/workflows` directory in your repository. Each YAML file represents a separate workflow.

To create a workflow:

1. Navigate to the repository's main page.
2. Click on the "Actions" tab.
3. Click on the "New workflow" button or choose an existing workflow template.
4. Modify the YAML file to define your workflow's steps, triggers, and configuration.

## Workflow Syntax

The syntax for a workflow file consists of a set of keys and values. Here's a basic example of a workflow file:

```yaml
name: My Workflow

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2
      
      - name: Build Project
        run: make build
```

This workflow is triggered when a push event occurs on the `main` branch. It runs on an `ubuntu-latest` runner and consists of two steps: checking out the repository and building the project using the `make build` command.

## Workflow Triggers

A workflow can be triggered by various events, including:

- `push` events: Occur when code is pushed to the repository.
- `pull_request` events: Occur when a pull request is created or updated.
- `schedule` events: Occur based on a cron schedule.
- `workflow_dispatch` events: Manually triggered from the GitHub Actions UI.

You can specify different triggers for a workflow using the `on` key in the YAML file.

## Workflow Steps

Steps define individual tasks that are executed sequentially within a job. Each step can consist of commands, actions, or a combination of both

.

Here's an example of a workflow with multiple steps:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2
      
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: 14
      
      - name: Install Dependencies
        run: npm install
      
      - name: Run Tests
        run: npm test
```

In this example, the workflow checks out the repository, sets up Node.js, installs dependencies, and runs tests.

## Workflow Outputs

Steps can also generate outputs that can be used in subsequent steps or accessed as artifacts of the workflow. You can define outputs using the `outputs` key.

Here's an example:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2
      
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: 14
      
      - name: Install Dependencies
        run: npm install
      
      - name: Run Tests
        run: npm test
        env:
          MY_OUTPUT: ${{ steps.build.outputs.test-results }}
      
      - name: Use Output
        run: echo $MY_OUTPUT
```

In this example, the `Run Tests` step generates an output called `test-results`. The output is accessed in the subsequent `Use Output` step.

## Workflow Events

Events allow you to trigger workflows based on specific conditions. You can use event filters and configuration options to control when a workflow should run.

Here's an example of a workflow that triggers only when a pull request is labeled with "bug":

```yaml
on:
  pull_request:
    types:
      - labeled

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2
      
      # Other steps...
```

## Workflow Environment Variables

You can set environment variables for your workflow using the `env` key. These variables can be accessed by steps within the same job.

Here's an example:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

    env:
      MY_VARIABLE: "Hello, World!"
    
    steps:
      - name: Use Environment Variable
        run: echo $MY_VARIABLE
```

In this example, the workflow sets an environment variable `MY_VARIABLE`, which is then accessed in the subsequent `Use Environment Variable` step.

## Workflow Secrets

GitHub Actions allows you to store and use secrets securely. Secrets are encrypted and can be used as environment variables in workflows.

To use secrets in a workflow:

1. Navigate to your repository's main page.
2. Click on "Settings" and then "Secrets".
3. Click on "New secret" to create a new secret.
4. Provide a name for the secret and its value.
5. In your workflow file, use the secret as an environment variable.

Here's an example of using a secret in a workflow:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Use Secret
        run: echo ${{ secrets.MY_SECRET }}
```

## Using Actions from the Marketplace

GitHub Actions Marketplace provides a wide range of pre-built actions that you can use in your workflows. These actions can help you automate common tasks or integrate with various tools and services.

To use an action from the Marketplace:

1. Navigate to your repository's main page.
2. Click on the "Actions" tab.
3. Click

 on the "New workflow" button or choose an existing workflow template.
4. Modify the YAML file to include the desired action.

Here's an example of using an action to publish a Node.js package to npm:

```yaml
jobs:
  publish:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2
      
      - name: Publish to npm
        uses: actions/npm@v1
        with:
          command: "publish"
          token: ${{ secrets.NPM_TOKEN }}
```

In this example, the workflow uses the `actions/npm` action to publish a package to npm, using the provided NPM token secret.

## Conclusion

GitHub Actions provide a flexible and powerful way to automate workflows, CI/CD processes, and more. By following this guide, you should have a good understanding of how to get started with GitHub Actions, define workflows, trigger events, use environment variables and secrets, and leverage actions from the Marketplace. Start automating your development workflows and enjoy the benefits of efficient and consistent automation with GitHub Actions!
