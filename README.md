# lightdm

Tout ce qu'il faut savoir sur lightdm

# Exécuter un script avant/après le login
```sh
user@host:~$ sudo cat /etc/lightdm/lightdm.conf.d/minidlna.conf 
[Seat:*]
# https://unix.stackexchange.com/questions/450835/how-to-execute-command-before-user-login-on-linux/450836#450836
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
# TODO tester : Liste au démarrage
```sh
user@host:~$ sudo cat /etc/lightdm/lightdm.conf
[Seat:*]
greeter-hide-users=false
...
```
