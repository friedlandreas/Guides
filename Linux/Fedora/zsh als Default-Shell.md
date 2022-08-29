Unter Fedora ist nachwievor (Fedora 36) die Bash die Standard-Shell. Ich bin aber von Arch und von MacOS die zsh schon so gewohnt das ich die natürlich auch unter Fedora haben will :-)

### zsh installieren

Wir installieren alle nötigen Pakete (auch schon für oh my zsh):

```console
dnf install zsh util-linux-user powerline-fonts
```
### oh my zsh installieren

Jetzt gehen wir in die zsh

```console
zsh
```

und installieren oh my zsh
```console
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Normal wird jetzt durch chsh die Shell durch das Script automatisch gesetzt - falls nicht kann das per **chsh -s $(which zsh)** erledigt werden 

### Abmelden und neu anmelden

Jetzt neu ab- und anmelden -> dann sollte die zsh die Standard-Shell sein.

## oh my zsh konfigurieren

Jetzt kann oh my zsh konfiguriert werden.

Infos dazu: https://ohmyz.sh/
