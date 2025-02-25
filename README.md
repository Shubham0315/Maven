# Maven

What is Maven and why is it used in DevOps?
-
- Maven is a powerful build automation and project management tool primarily used for Java-based projects, though it can also be used for other programming languages. It is developed by the Apache Software Foundation.
- Why Maven in used in DevOps?
  - **Dependency Management**: Maven automatically manages project dependencies by downloading the required libraries and plugins from a central repository, ensuring consistent builds across different environments.
  - **Build Automation**: It automates the process of compiling source code, running tests, packaging the application (e.g., as a JAR or WAR), and deploying it.
  - **Standardized Project Structure**: Maven enforces a standard project structure, making it easier for teams to understand and maintain the codebase. (groupID, artifactID, version)
  - **Integration with CI/CD Tools** :Maven integrates seamlessly with CI/CD tools like Jenkins, enabling automated builds, testing, and deployment in a DevOps pipeline.
  - **Version Control and Consistency**: It ensures consistent builds by maintaining version control of dependencies, reducing conflicts and compatibility issues.
  - **Extensibility with Plugins**: Maven is highly extensible with a wide variety of plugins available for tasks such as testing (JUnit), code analysis (SonarQube), and deployment.
 
- How is Maven used in a DevOps Pipeline?
  - **Code Compilation**: Maven compiles the source code into executable bytecode.
  - **Unit Testing**: It runs unit tests using frameworks like JUnit or TestNG.
  - **Code Quality Checks**: It integrates with tools like SonarQube for static code analysis.
  - **Packaging and Artifact Management**: Maven packages the application as a JAR/WAR and stores it in an artifact repository (e.g., Nexus, Artifactory).
  - **Deployment**: The packaged artifact is deployed to testing or production environments, often integrated with tools like Jenkins or Ansible for automation.
 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

What are the main components of Maven?
-
- Maven has several key components that make it a powerful build automation and project management tool:

POM (Project Object Model)
- Core of maven project, containsd all config details like dependencies, plugins, goals, project metadata
- Defines project structure, dependencies, build settings and plugins. Also manages versioning and build lifecycle.

![image](https://github.com/user-attachments/assets/796e9a28-b2a4-49fa-982e-9f5c3635881c)

**Dependencies**
- External libraries or modules required by the project.
- Maven automatically downloads the required dependencies from central or remote repositories and keeps them in the local repository.
- In the above POM example, JUnit is added as a test dependency. (SS)

**Repositories**
- Local Repository: Stored on the developer's machine. Maven first checks this location when resolving dependencies.
- Remote Repository: Online repositories (like Maven Central or custom Nexus/Artifactory) where Maven looks for dependencies not found locally.
- Central Repository: The default public repository from which Maven downloads libraries.

**Build Lifecycle**
- Sequence of phases to build and distribute project
- Phases:
  - validate: Checks the project structure and configuration.
  - compile: Compiles the source code.
  - test: Runs unit tests.
  - package: Bundles the compiled code into a distributable format (e.g., JAR, WAR).
  - verify: Runs integration tests to ensure quality.
  - install: Installs the package in the local repository.
  - deploy: Copies the final package to a remote repository for sharing.
 
**Plugins**
- Extensions that add specific tasks to maven lifecycle (compiling code, run tests, packaging)
- To enhance maven's functionality allowing to perform tasks like code analysis, deployment and reporting
- e.g :- maven-compiler-plugin :- to compile java code

Goals
- Tasks executed in specific phase of build lifecycle
- e.g :- clean :- deletes previos artifacts, package :- compiles and packages project

Profiles
- These are config for diff build env like dev, testing, prod
- Allow conditional build and deployments by activating specific config based on env variables

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

What is a POM file in Maven? What are its key elements?
- 
- POM stands for Project Object Model. It is fundamental config unit in maven
- It is XML file located at root of maven project
- POM manages dependencies, plugins, build settings, project structure

- POM defines project and its dependencies ensuring consistent builds across diff env
- Manages project versioning and build lifecycle
- Specifies plugins and goals needed to build, test and deploy project

Project Coordinates
- groupID :- Unique identifier for project's group or organization
- artifactID :- Name of project or module
- version :- Version of project (1.0.0-SNAPSHOT)
- packaging :- Type of artifact generated (JAR/WAR/POM)

Dependencies 
- Lists external libs required by project
- scope :- defines class path visibility (compile, test, provided, runtime)

Build Config
- Configures how project is built, including source directories and plugins
- plugins :- extend mavens functionality

Repositories
- Defines remote repos from which maven resolved dependencies

Properties
- Centralized config values for easy maintenance and version upgrades

Profiles
- Allow conditional build for diff env
- Activated using -P :- mvn clean install -Pprod

Parent POM
- Inherits configs and dependencies from parent object

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

What is the lifecycle of Maven?
-
- Maven's build lifecycle is a series of well-defined phases that handle complete build and deployment process of project. Each phase represent stage in build process and executing phases also triggers all other phases

**Default (Build) Lifecycle**
- Handles project deployment
- Uses are validate project structure, initialize, compile source code, test to run unit tests, package into WAR/JAR distributable format, verify checks results of tests, install packages into local maven repo, deploy to remote repo
- mvn package

**Clean Lifecycle**
- Cleans project by deleting previously compiled artifacts.
- pre clean, clean to delete artifacts (target/ dir), post clean
- mvn clean

**Site Lifecycle**
- Generates project documentation and reports.
- pre site, site to generate, post site, site deploy to deploy generated site to web server or repo
- mvn site

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

