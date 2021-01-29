---
description: >-
  MainVariant: Understanding how GitBook implements variants and versioning
  within GitBook spaces.
---

# Spaces v1.0.1

### GitBook Spaces

A GitBook Space is a set of documents that create a Book. A GitBook Space and Book are synonymous. 

Spaces can have **variants** such as different languages or semantic versions usually for both _minor_ or _patch_ level changes. While a semantic _major_ change can be used it becomes problematic since one cannot hide the variant from the user community during its development. Therefore a semantic _major_ version changed is best implemented as its own GitBook Space and it may be best to do so for _minor_ changes. 

### Variants

Each variant lives on its own branch and as such merging branches as a traditional operation is not recommended within a GitHub Repo. 

GitBook creates a single variant named _main_ when a space is created. This variant is merged to the repo's master branch. It is hidden in GitBook until a new variant is added by an author. The new variant will be pushed to a branch in the repo using the variant's slug as the branch name.

It should be noted that each time a variant is created it will go live \(available to users\) once the variant is merged with its GitHub repo's branch. GitBook does not allow the disabling of a variant during its development to hide it from users. For _minor_ \(and _patch_\) semantic release changes this is not an issue since the variant can be quickly implemented. This is not possible for _major_ release changes 

### Versioning

As mentioned earlier versioning a _major_ semantic release as a variant is problematic since the new version will go live as soon as the variant is created. The best practice is to create a new GitBook Space to hold it and a new GitHub Repo to support it.

Consider the following GitHub Repos which are in turn related to independent GitBook Spaces based on differences of the semantic _major_ version.

| Version | GitHub Repo | GitBook Space |
| :--- | :--- | :--- |
| v1 | owner/using-gitbook-v1 | using-gitbook-v1 |
| v2 | owner/using-gitbook-v2 | using-gitbook-v2 |

Some would argue the same should hold true for _minor_ semantic changes. 

| Version |  |  |
| :--- | :--- | :--- |
| v1.0.0 | owner/using-gitbook-v1.0.0 | using-gitbook-v1.0.0 |
| v1.1.0 | owner/using-gitbook-v1.1.0 | using-gitbook-v1.1.0 |
| v2.0.0 | owner/using-gitbook-v2.0.0 | using-gitbook-v2.0.0 |

Creating a new Repo/Space for _minor_ semantic changes is debatable based on the complexity of the docs the number of functionality changes the development team might implement as a semantic minor release.

It is doubtful that there is a need to create a Repo/Space or a new variant for semantic _patch_ release as changes to the docs for bug fixes or documentation errors/improvements are quick and easy to make. 

### GitBook Default Behavior

GitBook by default likes to merge a space's _main_ variant to the master branch of a repo. There is currently a reported bug by GitBook that does not allow this behavior to be changed unless a variant is added by the author. GitBook does not have a proposed date to release a bug fix.

### Conclusion

Using the GitBook online editor is the path GitBook is trying to convince authors as the best path. In fact, they have deprecated their CLI which allowed some level of local development. The use of the online editor is proprietary but is very useful. 

There are other complex issues with regards to two-way syncing should both the online editor and remote pushes to the repo be made. These can be managed however by understanding GItBook/GitHub integration.

* Do not merge branches.
* The master branch supports the main variant.
* Do not merge variant branches with each other or with the master.
* Remote git pushing should be made to the proper variant branch, they will sync automatically in the online editor.

This can result in a lot of merge activity on each branch if the GitBook online author merges with every change. The best practice is to save work and only merge when needed. Of course, this could be problematic should docs save by GitBook somehow get lost.

#### 



