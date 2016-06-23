# Checkstyle-Legacy-Code-Filter
Makes checkstyle relevant when only new committed code needs to adhere to the rules.

A very specific use case for this script can be made when work needs to be done in legacy Code that adheres to no/different checkstyle
rules than the new code you will be writing. It would be nice if the Continuous integration for example would then only fail if your
added lines do not adhere to checkstyle rules. This script manages this.

## Requirements:
- You have a Java Project
- You use git in your project
- You use Maven with checkstyle

## To use it:
- Pipe the diff information from git to the checkstylediff program. Last legacy commit is the last commit that you take as legacy code. It outputs an suppressions.xml file.

`git diff {LAST_LEGACY_COMMIT}...HEAD -U0 -- *.java --minimal | python checkstylediff.py`
- Check checkstyle with of your project where all lines that are legacy are suppressed

`mvn checkstyle:check -Dcheckstyle.suppressions.location="{DIR_WHERE_YOU_RAN_CHECKSTYLEDIFF_IN}/suppressions.xml"`

## When using Travis/ Don't have python:
If you use Travis they have specific containers for java and python is not installed there. To still use the script
you can use [jython](http://www.jython.org/ jython), and then invoke the script with: `java -jar jython-*.jar checkstyle.diff`. But that might be a bit farfetched :smile:
