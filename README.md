Git Flow Cheatsheet
=======================
#### Main branches
The central repo holds two main branches with an infinite lifetime:
- `master`
- `develop`

#### Supporting branches
The different types of branches we may use are:
- `Feature` branches
- `Release` branches
- `Hotfix` branches
- `Bugfix` branches

## Git commands
#### Initialize GitFlow
```
$ git checkout -b develop
```

#### Creating a feature branch
```
$ git checkout -b feature/myfeature develop
Switched to a new branch "feature/myfeature"
```

#### Incorporating a finished feature on develop
```
$ git checkout develop
$ git merge --no-ff feature/myfeature
$ git branch -d feature/myfeature
$ git push origin develop
```

### Release branchs
#### Creating a release branch
```
$ git checkout -b release/1.2 develop
$ ./bump-version.sh 1.2
$ git commit -a -m "Bumped version number to 1.2"
```

#### Finishing a release branch
```
$ git checkout master
$ git merge --no-ff release/1.2
$ git tag -a 1.2
$ git checkout develop
$ git merge --no-ff release/1.2
$ git branch -d release-1.2
```

### Bugfix branches
#### Creating a bugfix branch
```
$ git checkout -b bugfix/exception bug-12
```

#### Incorporating a finished bugfix on release
```
$ git checkout release/1.2
$ git merge --no-ff bugfix/bug-12
$ git branch -d bugfix/bug-12
```

### Hotfix branches
#### Creating a hotfix branch
```
$ git checkout -b hotfix/1.2.1 master
$ ./bump-version.sh 1.2.1
$ git commit -a -m "Bumped version number to 1.2.1"
$ git commit -m "Fixed severe production problem"
```

#### Finishing a hotfix branch
```
$ git checkout master
$ git merge --no-ff hotfix/1.2.1
$ git tag -a 1.2.1
$ git checkout develop
$ git merge --no-ff hotfix/1.2.1
$ git branch -d hotfix/1.2.1
```

## GitFlow commands
#### Initialize GitFlow
```
$ git flow init
Initialized empty Git repository in ~/project/.git/
No branches exist yet. Base branches must be created now.
Branch name for production releases: [main]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []

$ git branch
* develop
 main
```

#### Creating a feature branch
```
$ git flow feature start feature-branch
```

#### Incorporating a finished feature on develop
```
$ git flow feature publish feature-branch
```

### Release branchs
#### Creating a release branch
```
$ git flow release start 1.2.0
Switched to a new branch 'release/1.2.0'
$ ./bump-version.sh 1.2.0
$ git commit -a -m "Bumped version number to 1.2.0"
```

#### Finishing a release branch
```
$ git flow release publish '1.2.0'
```

### Bugfix branches
#### Creating a bugfix branch
```
$ git flow bugfix start bug-12
```

#### Incorporating a finished bugfix on release
```
$ git flow bugfix publish bug-12
```

### Hotfix branches
#### Creating a hotfix branch
```
$ git flow hotfix start 1.2.1
$ ./bump-version.sh 1.2.1
$ git commit -a -m "Bumped version number to 1.2.1"
$ git commit -m "Fixed severe production problem"
```

#### Finishing a hotfix branch
```
$ git flow hotfix publish 1.2.1
```
