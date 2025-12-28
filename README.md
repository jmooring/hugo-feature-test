# Hugo Feature Test

Use this repository to test various features with:

- The [Hugo snap package](https://snapcraft.io/hugo)
- The [veriphor/hugo Docker image](https://hub.docker.com/r/veriphor/hugo)
- Local installations

This site:

1. Includes content from a Hugo module
1. Transpiles Sass to CSS using Dart Sass
1. Performs vendor prefixing of CSS rules using the postcss, postcss-cli, and autoprefixer Node.js packages
1. Processes CSS files using the tailwindcss and @tailwindcss-cli Node.js packages
1. Encodes images to the WebP format
1. Includes a content file named hugö.md to verify that the Git `core.quotepath` setting is `false` [^1]
1. Includes Markdown content
1. Includes Emacs Org mode content
1. Includes HTML content
1. Includes AsciiDoc content[^2]
1. Includes Pandoc content[^3]
1. Includes reStructuredText content[^4]

[^1]: See [issue #9810](https://github.com/gohugoio/hugo/issues/9810). Git's `core.quotepath` setting is `false` if `/tests/hugö` has a non-zero "last modified" date.
[^2]: You must install Asciidoctor and its dependencies (Ruby) to render the AsciiDoc content format.
[^3]: You must install Pandoc to render the Pandoc content format.
[^4]: You must install Docutils and its dependencies (Python) to render the reStructuredText content format.

## Dependencies

> [!NOTE]
> The Hugo snap package and the veriphor/hugo Docker image include the dependencies below. No further action is required.

To build this site you must install the following:

- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Go](https://go.dev/doc/install)
- [Node.js](https://nodejs.org/en/download)
- [Dart Sass](https://github.com/sass/dart-sass?tab=readme-ov-file#using-dart-sass)
- [Asciidoctor](https://asciidoctor.org/)
- [Pandoc](https://pandoc.org/installing.html)
- [reStructuredText](https://docutils.sourceforge.io/rst.html)

If you want to skip the AsciiDoc, Pandoc, and reStructuredText tests, set the `environment` as shown below:

```text
hugo server --environment skip-external-renderers
```

## Installing Asciidoctor, Pandoc, and reStructuredText on Linux

### Asciidoctor

Install:

```text
sudo apt install ruby
gem install --user-install asciidoctor
```

Add this section to `$HOME/.bashrc`:

```text
# Set PATH to include $HOME/.local/share/gem/ruby/3.2.0/bin if it exists.
if [ -d "$HOME/.local/share/gem/ruby/3.2.0/bin" ];then
  PATH="$HOME/.local/share/gem/ruby/3.2.0/bin:$PATH"
fi
```

Test:

```text
source $HOME/.bashrc
asciidoctor --version
```

### Pandoc

Install: `sudo apt install pandoc`

Test: `pandoc --version`

### reStructuredText

Install: `sudo apt install python3-docutils`

Test: `rst2html --version`

## Security

> [!NOTE]
> The Hugo snap package and the veriphor/hugo Docker image include the required security settings. No further action is required.

Hugo's built-in security policy, which restricts access to `os/exec`, remote communication, and similar operations, is configured via allow lists. By default, access is restricted. If a build attempts to use a feature not included in the allow list, it will fail, providing a detailed message.

To render AsciiDoc, Pandoc, and reStructuredText content you must add their executables to the allow list.

You can do this in your site configuration:

```toml
[security.exec]
allow = ['^(dart-)?sass$','^git$','^go$','^npx$','^postcss$','^tailwindcss$','^asciidoctor$','^pandoc$','^rst2html$']
```

Or with an environment variable:

```text
export HUGO_SECURITY_EXEC_ALLOW="^((dart-)?sass|git|go|npx|postcss|tailwindcss|asciidoctor|pandoc|rst2html)$"
```

## Building the site

To build and serve the site:

```text
git clone https://github.com/jmooring/hugo-feature-test
cd hugo-feature-test
npm ci
hugo server
```

As noted above, if you want to skip the AsciiDoc, Pandoc, and reStructuredText tests, set the `environment` as shown below:

```text
hugo server --environment skip-external-renderers
```

## CI/CD Testing

Automated builds for this site are handled by both GitHub Pages and GitLab Pages, utilizing the veriphor/hugo Docker image.

Workflow files:

- [GitHub Pages](https://github.com/jmooring/hugo-feature-test/blob/main/.github/workflows/hugo.yaml)
- [GitLab Pages](https://github.com/jmooring/hugo-feature-test/blob/main/.gitlab-ci.yml)

Live sites:

- <https://jmooring.github.io/hugo-feature-test/>
- <https://jmooring.gitlab.io/hugo-feature-test/>
