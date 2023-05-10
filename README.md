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
1. Update latest upstream code to the build server
2a) Build package (test)
2b) Fix build time issues
2c) Upload package to test branch (PPA repository)
2d) Test runtime
2e) Fix installation time issues, runtime issues, return 2a
3. Upload to main branch

TODO: configurations of packages, how to build, how to install, ...