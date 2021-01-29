# lightdm

Tout ce qu'il faut savoir sur lightdm

# Exécuter un script avant/après le login
[Source](https://unix.stackexchange.com/questions/450835/how-to-execute-command-before-user-login-on-linux/450836#450836)
```sh
user@host:~$ sudo cat /etc/lightdm/lightdm.conf.d/minidlna.conf 
[Seat:*]
# BEFORE login
greeter-setup-script=/data/scripts/run_minidlna.sh
# AFTER login
# session-setup-script=/data/scripts/run_minidlna.sh
```

# autologin
```sh
user@host:~$ sudo cat /etc/lightdm/lightdm.conf
[Seat:*]
...
autologin-user=<user>
autologin-user-timeout=0
...
```
Nota : quand un utilisateur occasionnel utilisera l'autologin, le porte clé n'étant pas déverrouillé, lorsqu'il lancera certaines applications "à risque" (telle remmina), il aura une demande de mot de passe (voir keyring disable)

# Liste au démarrage
Plus convivial (pas de login à se souvenir), moins sécurisé (on connaît déjà les noms qui sont associés aux logins)
```sh
user@host:~$ sudo cat /etc/lightdm/lightdm.conf
[Seat:*]
greeter-hide-users=false
...
```
