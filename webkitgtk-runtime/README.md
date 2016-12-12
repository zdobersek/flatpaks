```
ostree  init --mode=archive-z2 --repo=/path/to/repo
flatpak-builder --force-clean --ccache --require-changes --repo=/path/to/repo --arch=x86_64 --subject="org.webkitgtk flatpak runtime, `date`" sdk org.webkitgtk.Sdk.json
```
