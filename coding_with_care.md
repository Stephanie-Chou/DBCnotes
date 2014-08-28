#coding with care
How to be responsible and be a better technical teammate. Code will be totz quality. Of particular interest for long term projects

## The power of a README
### Elements of a readme
+ Purpose
+ Getting started
+ Dependencies not just software
+ Configuration instructions
+ Examples
+ Contributing and license if Open Source

## Testing
use simplecov and coveralls
have metrics, even for code cleanliness

## Continuous integration
travis-ci: good for things for open source
jenkins-ci
codeship.io


## Static code quality analysis
+ analyzes ruby code to find anti patterms. code smells and areas of cyclomatic complexity
	+ cyclomatic complexity is how many paths you have. like nested loops
+ encourages ismple, elegantly abstracted code
+ scan often find performance problems brough on by complicated code

## Git workflow
+ one branch per logical feature or feature grouping
+ never push to master only use pull requests
+ small atomic commits with descriptive messages
+ pull requests are peer reviewed before merging


master should always be working, passing, and deployable.