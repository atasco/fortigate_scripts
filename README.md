# Expect scripts para automatizar diferentes tareas en FortiOS

## FG_VPN: Activar/desactivar políticas asociadas a VPNs en FortiGate

### Uso

``` sh
fg_vpn <VPN> <ACTIVACION> <KEY>
```

Donde:

* VPN: Identificador de la VPN
* ACTIVACION: ON o OFF
* KEY: Llave de cifrado para la password de acceso al FortiGate

### Configuración

Ajustar los siguientes parámetros:

* username: Cuenta de usuario con permisos de administración (por defecto *admin*). 
* hostname: Nombre de host o IP del FortiGate (por defecto *fortigate*).
* fgpd: Nombre del fichero con la password cifrada del usuario (por defecto *fgpd.enc*).
* cfg_dir: Directorio donde se encuentran los ficheros de configuración (por defecto *./etc*).
* log_dir: Directorio donde se guardarán los ficheros de log (por defecto *./logs*).
* log_name: Nombre del fichero de log (por defecto *fg_vpn.log*).
* exp_internal: Activación/desactivación de debugging (0=no 1=si).
* log_user: Activar/desactivar la salida del proceso de spawn (0=no 1=si).

#### Ficheros

Se guardan en el subdirectorio `etc` ubicado en el directorio desde el que se lanza el script. Son los siguientes:

* VPN ID: Fichero en texto plano que contiene los números de política del FortiGate que se va a activar/desactivar.

> Por ejemplo, para la *VPN UNO* (VPN_UNO):
>  
>  345    
>  543

* PASSWORD CIFRADA: Fichero con la password cifrada `fgpd.enc`.

### Cifrado de passwords

Para cifrar la password, guardada en texto plano en un fichero (fgpd.dec):

``` sh
$ openssl des3 -salt -in fgpd.dec -out fgpd.enc
enter des-ede3-cbc encryption password:
Verifying - enter des-ede3-cbc encryption password:
```

La *KEY* que pasamos al script es la `des-ede3-cbc encryption password` que se solicita en el comando anterior.

### Rotado de logs

Para evitar la acumulación de logs se puede hacer uso *logrotate*:

``` sh
vi /etc/logrotate.d/fg_vpn
```

con el contenido:

><DIRECTORIO_LOGS>/*log {    
>    rotate 14    
>    daily    
>    compress    
>    create 0755 root root    
>}