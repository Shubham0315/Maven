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

What are Maven goals and phases? How are they related?
-
**Maven Goals**
- Goals are specific tasks executed in maven build process 
- Each goal performs specific action like compiling code, packaging apps or cleaning up files
- Goals are executed by maven plugins and each plugin can have multiple goals
- Diff maven goals are :- compile, test, package, clean, install, deploy

**Maven Phases**
- Phases are stages in maven build lifecycle executed in sequence
- Each phase represent step in build process such as validation, compilation, testing, packaging, deployment
- Phases are part of maven's 3 built in lifecycles :- build, clean, site

**Relation between Goals and Phases**
- Goals are bound to phases. When we execute a phase, maven auto executes goals bound to that phase
- Executing a phase also triggers all preceding phases.
  - mvn package :- Executes validate - compile - test- package

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

What is a Maven repository? What are the different types?
-
- Maven repo is a directory where maven stores and retrieves project dependencies, plugins and artifacts. They act as centralises storage to share libraries and project binaries
- Maven repos are used to :-
  - Manage project dependencies efficiently
  - Rescue artifacts across projects
  - Maintain versioning and consistency of dependencies
  - Enable team collab by sharing binaries
 
**Local Repo**
- Stored on developer's machine
- Default location :- ~/.m2/repository
- Maven auto checks local repo first when resolving dependencies. if not found it downloads from remote repo and caches it locally
- We can edit local repo location :

![image](https://github.com/user-attachments/assets/c48709a1-ffd0-4a7f-b78e-5fd7138c3d43)

**Remote Repo**
- Hosted on web servers to share dependencies across teams and organizations
- Maven downloads dependencies from remote repos when not found locally
- Default remote repo :- https://repo.maven.apache.org/maven2
- Configure remote repos in pom.xml

![image](https://github.com/user-attachments/assets/1804cfb7-cf21-4b92-9bd5-d1f1b3015a38)

**Central Repo**
- Maven central is the default remote repo used by maven
- It hosts vast collection of open-source libs
- If dependency is n0t available locally, maven auto downloads it from central

- In short, local is cached on developer's machine, remote is hosted on web servers(public/private), central is default public repo (mvn central)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

How do you specify dependencies in Maven?
-
- In maven dependencies are specified in POM file. Dependencies are modules or libraries required by project to compile, test or run
- Dependencies are specified in <dependencies> tag of pom.xml, inside which we can define aspects like groupID, artifactsID, version, scope

![image](https://github.com/user-attachments/assets/a280229f-4e4c-4340-a221-8552cbb8917b)

- To manage version centrally and avoid repitition, use <dependencyManagement>

![image](https://github.com/user-attachments/assets/a7144e8a-e680-425a-8914-d0b4974b98a1)

- To exclude transitive dependencies

![image](https://github.com/user-attachments/assets/03c9bc4b-82af-40f5-906b-6d9ef2d22453)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

What is the purpose of the 'dependencyManagement' tag in POM?
-
- This tag is used in pom to centralize and control dependency versions across multiple modules or sub projects. It helps maintain consistency, avoid version conflicts and simplify dependency declarations

Centralized Version Control
- Defines versions of dependencies in a parent POM, preventing version conflicts in child modules.
- Child modules can inherit dependencies without specifying versions

Consistency across modules
- Ensures all sub-modules use the same version of a dependency.
- Avoids "version hell" caused by inconsistent versions across modules.

No direct inclusion in classpath
- Dependencies declared in <dependencyManagement> are not included in the classpath automatically.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

How can you exclude a transitive dependency in Maven?
-
- Transitive dependencies are indirectly included via another dependency. Sometimes they cause version conflicts or unnecessary bloat in project
- To exclude transitive dependency, use <exclusions> tag inside <dependency> section

Why exclude transitive dependencies
- To avoid version conflicts when multiple libraries depend on diff versions of same dependency
- To reduce size of build by excluding unnecessary dependencies
- To avoid conflicts with other libs or frameworks in project

![image](https://github.com/user-attachments/assets/3d75d2c9-10fa-462c-9b10-6fbe28fb4aea)

- Each exclusion specofies groupID, artifactID of transitive dependency to be excluded
- Version is not specified here as maven excluded all versions of specified artifact

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

What is the difference between 'compile', 'provided', and 'runtime' scopes in Maven?
-
- In maven scopes define visibility and availability of dependencies at different stages of build lifecycle such as compilation, testing and runtime. Common scopes are compile, provided and runtime

Compile (default)
- 


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

How do you create a custom Maven plugin?
- 
