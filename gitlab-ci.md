# Result of test gitlab CI x Debian pkging
** This is the next step after Debianize package is completed **
Reference: https://salsa.debian.org/salsa-ci-team/pipeline
1. Add CI script into the project
- The script must **NOT** be in the root folder of upstream source. It's recommended to be in `debian` folder, where debianized files are inside
- Create a file (in this example, it's `autobuild.yml`). Advanced usages are in the URL above
```angular2html
include: https://salsa.debian.org/salsa-ci-team/pipeline/raw/master/salsa-ci.yml

extract-source:
    extends: .provisioning-extract-source

variables:
  RELEASE: 'testing'

build:
  extends: .build-package
```
- Add CI script to project. Go to project -> `Settings` -> `CI/CD` -> Expand the `General pipelines` -> write `debian/autobuild.yml` to `CI/CD configuration file`. The value of this setting is the path of the script inside the project.
Please note that Debian example used the value `recipes/debian.yml@salsa-ci-team/pipeline` but the repo config `@salsa-ci-team/pipeline` will create error `Permission denied`
**Gitlab requires user to use credit card information to validate, otherwise user is unable to use CI/CD**

2. To trigger the CI build, maintainer just need to do `git push`. If maintainer wants to ignore the build, run
```
git push --push-option=ci.skip    # using git 2.10+
git push -o ci.skip               # using git 2.18+
```
