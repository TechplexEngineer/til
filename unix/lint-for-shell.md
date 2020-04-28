Lint for Shell Scripts
======================

[ShellCheck](https://www.shellcheck.net/) a static analysis tool for shell scripts

Writing good code is hard, even harder when the language actively tries to screw you over.

### lint all shell scripts in repo
```yaml
test:
    image: koalaman/shellcheck-alpine:latest
    stage: test
    before_script:
    - apk update
    - apk add git
    script:
    - git ls-files --exclude='*.sh' --ignored | xargs shellcheck
```
[Src](https://github.com/koalaman/shellcheck/wiki/GitLab-CI)

## Package for Sublime
```
apt-get install shellcheck
package control install package SublimeLinter-shellcheck
`
https://packagecontrol.io/packages/SublimeLinter-shellcheck
