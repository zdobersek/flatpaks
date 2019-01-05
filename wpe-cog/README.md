

Build:
```
flatpak-builder --user --install-deps-from=wpe build-dir org.wpe.Cog.yaml
```

Run:
```
flatpak-builder --run build-dir org.wpe.Cog.yaml cog -P fdo https://igalia.com
```

GStreamer WPE plugin:
```
flatpak-builder --run build-dir org.wpe.Cog.yaml gst-play-1.0 wpe://https://igalia.com --videosink gtkglsink
```
