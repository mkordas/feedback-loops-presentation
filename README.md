# feedback-loops-presentation
Blazing Fast Feedback Loops in the Java Universe

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

### Prohibit compilation warnings

- http://programmers.stackexchange.com/questions/94754/how-do-i-convince-my-teammates-that-we-should-not-ignore-compiler-warnings
- http://mark.koli.ch/fail-build-on-java-compiler-warnings
