# rEFInd


rEFInd és un gestor d'arrencada (boot manager) UEFI que permet arrencar diferents sistemes. Amb aquest gestor instal·lat a la partició UEFI podem fer que el nostre equip pugui arrencar la majoria de sistemes operatius.

La documentació d'aquesta eina, junt amb una molt bona explicació de com funciona EFI/UEFI la teniu en aquesta pàgina totalment recomanada: [https://www.rodsbooks.com/refind/](https://www.rodsbooks.com/refind/)


Aquesta eina no s'encarrega de iniciar el SO, ja que això ho delega en el carregador del pròpi sistema, ja que tots els SO que suporten EFI (actualment pràcticament tots) tenen un boot loader pròpi.


Si treballeu amb Debian/Ubuntu podeu descarregar un paquet .deb en aquesta adreça: https://sourceforge.net/projects/refind/[https://sourceforge.net/projects/refind/](https://sourceforge.net/projects/refind/) 

Si feu servir Windows cal fer la instal·lació de forma manual, el que no resulta gaire difícil.

## Instal·lar rEFInd a Windows

La documentació que podeu trobar a l'anterior pàgina sobre Windows presenta diferents alternatives, algunes no gaire senzilles. Hi ha una eina que simplifica molt el procés d'instal·lació, s'anomena "DiskGenius" i la podeu descarregar en aquesta pàgina: [https://www.diskgenius.com/](https://www.diskgenius.com/) 

Aquesta eina ens permetrà accedir a la partició ESP on es desa la informació EFI de arrencada. Aquesta partició té un sistema de fitxers FAT32, però Windows la oculta i no hi deixa accedir. També ens permetrà afegir una entrada al menú d'arrencada UEFI, o modificar el bootmanager de Windows per tal que sempre aparegui rEFInd i que sigui aquest el que ens carregui qualsevol SO.


Necessitem els binaris de rEFInd per copiar-los a la partició EFI. Us els podeu descarregar des de sourceforge: [https://sourceforge.net/projects/refind/files/0.12.0/refind-bin-0.12.0.zip/download](https://sourceforge.net/projects/refind/files/0.12.0/refind-bin-0.12.0.zip/download) 



En aquest repositori podeu trobar un arxiu amb la carpeta refind i les eines necessàries únicament per una arquitectura AMD64/x64.



Els dos passos que cal fer són senzills i els podem fer amb la eina DiskGenius.

- Copiar la carpeta refind amb totes les seves subcarpetes dins la carpeta EFI que hi ha a la partició ESP. Per fer-ho cal anar a la carpeta on vulguem copiar els arxius i amb el botó dret escollir "Copy Files to Current Partition"

![Copy Files](https://i.imgur.com/xFGXo9L.png) 

Aquesta eina no permet copiar una carpeta i totes les seves subcarpetes, així que haurem de crear les carpetes a mà i copiar els arxius a cada carpeta. Si que ens permet seleccionar un conjunt de fitxers. Per fer la còpia cal abans haver creat les carpetes a la partició de destí.


![rEFInd](https://i.imgur.com/OZigkpy.png) 


Una alternativa és instal·lar el programa [explorer++](https://explorerplusplus.com/) i executar-lo com administrador. Amb aquest programa podrem accedir a la partició ESP. Per tal de poder-la utilitzar amb aquest programa primer hem de fer click a la opció "Hide/unhide" dins DiskGenius fer apply per amagar la partició, i després tornar a fer el mateix per mostrar-la i que assigni una lletra al volum.

![DiskGenius Hide Partition](https://i.imgur.com/NuNC7wb.png) 



- Afegir una entrada a la NVRAM per que aparegui la opció de rEFInd. Es pot fer des del menú "Tools/Set UEFI BIOS bot entries"

![rEFInd Boot List](https://i.imgur.com/zDd4sHZ.png) 




## Arrencar des d'una shell EFI

De vegades UEFI no arrenca i mostra una shell on podem intentar arrencar manualment. Si us passa el que cal fer és anar a la partició des d'on voleu arrencar i executar un arxiu amb extensió `.efi` que és el que s'encarregarà d'iniciar el SO. Aquestos arxius acostumen a estar dins una carpeta anomenada EFI en una partició FAT32 petita, on només hi ha els arxius per iniciar el SO.

Primer cal veure quins discos/dispositius troba. Això ho podem veure amb la comanda `map` que ens dirà els elements trobats.

Després hem de seleccionar el dispositiu EFI des d'on volguem arrencar i anar a la carpeta on es trobi l'arxiu .efi a executar per arrencar. 

Un exemple de seqüència de comandes podria ser:

```
map
blk0:
cd EFI\BOOT
bootx64.efi
```


## Links a les eines emprades


- Eina DiskGenius per gestionar l'arrencada UEFI i treballar amb la partició ESP que Windows amaga.
[https://www.diskgenius.com/](https://www.diskgenius.com/)


- Eina Explorer++ que si executem com administrador ens permetrà copiar carpetes dins la partició ESP. 
[https://explorerplusplus.com/](https://explorerplusplus.com/) 


- Binaris refind per diferents plataformes. Cal copiar-los a una carpeta anomenada `refind`dins la partició EFI.
[https://sourceforge.net/projects/refind/files/0.12.0/refind-bin-0.12.0.zip/download](https://sourceforge.net/projects/refind/files/0.12.0/refind-bin-0.12.0.zip/download) 



- Paquet debian per a instal·lar refind a Ubuntu.
[https://sourceforge.net/projects/refind/](https://sourceforge.net/projects/refind/) 
