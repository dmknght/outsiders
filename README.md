# What's this
A short note of my idea about my new project. Outsiders is an external repository contains security tools (pentesting, digital forensics, ...) that's not included in Debian repository, or provide latest version when Debian tries keeping stable version. This is nothing new. There are many small projects are doing this. But I saw some good points of this idea.
# Components and structures
- A PPA repository (a good start for now). It should have
1. Testing branch, for latest update of all packages. Bugs are expected
2. Main branch, to use
- A gitlab repository that contains upstream source and Debian configs to build the package
- A build server (local, using Debian stable)
1. Automation upstream update
2. Automation build
3. Test, fix
# Repository data
- Extra security tools that Debian doesn't have
- Extra libraries for the tools that Debian doesn't have
- Latest update for some tools that Debian doesn't update. At this point, it'd be like backport repo.
# Goal achievement
- Be compatible with all Debian-based distro (LTS is the main goal for now). It brings the second point:
- Available for all, without forcing users install a new distro (unless it's not a Debian-based)
- Do not break the system's installation time (package dependency)
- Good quality of toolset for security testing
- Fast update. With automation solution, all upstream packages should be uploaded every week, or even everyday
- Fast patches for build time and packaging time for all tools and libraries
- No time gaps for system updating. At this point, some Debian-based distro will have to fork and rebuild packages from Debian.
- Todo: Multi-arch support
# Definition
- Upstream source: The source code of the original project
- Build time: Program's compilation progress
- Packaging time: The progress that makes a Debian package. It could have build time to compile packages (C, Cpp, Go) projects
- Installation time: When the package is installed inside the system.
- Runtime: When the program starts
# Issues might have
- Upstream update: Some repository doesn't have releases or tags. Or the source code files don't include full source code
- Build time: Missing build dependencies. Any error when compile the project
- Packaging time: Missing build time dependencies. Error violating Debian's build standard
- Installation time: Missing runtime dependencies 
- Runtime: Program crashes, have error due to missing configs or bugs of current upstream version
# Tools and Workflow
## Tools
- `git-buildpackage` (command `gbp`) to update upstream source
- `dh_make` and `devscripts` tools: Generate Debian's configurations to package
- A tool to build (not decided for now) package in the build server
- A custom script to update upstream source, build, and upload package to testing branch automatically, with error handling.
- Any tools for better development process. Update later
# Workflow
## The current idea
1. Update latest upstream code to the build server
2a) Build package (local build server)
2b) Fix build time issues (local build server)
2c) Upload package to test branch (PPA repository)
2d) Test runtime (local test machine)
2e) Fix installation time issues, runtime issues, return 2a (local build server)
3. Upload to main branch

## The idea with CI
1. Update latest upstream code version (Local build server)
2. Provide package in testing stage
   a. Build package (Gitlab CI)
   b. Create patch fix for package time issue if there's any (Local build server). Return 2a.
   c. Upload package to PPA repo, test branch (Gitlab CI)
   d. Test runtime (Local test machine)
   e. Create patch fix for runtime issue if there's any (Local build server). Return 2a.
3. Upload package to main branch (Manually? Need research)

TODO: configurations of packages, how to build, how to install, ...
TODO (done): Research how to use github CI-CD to do automation build. This also means saving time and resources for maintainer https://about.gitlab.com/blog/2016/10/12/automated-debian-package-build-with-gitlab-ci/
TODO: Connect CI-CD with repository (push latest update)
TODO: Build environment should include outsiders's repository in the future

**descr**: Debian is using 2 scripts for automation (repository: https://salsa.debian.org/salsa-ci-team/pipeline)
- https://salsa.debian.org/salsa-ci-team/pipeline/raw/master/salsa-ci.yml
- https://salsa.debian.org/salsa-ci-team/pipeline/raw/master/pipeline-jobs.yml