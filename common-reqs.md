# Common Requirements

These requirements are shared between all the related compliant projects. Every contributor is obliged to strictly follow them.

### Documentation

##### [.D.1] 
All documentation, explanatory notes and even these requirement descriptions should be prepared using either the [Markdown](https://guides.github.com/features/mastering-markdown/), or [LaTeX](https://www.latex-project.org) format.

##### [.D.2] 
Documentation should be written using *English* language only, except culture-specific explanations and code listings.

##### [.D.3] 
It is highly recommended to comment all code symbols using documentation notation. Use appropriate documentation notation for the target programming language. See *\<language\>/reqs.md -> **[\*.D.TOOLS]** section*.

##### [.D.4] 
It is also highly recommended to use UML for the diagrams.

##### [.D.5] 
All diagrams should be provided in the editor's document format (no PNGs, JPEGs, etc).

### Project and Repo

##### [.PROJ.STRUCTURE]
This is the recommended project structure outline:

* assets/internal/
* assets/export/
* external/
* help/
* platform/
* repo/
* source/
* LICENSE
* README.md
* CREDITS.md

*assets/internal/* should contain the assets that are needed for the development process only.

*external/* should contain the submodules and 3rd party modules

*platform/* should contain the platform related specific resources and assets

##### [.PROJ.1]
Each repo and project should contain the *LICENSE* file and must be licensed.

##### [.PROJ.2]
Each project should be configured to use the Continuous Integration service, preferably [Travis CI](https://travis-ci.com).

##### [.PROJ.3]
Each project should use the appropriate build system with the configurable options for the target platforms. See *\<language\>/reqs.md -> **[\*.B.TOOLS]** section*.

##### [.PROJ.4]
Each project must successfully build after each commit with at least the default configuration. For the default configuration explanation see *\<language\>/reqs.md -> **[\*.B.TOOLS.\*.DEFAULT]** section*.

##### [.PROJ.5]
One repo should contain one project only. You should create a new repo for each new project.

##### [.PROJ.6]
If you need to link the project to another, always use the [Git Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) system. It also applies to 3rd party repos inclusion and dependency management.

##### [.PROJ.7]
Each repo should contain the *README.md*, which describes the project and provides basic instructions and info. If the project is (or should be) compliant with the *Ignix Design*, it should also contain a link to the current repository.


### Code

##### [.CODE.1]
All code listing files should be in an appropriate format and should contain the sign in the document beginning.

Preferred sign format:
```
// ---
// [PROJECT NAME]
// Created by: [INITIAL AUTHOR NAME]
// Modified by:
// - [MODIFICATION AUTHOR NAME]
// - [MODIFICATION AUTHOR NAME]
// - etc
// --- 
```

where the ```//``` is the single-line mark symbol for the target code language.

##### [.CODE.2]
Code symbols usage and naming should follow the convention for the target language. See *\<language\>/reqs.md -> **[\*.C.NAMING]** section*.

##### [.CODE.3]
The code should be both performance-optimized and task-oriented as much as possible.

##### [.CODE.4]
All the code must be intended with *spaces*, not with *tabs*. 2 spaces indentation is highly recommended (except of some languages, that use indentation as a part of the syntax rules).

##### [.CODE.5]
It is highly recommended to have your code auto-reformatted using the IDE tools.

##### [.CODE.6]
It is recommended to use the appropriate IDEs for the target project languages with the provided settings. See *\<language\>/ide.md*.

##### [.CODE.7]
All code should be as cross-platform as possible, except the platform-specific regions or projects.

##### [.CODE.8]
Source folders should be well-structured, code files shouldn't be placed all-in-root folder.

### Privacy

##### [.PRIVACY.G]
Every project and repo should be compliant with the [GDPR privacy policy](https://gdpr-info.eu).

### Credits and 3rd party content

##### [.3RD.1]
Every work, asset, code listing, etc. should be properly credited either file-inside, or by an entry inside the *CREDITS.md* file.

##### [.3RD.2]
Every 3rd party content piece should be fully compliant with the project/repo license.

##### [.3RD.3]
The general rule is, less amount of dependencies = the better.

### Contribution

##### [.CONTRIB.0]
All contributions should be checked and will be only applied if they are compliant with the requirements.

##### [.CONTRIB.1]
All contributions should be performed using the commits and pull requests. 

##### [.CONTRIB.2]
Commit and pull request messages should describe the provided changes. Commit needs a short description. Pull request needs a full description including the changes' reasons.

##### [.CONTRIB.3]
Active project contributors may be credited in the special file *CONTRIBUTORS.md* or inside the *README.md*.

##### [.CONTRIB.4]
Always correctly update *.gitignore* and *.gitmodules* to exclude build, intermediate and other non-source folders and unnecessary modules.