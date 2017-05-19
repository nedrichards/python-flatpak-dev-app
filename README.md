# python-flatpak-dev-app
Command line flatpak that gives the user access to python dev tools. This is likely solely of use to people who use Linux computers with minimal read only root filesystems and run all applications inside flatpak containers, such as users of [https://endlessos.com/](Endless OS).

Instructions:
-------------

(1) Install the flatpak repository for GNOME:
```
flatpak remote-add --from gnome https://sdk.gnome.org/gnome.flatpakrepo

```
(2) Install the required runtimes
```
  flatpak install gnome org.freedesktop.Sdk
```
(3) Build the python dev app from this directory:
```
flatpak-builder --force-clean --ccache --require-changes --repo=repo app com.github.nedrichards.PythonDevApp.json
```
(4) Add a remote to your local repo and install it:
```
  flatpak --user remote-add --no-gpg-verify python-repo /path/to/your/flatpak/repo
  flatpak --user install python-repo com.github.nedrichards.PythonDevApp
```
(5) Run the DevApp:
```
  flatpak run com.github.nedrichards.PythonDevApp
```

Note that if you do further changes in the `appdir` (e.g. to the metadata), you'll need to re-publish it in your local repo and update before running it again:
```
  flatpak build-export /path/to/your/flatpak/repo /path/to/flatpak/appdir
  flatpak --user update com.github.nedrichards.PythonDevApp
```

Last, you can bundle it to a file with the `build-bundle` subcommand:
```
  flatpak build-bundle /path/to/your/flatpak/repo com.github.nedrichards.PythonDevApp.flatpak com.github.nedrichards.PythonDevApp
```
