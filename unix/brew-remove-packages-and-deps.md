brew remove packages and deps
=============================


```bash
unbrew () {
    local formula
    for formula in "$@"; do
        brew deps "$formula" |
        xargs brew uninstall --ignore-dependencies --force
        brew uninstall --force "$formula"
    done
    brew missing | cut -f2 -d: | sort -u | xargs brew install
}
```

[Source](https://stackoverflow.com/a/52356599)
