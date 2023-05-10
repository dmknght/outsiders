# What's this
A short note of my idea about my new project. Outsiders is an external repository contains security tools (pentesting, digital forensics, ...) that's not included in Debian repository, or provide latest version when Debian tries keeping stable version. This is nothing new. There are many small projects are doing this. But I saw some good points of this idea.
# Components and structures
- A PPA repository (a good start for now). It should have
1. Testing branch, for latest update of all packages. Bugs are expected
2. Main branch, to use
- A gitlab repository that contains upstream source and Debian configs to build the package
- A build server (local) to do
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
# Problems
- Build time
- Packaging time
- Installation time
- Runtime
