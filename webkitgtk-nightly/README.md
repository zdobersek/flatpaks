```
export FLATPAK_BUILD=/path/to/flatpak-build
export WEBKITGTK_BUILD=/path/to/webkitgtk-source
export REPO=/path/to/webkitgtk-repo

flatpak build-init FLATPAK_BUILD org.webkitgtk.WebKitGTKNightly org.webkitgtk.Sdk org.webkitgtk.Platform 0.1

flatpak build $FLATPAK_BUILD cmake -DPORT=GTK -DCMAKE_INSTALL_PREFIX=/app -DCMAKE_BUILD_TYPE=Release -DCMAKE_C_FLAGS_RELEASE="-O2 -DNDEBUG" -DCMAKE_CXX_FLAGS_RELEASE="-O2 -DNDEBUG" -DENABLE_MINIBROWSER=ON -DENABLE_INTROSPECTION=OFF $WEBKITGTK_BUILD
flatpak build $FLATPAK_BUILD make -C $WEBKITGTK_BUILD -j7 
flatpak build $FLATPAK_BUILD make -C $WEBKITGTK_BUILD install

cp manifest.in $FLATPAK_BUILD
flatpak build-finish $FLATPAK_BUILD
flatpak build-export $REPO $FLATPAK_BUILD
```

Install after initial export:
```
flatpak --user remote-add --no-gpg-verify --if-not-exists webkitgtk /path/to/webkitgtk-repo # can only be run once
flatpak --user install webkitgtk org.webkitgtk.WebKitGTKNightly
```

Update after later exports:
```
flatpak update org.webkitgtk.WebKitGTKNightly
```

Run:
```
flatpak run org.webkitgtk.WebKitGTKNightly
```
