# tor

Buscando la privacidad maxima y con la idea de garantizar una buena conexion a
internet  para personas que viajan, he decidio instalar `tor` e ir documentado
todo el proceso

## Instalacion

Para `fedora linux` sirve con instalar:

### Configuracion para usar desde terminal

#### Instalacion del paquete

```bash
sudo dnf install tor -y # que incluye la dependencia torsocks
```

Esta instalacion crea un usuario y grupo: `toranon` con uid y gid *969*

#### configuracion de `/etc/yum.repos.d/tor.repo`

```yml
[tor]
name=Tor for Fedora $releasever - $basearch
baseurl=https://rpm.torproject.org/fedora/$releasever/$basearch
enabled=1
gpgcheck=1
gpgkey=https://rpm.torproject.org/fedora/public_gpg.key
cost=100
```

#### Inicio del servicio

```txt
❯ sudo systemctl enable --now tor
Created symlink '/etc/systemd/system/multi-user.target.wants/tor.service' → '/usr/lib/systemd/system/tor.service'.
❯ torsocks curl -s https://check.torproject.org/api/ip | jq .

{
  "IsTor": true,
  "IP": "185.220.101.179"
}
```

Tras configurar *bridges*:

```txt
❯ sudo -e /etc/tor/torrc
❯ sudo systemctl restart tor
```

#### Instalacion de bridge

Por un lado, se puede configurar desde el navegador y parece bastante seguro.
Mientras se puede configurar para que el propio tor use los servicios de tor
con bridge. Esto incluira comando desde la terminal:

```txt
UseBridges 1
Bridge obfs4 49.12.247.119:23689 F59asdfgqwegaAasdgB3A9022EE8380F3CB09599 cert=d6hvXm+lZrrlDOy9kxnpGBgDplt6QTXgñaslkdghqoiwefnoiwefmñoi234VmiNvNb3zYQ iat-mode=0
Bridge obfs4 140.238.197.121:62812 388992800061234985jqrwiejf834jtp98324f23 cert=5hB813425tjp3984fj348·&"·4fowefwjUsm97Xf8eakEwdm3W781HJs8UDaAEwPicPUBA iat-mode=0
```

### Configuracion para usar desde el navegador de tor

#### Intalacion de paquetes

El paquete previamente instalado `dnf install tor`, contiene el binario de:

```bash
torbrowser-launcher # comando para iniciar el navegador
```

#### Configuracion

Este navegador usa de base firefox y le añade las funciones de la red de *tor*.

La configuración de las busquedas onion, la union a la red y los bridges son
muy sencillas y seguramente vayan cambiando.

En general, dirigete a `Settings > Connection`, o desde el inicio a veces
dando a la opocion de `Configure conecction`.
