# reus
Reusable Github workflows for the APES repositories

* **compile.yml**: compile `build debug` with the build-action for an APES tool.
  Takes a `name` input parameter to label the build step accordingly.
  The `systest` input parameter is a boolean that indicates whether pysys tests
  should be run after a successful compilation.
  For example the caller may want to run the system tests only when checks are
  requested for a merge and could pass
  `${{ github.event.action ==  checks_requested }}`.
  The waf unit tests are being run and their report is published accordingly.
  This should only be run in pull request.
  Needs the permission to write `checks` and `pull-requests`.
  If `systest` is `true`, the workflow proceeds to run the system tests with
  pysys.

* **ford.yml**: create FORD documentation with waf and deploy it to the github
  pages of the repository. Takes a `name` indicating the tool for which the
  documentation is to be created and a `docdir` indicating the parent directory
  of the generated `docu` directory.
  This workflow occupies the "pages" group and cancels running workflows.
  Usually you only want this workflow to run upon pushs to the main branch.
  Needs the permission to write content to the repository.

* **tag.yml**: automatically tag the repository with a new version with the
  [autotag-action](https://github.com/phish108/autotag-action), it should be
  used upon closing a pull request. Versions are following the semver format of
  `v#major.#minor.#patch`. To indicate which level should be increased, the
  commits have to contain on of those tags. The default is `#patch`.
  Needs the permission to write content to the repository.
