# What is "DevOps"?

- What are challenges in the application development and release process? 
- What of these challenges DevOps tries to solve? 
- What are main DevOps principles? 
- What are tasks and responsibilities of DevOps as a role? 
- What are the differences between DevOps and SRE? 

DevOps is quiet a new concept gaining growing popularity from around the 2008. The term itself is very broad, posing some difficulties in clearly define what is it about.  

The simplest way to define what is DevOps is starting just from the name: it is an intersection fo the words "Development" and "Operations": 
- **Development:** the phase of designing, and running the application; 
- **Operations:** the phase of deploy, operating and monitoring the application. 

We can consider DevOps as the working area with the target of letting development and operations activities run *continuously* in the smoothest way possible, *minimizing development errors* and making *deployment*, *operation* and *improvement* of the application easy. 

To understand better this definition in detail, let's look inside of typical  application development activities.

## From the Idea to the User

Whatever application you are developing, your main goal is always to deliver it to your target end user. 

This target do not depend by the development approach you are using, such as waterfall or agile: in any case, at the end of the process, you want the result of your work to be used by someone else. 

> At the end of the day, is always about creating an application and delivering it to end-users. 

Typical software release process can be summarized with the following schema: 
1. Idea and/or requirements collection; 
2. Design and coding of the solution; 
3. Test of the result; 
4. Building and packaging of the result artifact;
5. Deployment of the solution in a physical place such as a public server, setting it up for the proper use;
6. Announcement to your end-users of the release of the application (or of a new version of it).

By the way, the process do not end here; indeed, while in use: 
- it is necessary to monitor the application performance; 
- it is necessary to track users issues and discovered bugs; 
- more in general, it is necessary to track accessibility of the application and fix emerging problems. 

Moreover, during the development and deployment of the application usually possible improvements may arise in terms of features or optimizations, letting the steps from 1 to 6 previously seen repeat, indefinitely. Once an improvement, is ready ... it is necessary to deliver it to the user *immediately*!

> ... How are usually changes tracked? 

The continuous iteration between ideas or requirements collections, their implementation, deployment and monitoring of and application is at the core of DevOps acitivities.

> [!NOTE]
>
> Making the process of ***continuous-delivery*** of changes ***fast*** and ***reliable*** - i.e., with minimum errors and bugs.


<div align="center">
    <img src="../assets/images/ci-cd-infinite-loop-1.png" width="400"/>
    <img src="../assets/images/ci-cd-infinite-loop-2.png" width="400"/>
</div>
<div align="center">
    <figcaption>
        <em>CI/CD visual representations.</em>
        <br>
        <br>
    </figcaption>
</div>


## Developers and Operations: Existing Frictions

Developers are responsible for coding. Operations are responsible for running the application. This strict division of responsibilities between the two parts let frictions arise. 

### Miscommunication Friction

Typical issues developers and operations might face are: 
<!-- TODO: transform in table-->
Typical issues developers might face are: 
- I cannot run the application a I wrote;
- They code the application without knowing where the application will be deployed.

Typical issues operations might face are: 
- I am running the application but I do not know how it works; 
- They run applications without knowing implementation details.

Because of such a setup, usually coding artifacts where exchanged back and forth between developers and operations. The abscence of pieces of information on one side as well as not considering running details on the other was the origin of origin of the problem, rooted in the different responsibilities the two roles must carry out. 

> [!NOTE]
> 
> As a result, we will have miscommunications between the two areas, stretching release periods from days to weeks.

