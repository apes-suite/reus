# reus
Reusable Github workflows for the APES repositories

* **compile.yml**: compile `build debug` with the build-action for an APES tool.
  Takes a `name` input parameter to label the build step accordingly.
  The waf unit tests are being run and their report is published accordingly.
  This should only be run in pull request.

* **tag.yml**: automatically tag the repository with a new version with the
  [autotag-action](https://github.com/phish108/autotag-action), it should be used
  upon closing a pull request. Versions are following the semver format of
  `v#major.#minor.#patch`. To indicate which level should be increased, the commits
  have to contain on of those tags. The default is `#patch`.
