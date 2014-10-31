# Script para activar/desactivar políticas asociadas a VPNs

## Uso

``` sh
fg_vpn <VPN> <ACTIVACION> <KEY>
```

Donde:

* VPN: Identificador de la VPN
* ACTIVACION: ON o OFF
* KEY: Llave de cifrado para la password de acceso al FortiGate

## Ficheros de configuración

* VPN ID: Fichero en texto plano que contiene los números de política del FortiGate que se va a activar/desactivar.

> Por ejemplo, para la *VPN UNO* (VPN_UNO):
>  
>  345    
>  543

* PASSWORD CIFRADA: Fichero con la password cifrada `fgpd.enc`.

Se guardan en el subdirectorio `etc` ubicado en el directorio desde el que se lanza el script.

## Cifrado de passwords

Para cifrar la password, guardada en texto plano en un fichero (fgpd.dec):

``` sh
$ openssl des3 -salt -in fgpd.dec -out fgpd.enc
enter des-ede3-cbc encryption password:
Verifying - enter des-ede3-cbc encryption password:
```

La *KEY* que pasamos al script es la `des-ede3-cbc encryption password` que se solicita en el comando anterior.