Back in the days, indeed, the process was not clearly defined nor automated, but was a long, bureaucratic process manually handled, with checklists and documentations (let's think about how Linux was developed, and why `git` was born!).

### Conflict of Interest Friction

The different nature of the two roles is also stressed by the target of their jobs. Indeed: 

<!-- TODO: transform in table -->
- Developers want to add and release new features *fast*;
- Operations want to maintain system stability, limiting failures and keeping the application available.

Because of the two different focuses, they have different incentives. As a consequences, developers want to speed the process up, while operations on the contrary resist to the speed of releases, slowing it down. 

Considering also the difficulties for operations in evaluating code they did not write, is possible to understand that the struggle in keeping the process both fast and reliable can easily become real. 

Despite the high level goal for both roles is delivering high level application to the end user fast apparently pushing them to collaborate, job incentives and goals work on the opposite side: developers incentives is to quickly deliver new features, while operations incentives is to maintain system stability and resist to new changes pushed out.
<!-- TODO: transform in table-->

### Security Friction

In this picture, security teams work on the same side as operations teams, absolving the task of analyze and certificate the security of the application. If it is not achieved, the new release is blocked. In a traditional scenario, security checks are handled as for the operation team with bureaucracy and checklists, making the process slow and unreliable.

### Testing Friction

Several times testers are different people from developers. They test specific features, end-to-end application, deployment environments, performance and so on. 

In a traditional setup, these tests are carried out manually, and they need to be executed very carefully because are the first filter for bugs. Of course, this step slows down the releasing process. 

### Manual Work Friction

Many of the tasks needed during the release process used to be done manually. For example operations used to do most of their activities manually either by directly executing commands on the servers to install tools, configure stuff, do patches or have scripts or small programs they execute. This manual work is slow and error prone because of human error. 

Moreover, with manual work knowledge sharing is very difficult because people who do the tasks would have to document it, and others would have to read it, which is a very time consuming and tedious task. Manual processes are also intransparent, because it is hard to trace who did what and when on every server. Replicating the exact state of a server or piece of infrastructure to backtrack problem origins is nearly impossible, and everything relies on experts memory.

The common characteristic of all these issues is that they all slow down the release cycle and create roadblocks on the application distribution way.

## DevOps Goal 

The goal of DevOps activities is to remove all mentioned frictions and alleviate associated root causes, with the final goal of speeding up the release process of any kind of application.

Tools to achieve the target mainly rely on process automations, to lower the manual labour and, consequently, limit error prone activities. As a consequence, activities can be streamlined and releasing cycle can become tighter and tighter, with an optimization level that can support releasing a software multiple times a day 

### How DevOps achieves its Targets

DevOps defines a combination of cultural philosophies, practices and tools for streamlining software development and its distribution.

In reality, DevOps is not just one set of tools or one specific concept, but it is more a combination of anything that creates the process of releasing the software fast and with high quality, letting developers and operations people work together more often together and talk to each other better.

Naturally, different companies implemented devops in different ways so the actual implementation of devops looked pretty different across different realities.
Nvertheless, since the birth of the concept, common patterns arose, letting different tools emerge and started being use across the the DevOps cycle. 

<!-- TODO: immagine dei tre ruoli --->

Accordingly, in time the DevOps Engineer role became more and more defined, with DevOps Engineers working next to developers, next to operations or in between the two areas. In simple words, the responsibility of the DevOps Engineer is: 

> to build a streamlined release process without any kind of issue slowing down the release.

Because of this responsibility, the concept of *Continuous Integration / Continuous Deployment* arose, highlighting the main activities of DevOps Engineers. 

## Tools and Concepts to Learn as a DevOps Engineer

### Development

Being a DevOps Engineer means working side-by-side with software developers. Developers teams develop an applications with different kind of stacks and languages, with the final development result collected in a ***code repository***.

One of the most used code repositories used nowadays is `git`. As a DevOps Engineer you will not develop the core of the application, but you need to know: how the developers work, which git workflow they are using, how the application is configured to talk with other applications or databases, how automated tests are configurated and used, and so on. 

### Operating Systems

The developed code need to be deployed (most of the times) on a server, so that users can access it. Consequently, an infrastructure to host the development result is needed, on-premise or in cloud. 

As a DevOps Engineer you need to prepare the infrastructure to run the application, which means you will need to interact with the most used OS in the server domain: Linux. Moreover, you will need to use the CLI, because most of the stuff is done in that way with Linux, and understand the Linux filesystem, and so on.

### Network and Security

Deploying an application means also dealing with network and related stuff. Network and networking activities are central in systems security, so, as a DevOps Engineer, you will need to know firewalls, proxy servers, load balancers, HTTP/HTTPS, letting application accessible from outside, IPs, DNSs, and so on. 

Nevertheless, it does not mean that you need to know how to administrate a server from start to finish, such as a Network and System Administratorse, or a Security Engineer: only a basic knowledge is necessary, to be able to interact with the whole infrastructure in the best way possible to deploy your target application. 

### Containers

Containers are the new (and pivotal) standard for applications deployment, since they have become the *defacto standard* for application packaging and distribution. It means that concepts behind virutalization and containerization are needed to be unerstood by a DevOps Engineer. The most popular containerization technology nowadays is Docker. 

### Container Orchestration

Most of the time, any deployed application will run in a Docker container. Few Docker containers can be managed easily using `docker-compose`, but it could be not enough at the growth of the number of containers. 

The most popular option is `Kubernetes`. As a DevOps enginner, you will need the ability to manage the cluster and deploy containerized applications using it. 

Having hundreads of containers and/or thousands of `K8` running of hundreads of servers, tracking applications and infrastructure performance is key. To this regard, setting up performance monitoring services is very important, to track the user-experience quality level under the performance lens, and the infrastructure performance too. Typical tools in this area are `Prometheus`, or `Nagios`. 

### CI/CD and Cloud Technologies

Nowadays many companies use virtual infrastructure on the cloud instead of having and manage their own physical infrastructure. Indeed, having a physical infrastructure to manage means: 
- Selecting the hardware
- Keep the hardware up-to-date physically and digitally, with updates of various type
- Setup a workflow
- Guarantee the reliability of the hardware - in terms of backups, uptime and redundancy
- Guarantee the security of the hardware
- Manage the life-cycle of the hardware in every aspect - operatively, administratively, etc

Having the infrastructure running on the cloud, instead, gives to companies the opportunity to off-load most of these painful aspects, letting the team focusing only on the valuable aspect of their business, and levereaging the cloud elasticity to pay only what the team actually uses. 

### Infrastructure-as-a-Code

A `Development` environment to develop the code is not enough. Indeed, is also needed a `Testing` environment to *test* the code, and a `Production` environment to ship the result to the final user.

Implementing and maintaining manually one of these environments takes a lot of time, and multiplying the effort 3 times is not smart. 

Nevertheless, is possible to automate the creation and maintanance of these environments combining 2 types IaaC tools: 

1. Infrastructure provisioning tools, like `Terraform`;
2. Configuration management tools, like `Ansible`, `Chef` or `Puppet`. 

In this way, your environment is ***more efficient***, ***transparent*** and ***easy to replicate or recover***.

### Scripting Language

Working closely between developers and sys-admins means automating some minor tasks for them, like backups, system monitoring, cron-jobs, network management, and so on. 

To do that can be useful knowing a scripting language. There are many of them, and some can be OS specific, like **Bash** (Linux, MacOS) or **PowerShell** (Windows), or non-OS specific, like ***Python***, **Ruby** or **Go**.

### Version Control

Most of these automation logics are written as-a-code (IaaC), and it means that every chunk of code can be managed... exactly as any other piece of code!

To this regard, version control tools are useful, and is therefore necessary to know `git`.

### But ... Given the Technologies, how to CI/CD?

Let's see a step-by-step typical process for CI/CD: 

1. ***Test***: when process of writing code is completed (for a bug fix or after the completion of a new feature), it is tested. Tests can be of various nature, and can be written by the same developer or by an ad-hoc team.
2. **Packaging**: if tests are passed, the appliaction is packed in a file that contains it. It can be a `.jar` file, a `.zip` or anything else, and is strictly dependent by the language used and the various requirements of the project. Here is where ***Build Tools*** and ***Package Managers*** come in, helping to build and pack the application for the future deployment. 

> [!NOTE]
>
> There are different Building and Packing tools and they are usually associated with a defined language. Some examples are [Maven](https://maven.apache.org/) or [Gradle](https://gradle.org/) for Java, [npm](https://www.npmjs.com/) for JavaScript, ... 

3. **Containerization**: depending by the project, might be necessary to pack the project in a container, to confine the operation area of the application in a defined space and gain control over it. This is an additional packaging step that takes care not directly of the application itself, but of the environment where it will operate. Typical tools used at this stage are `Docker`, `Kubernetes`, `Podman`, and any containerization software.
4. **Repository**: the containerization result must then me stocked in an *artifact repository*, i.e., a repository storing all the images built until here for future usage. Usually, images are versioned too, usually following the semantic version tagging `major.minor.patch`. Typical docker image repositories are Nexus, Docker Hub, GitHub Container Registry (or `ghcr`) ...

These 4 steps can be packed into one fully automated pipeline to reduce the human labor and reduce the probability of related human failure. The type of software that can help you in automating the depicted pipeline is a ***Build Automation Tool*** such as [Jenkins](https://www.jenkins.io/). Tools like `Jenkins` need to be connected to other services such as git repositories to work properly.

The resulting pipeline represents the ***Continuous Integration*** step of the software, enabling is ***Continous Deployment*** through the simple pull, download and run of each new container image.

As a DevOps Engineer, you must be able to deploy the complete CI/CD pipeline for your application, which should be, indeed, *continuous*.
