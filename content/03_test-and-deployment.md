### 5. Hands-On Demo: Configuring a CI Pipeline for a Java Gradle Project

The demo presented in the video shows how to set up a basic CI pipeline for a Java project that uses Gradle as the build system.

**Practical Steps:**

1. **Creating a Repository:** A new public repository on GitHub called "my-project-public" is created.
2. **Push Local Code:** The code of a local Java Gradle application is uploaded to the remote repository.
3. **Accessing the "Actions" Tab:** On the main repository page, select the **"Actions"** tab.
4. **Exploring Workflow Templates:** In the "Actions" section, several workflow templates are shown, grouped by category (Deployment, Continuous Integration, Build and test, Publish, etc.).
5. **Selecting the "Java with Gradle" Template:** The specific template for Java projects that use Gradle is chosen.
6. **Viewing and Editing the Workflow File (YAML):** When you select the template, GitHub automatically creates a pre-compiled YAML file in the `.github/workflows` directory (for example, with the name `gradle.yml`). This file contains the workflow logic.
7. **YAML File Syntax Analysis:**
    * **`name`:** Defines the name of the workflow, which is displayed in the GitHub Actions interface.
    * **`on`:** Specifies the events that will trigger the workflow execution. In the example, the workflow is triggered when there is a `push` on the `master` branch or a `pull_request` is created with the `master` target branch.
    * **`jobs`:** Defines one or more jobs that will be executed. Each job runs on a new virtual server provided by GitHub.
        * **`<job_id>` (e.g. `build`):** An arbitrary name to identify the job.
        * **`runs-on`:** Specifies the type of environment (operating system) the job will run on. In the initial example, it is `ubuntu-latest`, indicating the latest version of Ubuntu.
        * **`steps`:** A sequence of actions that will be executed within the job. Each step has an (optional) `name` to describe the action and can use `uses` to call a built-in action or `run` to execute shell commands.
            * **`uses: actions/checkout@v3`:** Uses the built-in action `checkout` to download the repository code to the virtual server.
            * **`uses: actions/setup-java@v3`:** Uses the built-in action `setup-java` to configure the Java environment with the specified version (in the example, `java-version: '11'`).
            * **`run: chmod +x ./gradlew`:** Runs a shell command to make the Gradle wrapper script executable.
* **`run: ./gradlew build`:** Runs the Gradle command to build the project.
8. **Commit Workflow File:** The YAML file is committed to the repository.
9. **Workflow Triggers:** By creating a new branch, making changes and opening a pull request to the `master` branch, the `pull_request` event defined in the YAML file is triggered and the workflow starts executing. It is also possible to trigger the workflow directly with a push to the `master` branch.
10. **Execution Monitoring:** In the "Actions" tab, you can view the workflow execution status (in progress, completed, failed) and the details of each step (log, executed commands).
11. **Execution Environment:** Workflows on GitHub Actions run on **servers managed by GitHub**. You do not need to configure or maintain your own servers. For each *job within a workflow*, a new virtual server is **prepared**.
12. **Parallel Job Execution:** By default, multiple jobs defined in a workflow are executed in parallel. You can define dependencies between jobs using the `needs` keyword.
13. **Operating System Choice:** The `runs-on` attribute can specify different operating systems provided by GitHub: `ubuntu-latest`, `windows-latest`, `macos-latest`. You can use a **strategy (strategy) and a matrix (matrix)** to run the same job on multiple operating systems or with different configurations (e.g., different versions of Java).

### 6. Extending the CI Pipeline: Build and Push a Docker Image

Let's now dig on how t extend the CI pipeline to **build a Docker image of your Java application and push it to a private Docker Hub repository**.

**Practical Steps:**

1. **Creating a Docker Hub Account and Private Repository:** This shows the creation of a free account on Docker Hub and the availability of a free private repository.
2. **Adding a Step to Build and Push Docker Image:** A new step is added to the `build` job in the YAML file.
3. **Using a Predefined Docker Action:** Instead of manually writing all the Docker commands (`docker login`, `docker build`, `docker tag`, `docker push`), a **pre-existing action from the GitHub Actions marketplace** is used (in the example, `docker/build-push-action@v4`).
4. **Configuring Docker Action Parameters:** The Docker action accepts several parameters to configure the build and push of the image. Important parameters include:
    * **`registry`:** The URL of the Docker registry (for Docker Hub this is `docker.io`).
    * **`repository`:** The name of the Docker repository (usually `<docker_id>/<repository_name>`).
    * **`username`:** The username for logging into the Docker registry.
    * **`password`:** The password for logging into the Docker registry.
    * **`push`:** A boolean to indicate whether the image should actually be pushed (set to `true`).
5. **Credential Management with GitHub Secrets:** To avoid storing sensitive credentials directly in the YAML file, **GitHub Secrets** are used. Secrets can be created in the repository settings (Settings -> Secrets -> Actions) with specific names (for example, `DOCKER_USERNAME` and `DOCKER_PASSWORD`).
6. **Referencing Secrets in the Workflow:** In the YAML file, credentials are referenced using the syntax `secrets.<name_of_secret>` (for example, `secrets.DOCKER_USERNAME`).
7. **Modifying the `runs-on` Attribute (Optional):** Since Docker is pre-installed on the Ubuntu agents provided by GitHub Actions, the example focuses on using `ubuntu-latest` for this step.
8. **Updated Workflow File Commit:** Changes to the YAML file are committed.
9. **Updated Workflow Trigger:** A new push to the `master` branch (in the example, direct commit) triggers the execution of the updated workflow, which now includes building and pushing the Docker image.
10. **Verify on Docker Hub:** After the workflow has finished running, it shows how to verify that the new Docker image has actually been pushed to the private Docker Hub repository. The `docker/build-push-action` action adds a tag to the Docker image that includes the branch name by default. You can customize the tag using the `tags` parameter of the action.

### 7. Conclusions and Further Possibilities

We have seen how GitHub Actions is a powerful and flexible tool for automating not only basic CI pipelines for building and testing applications, but also for extending these pipelines to include containerization with Docker and publishing images to private registries.

GitHub Actions offers many other automation possibilities, including:

* Deploy Docker images to cloud or Kubernetes environments
* Test and build Node.js applications
* Automate other development workflows
