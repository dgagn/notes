---
title: Commitizen
author: Dany Gagnon
colorlinks: true
---
## Commitizen

Commitizen is very important to keep your
commit consistent with the [Conventional Commit Guideline](https://www.conventionalcommits.org/en/v1.0.0/). It adds a command to the terminal.
```console
cz
```
That command brings a menu to help the user commit with the [angular]() convention.

![Image showing cz command in action](../assets/commitizen.png)

To install the `cz` command in a project, simply run the command -

*PS: Make sure the comitizen package is installed globally before running the second command*

```console
<<<<<<< HEAD
=======
npm i -g commitizen
```

With the `commitizen` installed globally, simply run-

```console
>>>>>>> 101f92b712108498ac66c9237aea5264505ff88b
commitizen init cz-conventional-changelog --yarn --dev --exact
```
