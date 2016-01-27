## Deployment process

### Introduction

This document describes how the Digital Mortgage team members should work on their stories and documentation,
so that pre-production and production deployments would be as straightforward as possible.

Production releases should be frequent, at least one per sprint.


### Structure of the deployment directory

The deployment directory contains documents that describe each version of the Digital Mortgage:

- [Release notes document](release-notes.md) contains high-level information of the changes that contribute to each version
of the system. Versions are presented in reversed chronological order (newest first). On top of the document
there's *current* version. This section contains changes that will come with the next release.
- [releases/versions](releases/versions). This directory contains documents that describe each version of the system. Every document
represents a single release and contains:
    - application versions (which should ideally be the same as the release version)
    - environment variables used by each application
    - state of each database (including version number from alembic_version table)

    The upcoming version of the system is represented by [release-current.md](releases/versions/release-current.md)

- [releases/upgrades](releases/upgrades). This directory contains version-specific documents, each listing the steps
needed for the system to be upgraded to the given version (from the previous version). Upgrades to the upcoming version
should be included in [upgrade-current.md](releases/upgrades/upgrade-current.md).

### Working on a user story

When working on a story, chore or a bug, make sure that the following kinds of changes are documented:

- adding, renaming or removing an environment variable that the application uses
- changes in PostgreSQL databases
- adding, moving or deleting API endpoints
- changes in the logging configuration
- any other changes that may require adjusting the environments for the system to work properly

These changes should be reflected in the following documents:

- [Current release description](releases/versions/release-current.md)
- [Upgrade information](releases/upgrades/upgrade-current.md)

In addition, summary of the changes from your story should be added to the `current` section
of [release notes document](release-notes.md)

Also, when working on your story keep in mind that some changes, such as renaming a DB column,
cannot be deployed in one go with zero downtime and therefore should be planned to be applied in stages,
each stage being a part of a separate release.

### Creating a pull request

When creating a pull request, make sure that you've created a corresponding pull request
in *digital-mortgage-documentation* repository. That pull request should be linked in the description.

### Reviewing code

When reviewing a pull request, make sure that:

- there is a corresponding pull request with the documentation (release notes, current version, upgrade instructions)
- the documentation changes cover all changes that need to be applied to the environments (deployment scripts)

### Merging code from a feature branch

Before merging a pull request from a feature branch to *develop* branch, make sure that the integration deployment
job is updated with the environment changes from that pull request (e.g. configure the jobs to set the new
environment properties).

After merging the code, make sure that Jenkins jobs (*DM-acceptance-tests* in particular) have all passed.

### Deployment to preview

Deployments to preview environment should be done only when all integration jobs have passed in Jenkins. In order
to prepare the deployment, create a new pull request from *develop* branch to *release/production* branch for each
application involved. Before the pull requests are merged, update preview deployment jobs with the environment changes,
just like with integration deployment jobs.

Once the changes are in *release/production* branches, run each preview deployment job in Jenkins. Make sure the
jobs have passed, including *smoke_tests_preview*.

### Preparing for pre-production and production release

In order to prepare the release, perform the following steps:

- Make sure all the preview-related jobs have passed in Jenkins
- Make sure that the system works as expected, by performing basic manual tests on preview
- For each application included in the release, create a pull request from *release/production* branch to *master* branch
- Walk through the changes in those pull requests and compare them with the [release notes](release-notes.md) for
 the coming version. If necessary, update the release notes.
- Make sure all the changes that affect the environments (env. properties, DB schema changes, etc.) are included
 in the [upgrade document](releases/upgrades/upgrade-current.md).
- Review the [upgrade document](releases/upgrades/upgrade-current.md) to make sure the right order of actions
 is indicated (only where it matters). The deployments should be zero-downtime deployments so the upgrade should
 be defined in a way that would allow for this.
- Review the [current version document](releases/versions/release-current.md) to make sure it reflects all the changes
 included in the pull requests to *master* branch.
- In the [release notes document](release-notes.md) copy the *current* section header and rename the lower copy
from `current (YYYY-MM-DD)` to `X.Y.Z (year-month-day)`, where *X.Y.Z* is the release version and the brackets contain
today's date. Example: `3.2.1 (2015-07-29)`
- Create a copy of the [release-current.md](releases/versions/release-current.md) document
 in *releases/versions* directory. Give it the following name: `release-X.Y.Z.md`, where *X.Y.Z*
 is the release version. Adjust the header section of that document to reflect the release version and date. Leave
 *release-current.md* as it is - it will serve as the base for future changes.
- Create a copy of the [upgrade-current.md](releases/upgrades/upgrade-current.md) document in *releases/upgrades*
 directory. Give it the following name: `upgrade-X.Y.Z.md`, where *X.Y.Z* is the release version. Adjust the header
 section of that document to reflect the release version and date. Delete all the content of *upgrade-current.md* file,
 leaving just the header template.
- Create a pull request with the documentation changes
- Get someone to review and merge all the pull requests, both documentation and the actual code
- Once the pull requests have been merged, tag the merge commits with the release version:

```    
    git checkout master
    git pull
    git log
    # Now, copy the number of the last commit from the output.
    # Assuming the release version is X.Y.Z and the last commit is 8f2a7224f589a1467a1c17d977f78ae01f55d6cf, execute:
    git tag -a X.Y.Z 8f2a7224f589a1467a1c17d977f78ae01f55d6cf -m "Release X.Y.Z"
    git push origin X.Y.Z
```

- For each application included in the release, create a release in the corresponding GitHub repository
(releases -> Draft a new release), using the tag you've just created.
- The release is now ready to be deployed. Ask the Infrastructure team to deploy the new version, pointing
 to the release documents. Offer your help.

### After the deployment

The described process shouldn't be considered final. As we deploy new versions, we may find better ways
of working. Therefore, we should make improvements all the time and reflect them in this document.
