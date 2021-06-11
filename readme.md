# blog

Details Project Aeon, with a focus on dev practices and notes on technology review, challenges and insights.

## ProjectAeon Organization Overview

ProjectAeon is a colloborative effort to perform behavioral neuroscience experiments where the behavior and neural activity of freely moving animals engaging in a complex task are continuously recorded. This project is contributed to by researchers and support staff at UCL's SWC, Neurogears, and Datajoint.

## Repositories

### [acquisition](https://github.com/ProjectAeon/acquisition)

Contains Bonsai visual programming workflows for running the behavioral task and acquiring experiment data.

### [aeon](https://github.com/ProjectAeon/aeon)

Contains Python code for preprocessing, querying, and analyzing experiment data.

*Note*: All experiment data is acquired and/or triggered and/or synced by [Harp devices](https://www.cf-hw.org/harp). Code in the 'acquisition' and 'aeon' repos makes use of the [Harp protocol](https://github.com/harp-tech/protocol) during data acquisition, raw data file writing, and raw data file reading. In the 'harp-tech/protocol' Github repo, you can find documentation on [Harp device operation and common registers](https://github.com/harp-tech/protocol/blob/master/Device%201.0%201.4%2020200901.pdf), the [Harp binary protocol](https://github.com/harp-tech/protocol/blob/master/Binary%20Protocol%201.0%201.1%2020180223.pdf), and [Harp clock synchronization](https://github.com/harp-tech/protocol/blob/master/Synchronization%20Clock%201.0%201.0%2020200712.pdf).

## Dev Practices

### SDLC

Our SDLC roughly follows the [iterative model](https://www.tutorialspoint.com/sdlc/sdlc_iterative_model.htm).

### Github

We prioritize and track dev progress using Github Discussions and Github Issues in Github Projects. Each code repository has at least 3 project boards at a given time: one for the issues that need to be completed before the next experiment, one for general feature requests and bugs, and one for documentation.

### Contributing

Each repository roughly follows the [gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow): there is a 'main' branch, 'dev' branch, and feature branches branched off of 'dev'. The 'main' branch serves as the production release branch, and the 'dev' branch serves as a bug fix + feature integration branch. 

When contributing to any repository, the change to be made should first be discussed in a Github Discussion or a Github Issue. Thereafter, contributors should create a new 'feature' branch (branched off of 'dev') that contains the changes/additions they wish to make, and then create a pull request for merging this feature branch into 'dev'.

All pull requests will be reviewed by the [project maintainers](#Project-Maintainers). Minimally, maintainers should follow the below steps when reviewing pull requests:

1) Ensure new code adheres to the [style and documentation guidelines](#Style-and-Documentation-Guidelines), is covered by a test, and passes a build test. These can all be checked via CI.

2) As necessary, update the `changelog`, `readme`, and any other relevant doc and config files.

3) Follow the ["squash, rebase, merge"](https://blog.carbonfive.com/always-squash-and-rebase-your-git-commits/) workflow when merging the pull request. In essence, this means that upon completion of a feature branch that is ready to be merged into 'dev', 1) the feature branch should be pushed to github; 2) locally, the feature branch should be rebased and squashed down to the commit from which it branch off of 'dev' (this is a useful git command for finding the "branched off" commit: `git log --graph --decorate --pretty=oneline --abbrev-commit`, and this for rebase squashing: `git rebase -i <commitSHA>`); 3) the feature branch should be merged into 'dev'; 4) the feature branch should be deleted locally. This way it is ensured that the feature branch keeps its full history on github, while the 'dev' branch keeps an abridged history that is easy to read and undo.

Once the project maintainers agree that the 'dev' branch has accumulated sufficient changes to be considered a new release, a pull request should be opened into 'main' from 'dev'. Upon merging 'dev' into 'main', a new release should be made from 'main'. Release version numbering should follow [SemVer](http://semver.org/). 

### Style and Documentation Guidelines

Please see our [style and documentation guidelines](https://github.com/ProjectAeon/blog/blob/main/style_and_doc_guidelines.md).

We also believe in the [readme manifesto](http://thinkinghard.com/blog/TheREADMEManifesto.html), which says that `readme` files should provide at least a general description that covers _all_ of a project's files, and that one `readme` per subdirectory is generally good practice.

### Code of Conduct

Please see our [code of conduct](https://github.com/ProjectAeon/blog/blob/main/code_of_conduct.md).

## Project Maintainers

Gonçalo Lopes, Jai Bhagat.

## Repository Contents

- `code_of_conduct.md`: Our organization's code of conduct.
- `design_considerations.md`: Design considerations for Project Aeon.
- `init_proj.sh`: A script for initializing a project repository.
- `style_and_doc_guidelines.md`: Code style and documentation guidelines for Project Aeon.