# Introduction to GitHub Actions
<!--TODO: modifica gli '*' con '-' -->
**GitHub Actions is a platform for automating software developer workflows**. Contrary to popular belief, it is not just another CI/CD (Continuous Integration/Continuous Delivery) tool. CI/CD is just one of many workflows you can automate with GitHub Actions.

The primary goal of GitHub Actions is to **reduce the manual, repetitive, and potentially error-prone tasks** that development teams face on a daily basis. By automating these tasks, developers can focus more on programming and developing new features.

# Developer Workflows and Automation Needs

Developer workflows include all the activities that a team or individual developer performs during the software lifecycle. In particular, for **open source projects hosted on GitHub**, maintainers have to manage numerous **organizational activities**, including:

* **Issue Management:** Review, classification (minor, major, urgent), assignment, reproducibility check.
* **Pull Request Management:** Code review, issue resolution check, merge into main branch.
* **Release Process:** Starting build pipelines, testing and creating the artifact, preparing release notes, updating the tag or version number.
* **Contributor Management:** Onboarding new contributors.

These activities, especially in large projects with many contributors, can become **time-consuming, error-prone, and tedious**. Automating these tasks using GitHub Actions allows you to:

* **Increase efficiency:** Reduce time spent on repetitive tasks.
* **Improve quality:** Standardize processes and reduce human errors.
* **Free up resources:** Allow developers to focus on development.

# GitHub Actions Basics

GitHub Actions automates workflows through the interaction of three key concepts: 
1. **Events** 
2. **Actions**
3. **Workflow**

* **Events:** An event is **something that happens** ***IN or TO your GitHub repository***. These events can be triggered by user activities (for example, creating a pull request, opening an issue, pushing code, merging a pull request) or by integrations with other tools. **Whenever a configured event occurs, you can automatically trigger a workflow**. There is a full list of available events in the [GitHub Actions documentation](https://docs.github.com/en/actions).

* **Actions:** An action is a ***single automated task***. A workflow, instead, is composed of ***one or more actions***. 

    Actions can include things like:
    * Writing a comment on an issue or pull request.
    * Adding a label to an issue.
    * Assigning an issue to a team member.
    * Test code.
    * Build an application.
    * Create and publish artifacts.
    * Deploy an application.

GitHub hosts a marketplace of **pre-built, predefined actions** (accessible via `github.com/actions`) that you can reuse in your own workflows. These actions are repositories that contain code and an `action.yml` file that defines the logic of the action. You can also use actions created by the community or your team. When using an action, you specify its location (usually `organization/repository@version`) via the `uses` attribute.

* **Workflow:** A workflow is a **configurable file (usually in YAML format) that defines an automated process**. A workflow is made up of one or more **jobs**, which in turn contain a sequence of **steps**. Each step executes a single action or script. Workflows are **triggered by one or more events** defined in the YAML file. Workflow files are stored in the `.github/workflows` directory within the repository.

Automating GH-Actions flows means: 

- ***listening*** to events of interest
- ***triggering*** a determined workflow when an event of interest takes place
- ***running*** actions associated to the triggered workflow

The workflow can run one or a multiple actions, in chains. The chain of actions is what builds a defined workflow. 

# CI/CD Pipeline with GitHub Actions

One of the most common workflows that are automated with GitHub Actions is the **Continuous Integration and Continuous Delivery (CI/CD)** pipeline.

**Benefits of using GitHub Actions for CI/CD:**

* **Native Integration:** If your code is already hosted on GitHub, you can use the same tool for CI/CD, **without having to set up and manage third-party tools separately**.
* **Easy to Set Up:** GitHub Actions is designed to be **easy to use even for developers**, without the need for a dedicated DevOps team to set up and maintain the pipeline.
* **Extensive Tool Integration:** GitHub Actions makes it easy to integrate with different tools used in the development process (Node.js, Java, Docker, cloud services like AWS, Azure, Google Cloud, etc.). Instead of manually configuring each integration, you can use pre-existing actions that greatly simplify the process.

**Ease of creating pipelines:**

GitHub Actions offers a user interface integrated into the GitHub repository, accessible via the **"Actions"** tab. Here you can find a large library of pre-configured **workflow templates** for different programming languages, frameworks and deployment scenarios. This allows you to **not have to start from scratch** when creating a workflow.

**Most common use case:**

The most common use case involves a project you already have on GH. Steps are usually: 

<!--TODO: riorganizza in una tabella, con a sx gli step, e a dx la spiegazione -->
- Code commit
- Code test
- Code build
- Code push
- Code deployment
