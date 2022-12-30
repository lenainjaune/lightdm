RO en attente de la fin de migration









































# lightdm

Tout ce qu'il faut savoir sur lightdm

# Exécuter un script avant/après le login
[Source](https://unix.stackexchange.com/questions/450835/how-to-execute-command-before-user-login-on-linux/450836#450836)
```sh
user@host:~$ cat /etc/lightdm/lightdm.conf 
[Seat:*]
# BEFORE login
greeter-setup-script=/path/to/script
# AFTER login
session-setup-script=/path/to/script
...
```
Pour vérifier que le script s'exécute bien pendant l'ouverture de session :
```sh
user@host:~$ tail -f /var/log/lightdm/lightdm.log
```

# Autologin
```sh
user@host:~$ cat /etc/lightdm/lightdm.conf
...
[Seat:*]
...
autologin-user=<user>
autologin-user-timeout=0
...
```
Nota : quand un utilisateur occasionnel utilisera l'autologin, le porte clé n'étant pas déverrouillé, lorsqu'il lancera certaines applications "à risque" (telle remmina), il aura une demande de mot de passe (voir keyring disable)

# Liste d'utilisateurs au login
Plus convivial (pas de login à se souvenir), moins sécurisé (on connaît déjà les noms qui sont associés aux logins)
```sh
user@host:~$ cat /etc/lightdm/lightdm.conf
[Seat:*]
greeter-hide-users=false
...
```

# Numlock avant login
[source](https://superuser.com/questions/1282192/debian-9-stretch-xfce4-possible-screen-lock-numlock-bug/1331883#1331883)

Testé sous Debian Stretch, Buster, Bullseye avec succès !
```sh
user@host:~$ apt install numlockx
user@host:~$ cat /etc/lightdm/lightdm.conf
[Seat:*]
greeter-setup-script=/usr/bin/numlockx on
...
```
Attention : ça ne concerne que le login et PAS après

# touchpad tapping enabled

```sh
cat << EOF > /etc/X11/xorg.conf.d/40-libinput.conf
Section "InputClass"
        Identifier "libinput touchpad catchall"
        MatchIsTouchpad "on"
        MatchDevicePath "/dev/input/event*"
        Driver "libinput"
        Option "Tapping" "on"
EndSection
EOF
```
[source](https://wiki.debian.org/SynapticsTouchpad#Debian_9_.22Stretch.22)

