Build:

```
export FLATPAK_BUILD=/path/to/flatpak-build
export WPE_BUILD=/path/to/wpe-source
export REPO=/path/to/wpe-repo

flatpak build-init $FLATPAK_BUILD org.wpe.WPENightly org.wpe.Sdk org.wpe.Platform 0.1

flatpak build $FLATPAK_BUILD cmake -DPORT=WPE -DCMAKE_INSTALL_PREFIX=/app -DCMAKE_BUILD_TYPE=Release -DCMAKE_C_FLAGS_RELEASE="-O2 -DNDEBUG -DMESA_EGL_NO_X11_HEADERS" -DCMAKE_CXX_FLAGS_RELEASE="-O2 -DNDEBUG -DMESA_EGL_NO_X11_HEADERS" $WPE_BUILD
flatpak build $FLATPAK_BUILD make -C $WPE_BUILD -j7 
flatpak build $FLATPAK_BUILD make -C $WPE_BUILD install

cp manifest.in $FLATPAK_BUILD
flatpak build-finish $FLATPAK_BUILD
flatpak build-export $REPO $FLATPAK_BUILD
```

Install after initial export:
```
flatpak --user remote-add --no-gpg-verify --if-not-exists wpe /path/to/wpe-repo # can only be run once
flatpak --user install wpe org.wpe.WPENightly
```

Update after later exports:
```
flatpak update org.wpe.WPENightly
```

Run:
```
weston # run on the host system
flatpak run --env=WAYLAND_DISPLAY=wayland-0 org.wpe.WPENightly
```
