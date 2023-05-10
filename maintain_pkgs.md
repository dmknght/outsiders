# Notes about maintaining packages
There are 2 types of packages in term of source code
1. Open source
2. Non-free

The non-free applications provides prebuild binaries only. It's possible to do automation update depends on the release page.
There are some projects / applications are not able to do automation update
1. Burpsuite
2. Rizin. For some reason, github release page no longer provides release URL in HTML, causing `usan` failed to fetch the latest version

When do auto build on gitlab CI, the burpsuite might have this error:
```angular2html
gbp:error: upstream/2023.2.4 is not a valid treeish
W: Unable to locate package burpsuite
Could not find any location for burpsuite_2023.2.4.orig.tar.*
```