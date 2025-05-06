1. Create a new repository on GH: 

...

### Workflow Syntax

- `name`: name of the workflow describing what it does
- `on`: the keyword `on` specifies events to listen triggering the workflow. In the actual case: 
    - `push`: everytime someone pushes in the master branch, the actual workflow is triggered
    - `pull`: everytime a pull request is created, the actual workflow is triggered

    In this case, having these two triggers makes sense, because: 
    - everytime something is pushed into the `master branch`
    
    or
    
    - everytime someone wants to merge into the `master branch`
    it makes sense to run tests to make sure errors are not introduced in the master branch.

    A complete list of events is present here. <!-- TODO: add link -->

- `jobs`: this section specifies all the actions that are executed when one of the events occurs. One or more `jobs` can be specified

    - `job_name`: this key specifies the name of the job it is goind to define. The name is specified as a key under the `jobs` upper-level key

        - `runs-on`: specifies the machine where the workflow will run. The destination machine can be a `gh-hosted-runner`, a `large-runner`, or a `self-hosted-runner`. More info here. <!-- TODO: add link -->
        
            For gh-hosted-runners, billings exist. They vary with respect the [usage time](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-actions/about-billing-for-github-actions#per-minute-rates), and the specs specified in this section. 
        
            Available options ***for public repositories*** are: 
            
            - Linux (x64, arm64)
            - Windows (x64, arm64)
            - MacOS (intel, arm64)

            Available options ***for private repositories*** are: 
            
            - Linux (x64)
            - Windows (x64)
            - MacOS (intel, arm64)

            A [free tier](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-actions/about-billing-for-github-actions#included-storage-and-minutes) of 500MB of storage and 2000 minutes per month of `GH-Actions` activities exists.
        
        - `steps`: this section specifies the chain of actions to be executed for the given workflow. Each action is specified by the keyword `uses`, that specifies an "***action***" to be used in that particular step.

            - `uses: actions/checkout@v4`: the first action usually specified is the standard action `actions/checkout@v4`. This action takes the code of your repository, and makes it available on the runner machine speciied at the key `runs-on`. 
                > [!NOTE] <!--TODO: look if the callout tag fits the section -->
                >
                > Why is it called *checkout*? The term comes from the cash registers. In this case, the meaning is that the automation tools "taking with him" a specific version of the code to use or modify.

                > [!NOTE] <!--TODO: look if the callout tag fits the section -->
                >
                > The `actions/` path stores predefined actions, like the `checkout` action. 
                > The repository of predefined GH Actions is available [here](https://github.com/actions). 
                
                Look at the [checkout](https://github.com/actions/checkout) repository. *Actions* actually performed by this step are described into the `action.yml` file. For more specifications, look at the documentation of the given action.

                Is a good norm call the needed actions ***specifying its version***.

                Is also possible to run actions from repositories different from `actions/`. For more information, look [here](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/using-pre-written-building-blocks-in-your-workflow#adding-an-action-from-the-same-repository). 

            - `name: Set up JDK 1.8`: the next step is the following: 

                ``` yaml
                - name: Set up JDK 1.8
                  uses: actions/setup-java@v1
                  with: 
                    java-version: 1.8
                ```
                Since the runner is not aware, at the startup, what kind of environment it must use, is necessary to specify it. 

                Since the project is a Java project, we specify the JDK version the runner must have. 

                The keyword `with` specifies a map (key:value) of the input parameters defined by the action. Each action can have one or more input parameters, like *functions*. Such parameters can be passed at the keyword `with`.
            
            - `name: Grant execute permissions for gradlew`: the next step is the following: 

                ``` yaml
                - name: Grant execute permissions for gradlew
                  run: chmod +x gradlew
                ```
                In this case, the step runs a linux command specified at the key `run`. This specific command grants execution permissions to gradlew. 

            - `name: Build with Gradle`: the next step is the following: 
                ``` yaml
                - name: Build with Gradle
                  run: ./gradlew build
                ```
                Like the previous step, in this case an additional command is run. The command launches the build of the java codebase passed to the runner. 

In the following there is the complete file of the mentioned workflow: 
``` yaml
name: Java CI with Gradle

on: 
  push:
    branches: [master]
  pull_request: 
    branches: [master]

jobs: 
  build: 
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up JDK 1.8
      uses: actions/setup-java@v1
      with: 
        java-version: 1.8
    - name: Grant execute permissions for gradlew
      run: chmod +x gradlew
    - name: Build with Gradle
      run: ./gradlew build
```

***

# New Exercise

- `name`: name of the workflow describing what it does
- `on`: the keyword `on` specifies events to listen triggering the workflow. In the actual case: 
    - `push`: everytime someone pushes in the master branch, the actual workflow is triggered
    - `pull`: everytime a pull request is created, the actual workflow is triggered

    In this case, having these two triggers makes sense, because: 
    - everytime something is pushed into the `master branch`
    
    or
    
    - everytime someone wants to merge into the `master branch`
    it makes sense to run tests to make sure errors are not introduced in the master branch.

    A complete list of events is present here. <!-- TODO: add link -->

- `jobs`: this section specifies all the actions that are executed when one of the events occurs. One or more `jobs` can be specified

    - `job_name`: this key specifies the name of the job it is goind to define. The name is specified as a key under the `jobs` upper-level key. In this case the `job_name` is "*build*".

    - `runs-on`: specifies the machine where the workflow will run. The destination machine can be a `gh-hosted-runner`, a `large-runner`, or a `self-hosted-runner`. More info here. <!-- TODO: add link -->
        
            For gh-hosted-runners, billings exist. They vary with respect the [usage time](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-actions/about-billing-for-github-actions#per-minute-rates), and the specs specified in this section. 
        
            Available options ***for public repositories*** are: 
            
            - Linux (x64, arm64)
            - Windows (x64, arm64)
            - MacOS (intel, arm64)

            Available options ***for private repositories*** are: 
            
            - Linux (x64)
            - Windows (x64)
            - MacOS (intel, arm64)

            A [free tier](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-actions/about-billing-for-github-actions#included-storage-and-minutes) of 500MB of storage and 2000 minutes per month of `GH-Actions` activities exists.
        
    - `permissions`: this key specifies the level of permissions the actual workflow has when it runs. 
        > [!NOTE]
        >
        > In other words, it responds the question:
        > "what can this workflow do on this repository?"

        Persmissions are set as follows:
        ``` yaml
        permissions:
          contents: read
        ``` 
        It means that the workflow has the permission to read the files in the repository. Available options for `permissions` are explained [here](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions#jobsjob_idpermissions).

        A permission can be set to `read`, `write` or `none`. The `write` option includes `read`. If `permissions` are not specified, default values are used, which depend by the type of event triggering the workflow.

        Is also possible to defined `permissions: read-all`, `permissions: write-all`, or `permissions: {}`, which denies any permission to the workflow. It is useful when the workflow does not operate on the repository (e.g., if it only sends a notification).

    - `steps`: this section specifies the chain of actions to be executed for the given workflow. Each action is specified by the keyword `uses`, that specifies an "***action***" to be used in that particular step.

        - `uses: actions/checkout@v4`: the first action usually specified is the standard action `actions/checkout@v4`. This action takes the code of your repository, and makes it available on the runner machine speciied at the key `runs-on`. 
            > [!NOTE] <!--TODO: look if the callout tag fits the section -->
            >
            > Why is it called *checkout*? The term comes from the cash registers. In this case, the meaning is that the automation tools "taking with him" a specific version of the code to use or modify.

            > [!NOTE] <!--TODO: look if the callout tag fits the section -->
            >
            > The `actions/` path stores predefined actions, like the `checkout` action. 
            > The repository of predefined GH Actions is available [here](https://github.com/actions). 
            
            Look at the [checkout](https://github.com/actions/checkout) repository. *Actions* actually performed by this step are described into the `action.yml` file. For more specifications, look at the documentation of the given action.

            Is a good norm call the needed actions ***specifying its version***.

            Is also possible to run actions from repositories different from `actions/`. For more information, look [here](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/using-pre-written-building-blocks-in-your-workflow#adding-an-action-from-the-same-repository). 

        - `name: Set up JDK 17`: the next step is the following: 

            ``` yaml
            - name: Set up JDK 17
              uses: actions/setup-java@v4
              with: 
                java-version: 17
                distribution: temurin
            ```
            Since the runner is not aware, at the startup, what kind of environment it must use, is necessary to specify it. 

            Since the project is a Java project, we specify the JDK version the runner must have. 

            The keyword `with` specifies a map (key:value) of the input parameters defined by the action. Each action can have one or more input parameters, like *functions*. Such parameters can be passed at the keyword `with`.
        
        - `name: Setup Gradle`: the next step is the following: 

            ``` yaml
            - name: Setup Gradle
              uses: gradle/actions/setup-gradle@af1da67850ed9a4cedd57bfd976089dd991e2582 # v4.0.0
            ```
            This step set ups Gradle, taking the action from a *different repository*(`gradle/actions/setup-gradle@...`). 

        - `name: Build with Gradle`: the next step is the following: 
            ``` yaml
            - name: Build with Gradle
              run: ./gradlew build
            ```
            In this case, the step runs a linux command specified at the key `run`. This specific command launches the build of the java codebase passed to the runner.

    


``` yaml
name: Java CI with Gradle

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:

    runs-on: ubuntu-latest
    permissions:
      contents: read

    steps:
    - uses: actions/checkout@v4
    - name: Set up JDK 11
      uses: actions/setup-java@v4
      with:
        java-version: '11'
        distribution: 'temurin'

    # Configure Gradle for optimal use in GitHub Actions, including caching of downloaded dependencies.
    # See: https://github.com/gradle/actions/blob/main/setup-gradle/README.md
    - name: Setup Gradle
      uses: gradle/actions/setup-gradle@af1da67850ed9a4cedd57bfd976089dd991e2582 # v4.0.0

    - name: Build with Gradle Wrapper
      run: ./gradlew build

    # NOTE: The Gradle Wrapper is the default and recommended way to run Gradle (https://docs.gradle.org/current/userguide/gradle_wrapper.html).
    # If your project does not have the Gradle Wrapper configured, you can use the following configuration to run Gradle with a specified version.
    #
    # - name: Setup Gradle
    #   uses: gradle/actions/setup-gradle@af1da67850ed9a4cedd57bfd976089dd991e2582 # v4.0.0
    #   with:
    #     gradle-version: '8.9'
    #
    # - name: Build with Gradle 8.9
    #   run: gradle build

  dependency-submission:

    runs-on: ubuntu-latest
    permissions:
      contents: write

    steps:
    - uses: actions/checkout@v4
    - name: Set up JDK 17
      uses: actions/setup-java@v4
      with:
        java-version: '17'
        distribution: 'temurin'
    # Generates and submits a dependency graph, enabling Dependabot Alerts for all project dependencies.
    # See: https://github.com/gradle/actions/blob/main/dependency-submission/README.md
    - name: Generate and submit dependency graph
      uses: gradle/actions/dependency-submission@af1da67850ed9a4cedd57bfd976089dd991e2582 # v4.0.0
```
