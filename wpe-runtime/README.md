Build:

```
ostree  init --mode=archive-z2 --repo=/path/to/repo
flatpak-builder --force-clean --ccache --require-changes --repo=/path/to/repo --arch=x86_64 --subject="org.wpe flatpak runtime, `date`" sdk org.wpe.Sdk.json
```

Enable local remote:

```
flatpak --user remote-add --no-gpg-verify --if-not-exists wpe /path/to/wpe-repo # can only be run once
```

