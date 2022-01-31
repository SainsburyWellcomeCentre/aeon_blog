# blog

Details Project Aeon, with a focus on dev practices and notes on technology 
review, challenges and insights.

## ProjectAeon Organization Overview

ProjectAeon is a collaborative effort to perform behavioral neuroscience 
experiments where the behavior and neural activity of freely moving animals 
engaging in a complex task are continuously recorded. This project is 
contributed to by researchers and support staff at UCL's SWC, Neurogears,  
and Datajoint.

If you are interested in joining this project, please contact Jai Bhagat  
(j.bhagat@ucl.ac.uk) and/or Goncalo Lopes (g.lopes@neurogears.org) and/or  
Dario Campagner (d.campagner@ucl.ac.uk).

## Credentials

Below are the required sets of credentials for Project Aeon's members: 

- Microsoft Teams: contact Jai Bhagat, Goncalo Lopes, or Dario Campagner
- SWC Github organization: contact SWC Helpdesk(helpdesk@swc.ucl.ac.uk)
- SWC Github 'aeon' project: contact Jai Bhagat or Goncalo Lopes
- SWC HPC: contact SWC Helpdesk
- 'aeon' HPC Linux group: contact SWC Helpdesk
- Datajoint database username: contact Thinh Nguyen (thinh@vathes.com)

To be granted these credentials, please send a single email to all contact
parties requesting this access.

## Repositories

You must be an SWC Github 'aeon' project member to view these repositories.

### [aeon_mecha](https://github.com/SainsburyWellcomeCentre/aeon_mecha)

Contains Python code for preprocessing, querying, and analyzing experiment  
data. This is the main user repository.

*Note*: All experiment data is acquired and/or triggered and/or synced by  
[Harp devices](https://www.cf-hw.org/harp). Code in the 'aeon_acquisition' 
and 'aeon_mecha' repos makes use of the 
[Harp protocol](https://github.com/harp-tech/protocol) during data 
acquisition, raw data file writing, and raw data file reading. In the  
'harp-tech/protocol' Github repo, you can find documentation on 
[Harp device operation and common registers](https://github.com/harp-tech/protocol/blob/master/Device%201.0%201.4%2020200901.pdf), 
the 
[Harp binary protocol](https://github.com/harp-tech/protocol/blob/master/Binary%20Protocol%201.0%201.1%2020180223.pdf), 
and 
[Harp clock synchronization](https://github.com/harp-tech/protocol/blob/master/Synchronization%20Clock%201.0%201.0%2020200712.pdf).

### [aeon_acquisition](https://github.com/SainsburyWellcomeCentre/aeon_acquisition)

Contains Bonsai visual programming workflows for running the behavioral task 
and acquiring experiment data.

## Dev Practices

### Software Development Life Cycle (SDLC)

Our SDLC roughly follows the 
[iterative model](https://www.tutorialspoint.com/sdlc/sdlc_iterative_model.htm).

### Versioning

We version all the following, according to [SemVer](http://semver.org/) 
numbering: 

- experiments, by name, including full hardware specs (arena, I/O devices, 
  acquisition computer)
    
- repositories

- aeon-db

- aeon-db tables

- ceph directory structure

- qc protocols (for raw and preprocessed data)

- data preprocessing algorithms

- bonsai workflows

### Issue Tracking

We prioritize and track dev progress using Github Discussions and Github 
Issues in Github Projects. Each code repository has at least 3 project boards 
at a given time: one for the issues that need to be completed before the next 
experiment, one for general feature requests and bugs, and one for 
documentation.

### Continuous Integration (CI)

We use Github Actions to run CI. We run unit tests on Github Virtual 
Machines on Windows, MacOS, and Ubuntu. We run integration tests on the SWC 
HPC. Workflows of the CI jobs we run can be found in each repo's respective
`.github/workflows/` directory.

### Contributing

Each repository roughly follows the 
[github flow](https://guides.github.com/introduction/flow/) (which is adapted 
from the more general 
[gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)). 
In brief, each of our repos has a 'main' branch which serves as our 
"in-production" branch, and we have feature and bug fix branches branched off
of 'main'. At certain agreed upon timepoints we create a "stable release" from
our main branch which serves as a snapshot of the code at the time, 
version numbered according to [SemVer](http://semver.org/).

When contributing to any repository, the change to be made should first be 
discussed in a Github Discussion or a Github Issue. Thereafter, contributors
should create a new branch (branched off of 'main') that contains the 
changes/additions they wish to make, and then create a pull request for 
merging this branch into 'main'.

All pull requests will be reviewed by the
[project maintainers](#Project-Maintainers). Minimally, maintainers should 
follow the below steps when reviewing pull requests:

1) Ensure new code adheres to the 
   [style and documentation guidelines](#Style-and-Documentation-Guidelines), 
   is covered by a test, and passes a build test. These can all be checked via
   CI.

2) As necessary, update the `changelog`, `readme`, callgraphs, env config 
   files, and any other relevant doc and config files.

3) Follow the 
   ["squash, rebase, merge"](https://blog.carbonfive.com/always-squash-and-rebase-your-git-commits/) 
   workflow when merging the pull request. In essence, this means that upon 
   completion of a feature branch that is ready to be merged into 'main', 1) 
   the feature branch should be pushed to Github; 2) locally, the feature 
   branch should be rebased and squashed down to the commit from which it 
   branched off of 'main' (this is a useful git command for finding the 
   "branched off" commit: 
   `git log --graph --decorate --pretty=oneline --abbrev-commit`, and this for 
   rebase squashing: `git rebase -i <commitSHA>`); 3) the feature branch 
   should be merged into 'main'; 4) the feature branch should be deleted 
   locally. This way it is ensured that the feature branch keeps its full 
   history on Github, while the 'main' branch keeps an abridged history that 
   is easy to read and undo.

### Style and Documentation Guidelines

Please see our 
[style and documentation guidelines](https://github.com/ProjectAeon/blog/blob/main/style_and_doc_guidelines.md).

We also believe in the 
[readme manifesto](http://thinkinghard.com/blog/TheREADMEManifesto.html), 
which says that `readme` files should provide at least a general description 
that covers _all_ of a project's files, and that one `readme` per subdirectory 
is generally good practice.

### Code of Conduct

Please see our 
[code of conduct](https://github.com/ProjectAeon/blog/blob/main/code_of_conduct.md).

## Project Maintainers

Gonçalo Lopes, Jai Bhagat.

## Repository Contents

- `code_of_conduct.md`: Project Aeon's code of conduct.
- `design_considerations.md`: Design considerations for Project Aeon.
- `glossary.tsv`: A glossary of Project Aeon terminology.
- `init_proj.sh`: A script for initializing a project repository.
- `member_info.tsv`: A table with Project Aeon member names and affiliations.
- `style_and_doc_guidelines.md`: Code style and documentation guidelines for Project Aeon.
