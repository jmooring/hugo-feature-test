# Hugo Feature Test

Use this repository to test various features with:

- The [Hugo snap package][]
- The [`veriphor/hugo`][] Docker image
- Local installations

All components are imported from the [`jmooring/hugo-module-feature-test`][] module. See its [README][] file for details.

Automated builds for this site are handled by both GitHub Pages and GitLab Pages, utilizing the `veriphor/hugo` Docker image.

Workflow files:

- [GitHub Pages][]
- [GitLab Pages][]

Live sites:

- <https://jmooring.github.io/hugo-feature-test/>
- <https://jmooring.gitlab.io/hugo-feature-test/>

[GitHub Pages]: https://github.com/jmooring/hugo-feature-test/blob/main/.github/workflows/hugo.yaml
[GitLab Pages]: https://github.com/jmooring/hugo-feature-test/blob/main/.gitlab-ci.yml
[Hugo snap package]: https://snapcraft.io/hugo
[README]: https://github.com/jmooring/hugo-module-feature-test?tab=readme-ov-file#readme
[`jmooring/hugo-module-feature-test`]: https://github.com/jmooring/hugo-module-feature-test
[`veriphor/hugo`]: https://hub.docker.com/r/veriphor/hugo
