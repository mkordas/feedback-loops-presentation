# feedback-loops-presentation
Blazing Fast Feedback Loops in the Java Universe

## What it is?

* anything that gives opprotunity to inspect and adapt
* ability to make constant adjustments
* do a thing and check how it went
* cost per assumption...
* bit of feedback now is better than a lot of feedback later
* with fast feedback we learn much more
* anything that prevents change also prevents feedback

## How to?

- parallelize
- remove duplicates
- push tests down in pyramid
- no waiting
- small pieces
- great tools

## Types

- retros
- planning
- customer opinion
- creating stories
- standup
- ci/build monitor
- demos (dev and business)
- sign-off
- iterations
- metrics
- exploring

## Length

#### Instant

- IDE
- pair programming
- compiler

#### Seconds

- unit tests
- static analysis

#### Minutes

- integration/system tests
- builds on master/pipelines
- performance tests
- health checks

#### Days

- manual/exploratory tests
- demos/UAT

## Ideas

- warnings
- `task-tree` https://github.com/dorongold/gradle-task-tree
- badges: current version, build status, button to release/deploy
- base plugin
 - `java`, `groovy`, `maven` plugins
 - `provided` configuration
 - compiler configuration for Java and Groovy
  - `-Xlint:all`
  - `-Werror`
- `--continue` to gather errors
- quality plugin
- script to update maven dependencies
- custom codeStyleSettings.xml
- custom codeInsightSettings.xml
- custom inspectionProfiles
- Java | Dependency issues | Illegal package dependencies
- JaCoCo rules - Maven
- FindBugs for tests Maven
- Sevntu Checkstyle Maven
- check commit message - validate phase
 - `"git log origin/master..HEAD".execute().text`
- `classycle-maven-plugin`
 - sets
 - layers
 - check sets, check layeringOf, check absenceOfPackageCycles
- GitGuard https://chrome.google.com/webstore/detail/gitguard/dlbacfedgdjanlkofjckclmgmijbhakl
- `CONTRIBUTING.md` - link
- http://www.gdub.rocks/
- pipelines
  - every change on master goes instantly through all pipeline steps that needs to be passed successfully to release the code to production
  - artifacts are built once (push artifacts instead of git commit)
- Emmet
 - In XML type `fast>xml>creation+modification^test>me>try$*10` and press TAB.
- build screens
- open pull requests dashboard
- on each problem
 - add health check
 - add rule
 - add note to README
- catch exceptions and throwables

### Prohibit compilation warnings

- http://programmers.stackexchange.com/questions/94754/how-do-i-convince-my-teammates-that-we-should-not-ignore-compiler-warnings
- http://mark.koli.ch/fail-build-on-java-compiler-warnings

### Retrospectives

> If it is not fun, you're doing it wrong

Types:

* Speed-car Abyss
* Speedboat
* Starfish
* Six Thinking Hats
* Dialogue Sheets
* Sandwich

### Never leave problems without improvement

Whenever you notice that some feedback was too late try to make it faster in future.

- broken environment: add health check build 
- style-related commend during code review: add task to enable new static analysis check
- unmeaningful exception: add more context and fail fast
- struggling with technology: ask question on StackOverflow (and event answer by yourself)
- struggling with project: add to knowledge base (README.md, wiki)

### Unit Tests

Have a suite of really fast and reliable tests
- milliseconds (hundreds of tests per second)
- very repeatable
- run in parallel
- fully isolated
- FIRST
  - Fast (milliseconds or less)
  - Isolated (test only one unit)
  - Repeatable (able to be run millions of times on any machine with the same result)
  - Self verifying (either passes or fails)
  - Timely (written first)

### Code Style / Static Analysis

- Checkstyle, PMD, FindBugs, CodeNarc
- agree on common rules for all projects
 - Gradle plugin
 - Maven plugin
 - Maven parent POM (tricky)
- use blacklists instead of whitelists
 
### Internal Quality Plugin

- zero configuration by default
 - integrates all agreed tools with all rules enabled
 - disables unwanted rules
- possibility to customize for project needs
- instead of `gradlew checkstyleMain pmdMain findbugsMain codenarcMain checkstyleTest pmdTest findbugsTest codenarcTest` just `gradlew quality`

### Late static analysis feedback

- gather violations from all tools and modules
 - `gradlew quality --continue`
 - `mvn -fae` or `mvn --fail-at-end`
- CheckStyle-IDEA
- FindBugs-IDEA
- SonarLint

### Sanity build matrix

Periodically run on master series of builds using different configurations that developers may use
- various Java and Maven versions
- various parameters like `-DskipTests`?
- various JVM params like locale

### Challenge your tests

- https://github.com/TestingResearchIllinois/NonDex
- Pitest 
  - `test-compile org.pitest:pitest-maven:scmMutationCoverage -Dinclude=ADDED,UNKNOWN,MODIFIED -DmutationThreshold=100`

### Base Plugin

- Applies java, groovy, maven plugins
- Always shows full stacktraces, even if --stacktrace is forgotten
- Adds provided configuration (missing in Gradle)
- Configures repositories with dependencies
- Adds tuned compiler configuration for Java and Groovy
 - Displays detailed information about all warnings (-Xlint:all option)
 - Fails build on any unsuppressed warning (-Werror option)
- Adds configuration to run tests in parallel
- Enables rich test logging with summary (Tests run: 3, Failures: 2, Skipped: 1) and full stacktraces
- Configures wrapper task with latest Gradle
- Applies taskTree plugin
- Applies com.github.ben-manes.versions plugin
 - run gradlew dependencyUpdates to display all dependency updates in project
- Prints Gradle and JVM versions in the output
