# rEFInd


rEFInd és un gestor d'arrencada (boot manager) UEFI que permet arrencar diferents sistemes. Amb aquest gestor instal·lat a la partició UEFI podem fer que el nostre equip pugui arrencar la majoria de sistemes operatius.

La documentació d'aquesta eina, junt amb una molt bona explicació de com funciona EFI/UEFI la teniu en aquesta pàgina totalment recomanada: [https://www.rodsbooks.com/refind/](https://www.rodsbooks.com/refind/) https://www.rodsbooks.com/refind/ 


Aquesta eina no s'encarrega de iniciar el SO, ja que això ho delega en el carregador del pròpi sistema, ja que tots els SO que suporten EFI (actualment pràcticament tots) tenen un boot loader pròpi.


Si treballeu amb Debian/Ubuntu podeu descarregar un paquet .deb en aquesta adreça: https://sourceforge.net/projects/refind/[https://sourceforge.net/projects/refind/](https://sourceforge.net/projects/refind/) 

Si feu servir Windows cal fer la instal·lació de forma manual, el que no resulta gaire difícil.

## Instal·lar rEFInd a Windows

La documentació que podeu trobar a l'anterior pàgina sobre Windows presenta diferents alternatives, algunes no gaire senzilles. Hi ha una eina que simplifica molt el procés d'instal·lació, s'anomena "DiskGenius" i la podeu descarregar en aquesta pàgina: [https://www.diskgenius.com/](https://www.diskgenius.com/) https://www.diskgenius.com/

Aquesta eina ens permetrà accedir a la partició ESP on es desa la informació EFI de arrencada. Aquesta partició té un sistema de fitxers FAT32, però Windows la oculta i no hi deixa accedir. També ens permetrà afegir una entrada al menú d'arrencada UEFI, o modificar el bootmanager de Windows per tal que sempre aparegui rEFInd i que sigui aquest el que ens carregui qualsevol SO.


Necessitem els binaris de rEFInd per copiar-los a la partició EFI. Us els podeu descarregar des de sourceforge: [https://sourceforge.net/projects/refind/files/0.12.0/refind-bin-0.12.0.zip/download](https://sourceforge.net/projects/refind/files/0.12.0/refind-bin-0.12.0.zip/download) 


Els dos passos que cal fer són senzills i els podem fer amb la eina DiskGenius.

Copiar la carpeta refind amb totes les seves subcarpetes dins la carpeta EFI que hi ha a la partició ESP.

Afegir una entrada a la NVRAM per que aparegui la opció de rEFInd. Es pot fer des del menú "Tools/Set UEFI BIOS bot entries"



## Arrencar des d'una shell EFI

Primer cal veure quins discos/dispositius troba. Això ho podem veure amb la comanda `map` que ens dirà els elements trobats.

Després hem de seleccionar el dispositiu EFI des d'on volguem arrencar i anar a la carpeta on es trobi l'arxiu .efi a executar per arrencar. 

Un exemple de seqüència de comandes podria ser:

```
map
blk0:
cd EFI\BOOT
bootx64.efi
```






