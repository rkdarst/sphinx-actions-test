Demo of Sphix + github actions to deploy it
===========================================

This demonstrates building a Github Action workflow.  Main points:

* Everything in ``.github/workflows``
* You can have multiple workflow files (presumably)
* Similar to ``.travis.yml`` but with custom syntax
* Each workflow has multiple **steps**.  Each step can be an inline
  shell script or reference to another action.  Actions are written
  with ``uses:`` and refer to another Github repository where the
  action is defened.  Thus, there is more reusability of certain building
  blocks.

* For example, the repo is not automatically checked out (because you
  could have actions that run on issues only which comment on the
  issue).  You check out a repository with ``- uses:
  actions/checkout@v1`` which uses the environment variables to check
  out the repository to ``.``.


https://rkdarst.github.io/sphinx-actions-test/

Useful reading
--------------
* General actions intro: https://help.github.com/en/articles/about-github-actions
* Description of build environment: https://help.github.com/en/articles/virtual-environments-for-github-actions
* Full reference for workflow action file syntax: https://help.github.com/en/articles/workflow-syntax-for-github-actions


Limitations
-----------

This repo doesn't do "build on PR, deploy on master" - need to find
the syntax to do that.

Deployment does not currently work with ``GITHUB_TOKEN`` because
pushing back to the repo with this token does not trigger the Github
Pages building actions.  See
https://github.com/maxheld83/ghpages/issues/1 and basically every
other Github Pages deploy action.

Workarounds are to make a Personal Access Token (which then has access
to *all* your repositories - not good) or perhaps a deploy ssh key
(which I haven't seen any pre-build action use).
