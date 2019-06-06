---
title: 'Configurar la instancia de clúster de conmutación por error iSCSI almacenamiento: SQL Server en Linux | Microsoft Docs'
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 9a64460b2d04f1d6957a181657af7255d64cc829
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705068"
---
# <a name="configure-failover-cluster-instance---iscsi---sql-server-on-linux"></a>Configurar la instancia de clúster de conmutación por error - iSCSI: SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se explica cómo configurar el almacenamiento iSCSI para una instancia de clúster de conmutación por error (FCI) en Linux. 

## <a name="configure-iscsi"></a>Configuración de iSCSI 
iSCSI utiliza redes para presentar los discos de un servidor conocido como un destino para los servidores. Los servidores de conectarse al destino iSCSI requieren que un iniciador iSCSI está configurado. Los discos en el destino tienen permisos explícitos para que solo los iniciadores que se deben poder tener acceso a ellos pueden hacerlo. El propio destino debe ser de alta disponibilidad y confiabilidad.

### <a name="important-iscsi-target-information"></a>Información de destino iSCSI importante
Aunque esta sección no explica cómo configurar un destino iSCSI, ya que es específico del tipo de origen que se va a usar, asegúrese de que se ha configurado la seguridad de los discos que se usará en los nodos del clúster.  

El destino nunca debe configurarse en cualquiera de los nodos FCI si usa un destino iSCSI basadas en Linux. Rendimiento y disponibilidad, las redes iSCSI deben ser independientes de las utilizadas por el tráfico de red regular en el origen y los servidores de cliente. Las redes usadas para iSCSI deben ser rápidas. Recuerde esa red consumen algunos ancho de banda de procesador, por lo tanto, planee en consecuencia si usa un servidor normal.
Es lo más importante para asegurarse de completado en el destino es que los discos que se crean se asignan los permisos adecuados para que sólo los servidores que participan en la FCI tienen acceso a ellos. A continuación se muestra un ejemplo en el destino de iSCSI de Microsoft donde linuxnodes1 es el nombre creado y, en este caso, se asignan las direcciones IP de los nodos para que aparezca NewFCIDisk1.vhdx a ellos.

![Iniciador][1]

### <a name="instructions"></a>Instructions

Esta sección explica cómo configurar un iniciador iSCSI en los servidores que servirán como nodos en la FCI. Las instrucciones deberían funcionar tal cual en Ubuntu y RHEL.

Para obtener más información sobre el iniciador iSCSI para las distribuciones admitidas, consulte los siguientes vínculos:
- [Red Hat](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/iscsi-api.html)
- [SUSE](https://www.suse.com/documentation/sles11/stor_admin/data/sec_inst_system_iscsi_initiator.html) 
- [Ubuntu](https://help.ubuntu.com/lts/serverguide/iscsi-initiator.html)

1.  Elija uno de los servidores que participarán en la configuración de FCI. No importa cuál de ellos. iSCSI debe estar en una red dedicada, por lo que configure iSCSI para reconocer y usar esa red. Ejecute `sudo iscsiadm -m iface -I <iSCSIIfaceName> -o new` donde `<iSCSIIfaceName>` es el nombre descriptivo único para la red. En el ejemplo siguiente se usa `iSCSINIC`:
   
    ```bash
    sudo iscsiadm -m iface -I iSCSINIC -o new
    ```
    ![7-setiscsinetwork][6]
 
2.  Editar `/var/lib/iscsi/ifaces/iSCSIIfaceName`. Asegúrese de que tiene los siguientes valores rellenados completamente:

    - iface.net_ifacename es el nombre de la tarjeta de red, tal como se muestra en el sistema operativo.
    - iface.hwaddress es la dirección MAC del nombre único que se creará para esta interfaz siguiente.
    - iface.ipaddress
    - iface.subnet_Mask 

    Vea el ejemplo siguiente:

    ![iSCSITargetSettings][2]

3.  Encontrar el destino iSCSI.

    ```bash
    sudo iscsiadm -m discovery -t sendtargets -I <iSCSINetName> -p <TargetIPAddress>:<TargetPort>
    ```

     \<iSCSINetName > es el nombre único y descriptivo para la red, \<TargetIPAddress > es la dirección IP del destino iSCSI, y \<TargetPort > es el puerto de destino iSCSI. 

    ![iSCSITargetResults][3]

 
4.  Inicie sesión en el destino

    ```bash
    sudo iscsiadm -m node -I <iSCSIIfaceName> -p TargetIPAddress -l
    ```

    \<iSCSIIfaceName > es el nombre único y descriptivo para la red y \<TargetIPAddress > es la dirección IP del destino iSCSI.

    ![iSCSITargetLogin][4]

5.  Compruebe que hay una conexión con el destino iSCSI.

    ```bash
    sudo iscsiadm -m session
    ```

    ![iSCSIVerify][5]

 
6.  Comprobación de discos iSCSI conectados

    ```bash
    sudo grep "Attached SCSI" /var/log/messages
    ```
    ![30-iSCSIattachedDisks][7]

7.  Crear un volumen físico en el disco iSCSI.

    ```bash
    sudo pvcreate /dev/<devicename>
    ```

    \<DeviceName > es el nombre del dispositivo desde el paso anterior. 

 
8.  Crear un grupo de volúmenes en el disco iSCSI. Discos asignados a un único grupo de volúmenes se ven como un grupo o una colección. 

    ```bash
    sudo vgcreate <VolumeGroupName> /dev/devicename
    ```

    \<VolumeGroupName > es el nombre del grupo de volúmenes y \<devicename > es el nombre del dispositivo del paso 6. 
 
9.  Crear y comprobar el volumen del disco lógico.

    ```bash
    sudo lvcreate -Lsize -n <LogicalVolumeName> <VolumeGroupName>
    ```
    
    \<tamaño > es el tamaño del volumen para crear y puede especificarse con G (gigabytes), T (terabytes), etc.,\<LogicalVolumeName > es el nombre del volumen lógico, y \<VolumeGroupName > es el nombre del grupo de volúmenes de la paso anterior. 

    El ejemplo siguiente crea un volumen de 25GB.
 
    ![Create25GBVol][10]

10. Ejecutar `sudo lvs` para ver el LVM que se creó.
 
11. Formatee el volumen lógico con un sistema de archivos admitido. Para EXT4, use el ejemplo siguiente:

    ```bash
    sudo mkfs.ext4 /dev/<VolumeGroupName>/<LogicalVolumeName>
    ```

    \<VolumeGroupName > es el nombre del grupo de volúmenes en el paso anterior. \<LogicalVolumeName > es el nombre del volumen lógico en el paso anterior.  

12. Para las bases de datos del sistema o cualquier elemento almacenado en la ubicación de datos de forma predeterminada, siga estos pasos. En caso contrario, vaya al paso 13.

   *    Asegúrese de que SQL Server se ha detenido en el servidor que está trabajando.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    Conmutador totalmente que será el superusuario. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    sudo -i
    ```

   *    Cambiar a ser el usuario de mssql. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    su mssql
    ```

   *    Cree un directorio temporal para almacenar los datos de SQL Server y los archivos de registro. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > es el nombre de la carpeta. El ejemplo siguiente crea una carpeta denominada /var/opt/mssql/TempDir.

    ```bash
    mkdir /var/opt/mssql/TempDir
    ```
    
   *    Copie los archivos de registro y datos de SQL Server en el directorio temporal. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > es el nombre de la carpeta en el paso anterior.
    
   *    Compruebe que los archivos están en el directorio.

    ```bash
    ls \<TempDir>
    ```
    \<TempDir > es el nombre de la carpeta del paso d.

   *    Elimine los archivos del directorio de datos de SQL Server existente. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   *    Compruebe que se han eliminado los archivos. La figura siguiente muestra un ejemplo de la secuencia completa de c a través de h.

    ```bash
    ls /var/opt/mssql/data
    ```

    ![45-CopyMove][8]
 
   *    Tipo `exit` para volver al usuario raíz.

   *    Monte el volumen lógico de iSCSI en la carpeta de datos de SQL Server. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> /var/opt/mssql/data
    ``` 

    \<VolumeGroupName > es el nombre del grupo de volúmenes y \<LogicalVolumeName > es el nombre del volumen lógico que se creó. La sintaxis de ejemplo siguiente coincide con el grupo de volúmenes y el volumen lógico del comando anterior.

    ```bash
    mount /dev/FCIDataVG1/FCIDataLV1 /var/opt/mssql/data
    ``` 

   *    Cambiar el propietario del montaje a mssql. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    chown mssql /var/opt/mssql/data
    ```

   *    Cambiar la propiedad del grupo del montaje a mssql. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    chgrp mssql /var/opt/mssql/data
    ``` 

   *    Cambie al usuario mssql. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    su mssql
    ``` 

   *    Copie los archivos desde el directorio temporal de /var/opt/mssql/data. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    cp /var/opt/mssql/TempDir/* /var/opt/mssql/data
    ``` 

   *    Compruebe que existen los archivos.

    ```bash
    ls /var/opt/mssql/data
    ``` 
 
   *    Escriba `exit` a no ser mssql.
    
   *    Escriba `exit` a no ser raíz.

   *    Inicie SQL Server. Si todo lo que se copió correctamente y seguridad aplicada correctamente, SQL Server debe aparecer como iniciado.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ``` 
 
   *    Detener SQL Server y comprobar que es apagar.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ``` 

13. Para elementos distintos de las bases de datos del sistema, como las bases de datos de usuario o las copias de seguridad, siga estos pasos. Si solo usa la ubicación predeterminada, vaya al paso 14.

   *    Conmutador que será el superusuario. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    sudo -i
    ```

   *    Cree una carpeta que se usará en SQL Server. 

    ```bash
    mkdir <FolderName>
    ```

    \<Nombre de carpeta > es el nombre de la carpeta. Ruta de acceso completa de la carpeta debe especificarse si no están en la ubicación correcta. El ejemplo siguiente crea una carpeta denominada /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    Monte el volumen lógico de iSCSI en la carpeta que creó en el paso anterior. No recibirá ninguna confirmación si se realiza correctamente.
    
    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > es el nombre del grupo de volúmenes, \<LogicalVolumeName > es el nombre del volumen lógico que se creó, y \<nombreDeCarpeta > es el nombre de la carpeta. Sintaxis de ejemplo se muestran a continuación.

    ```bash
    mount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

   *    Cambiar la propiedad de la carpeta creada para mssql. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    chown mssql <FolderName>
    ```

    \<Nombre de carpeta > es el nombre de la carpeta que se creó. A continuación, se muestra un ejemplo.

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```
  
   *    Cambiar el grupo de la carpeta creada para mssql. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    chown mssql <FolderName>
    ```

    \<Nombre de carpeta > es el nombre de la carpeta que se creó. A continuación, se muestra un ejemplo.

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```

   *    Tipo `exit` ya no sea el superusuario.

   *    Para probar, cree una base de datos en esa carpeta. El ejemplo que se muestra a continuación, usa sqlcmd para crear una base de datos, cambiar el contexto a ella, compruebe los archivos existen en el nivel de sistema operativo y, a continuación, elimina la ubicación temporal. Puede usar SSMS.
  
    ![50-ExampleCreateSSMS][9]

   *    Desmontar el recurso compartido 

    ```bash
    sudo umount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > es el nombre del grupo de volúmenes, \<LogicalVolumeName > es el nombre del volumen lógico que se creó, y \<nombreDeCarpeta > es el nombre de la carpeta. Sintaxis de ejemplo se muestran a continuación.

    ```bash
    sudo umount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

14. Configure el servidor para que esa única Pacemaker puede activar el grupo de volúmenes.

    ```bash
    sudo lvmconf --enable-halvm --services -startstopservices
    ```
 
15. Generar una lista de los grupos de volúmenes en el servidor. Nada muestran que no sea el disco iSCSI se usa el sistema, como para el disco del sistema operativo.

    ```bash
    sudo vgs
    ```

16. Modifique la sección de configuración de activación de la /etc/lvm/lvm.conf archivo. Configure la siguiente línea:

    ```bash
    volume_list = [ <ListOfVGsNotUsedByPacemaker> ]
    ```

    \<ListOfVGsNotUsedByPacemaker > es la lista de grupos de volúmenes de la salida de paso 20 que no se usará para la FCI. Coloque cada uno de ellos en las comillas y separados por punto y coma. A continuación, se muestra un ejemplo.

    ![55-ListOfVGs][11]
 
 
17. Cuando se inicia Linux, montará el sistema de archivos. Para asegurarse de que Pacemaker sólo puede montar el disco iSCSI, vuelva a generar la imagen de sistema de archivos raíz. 

    Ejecute el siguiente comando lo que puede tardar unos minutos en completarse. No pondremos ningún mensaje si se realiza correctamente.

    ```bash
    sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
    ```

18. Reinicie el servidor.

19. En otro servidor que vaya a participar en la FCI, realice los pasos 1 - 6. Esto presentará el destino iSCSI para el servidor SQL Server. 
 
20. Generar una lista de los grupos de volúmenes en el servidor. Debe mostrar el grupo de volúmenes que creó anteriormente. 

    ```bash
    sudo vgs
    ``` 
23. Inicie SQL Server y compruebe que se puede iniciar en este servidor.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```

24. Detener SQL Server y compruebe que está apagada.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
25. Repita los pasos del 1 al 6 en cualquier otro servidor que vaya a participar en la FCI.

Ahora está listo para configurar la FCI.

|Distribución |Tema 
|----- |-----
|**Red Hat Enterprise Linux con el complemento de alta disponibilidad** |[Configurar](sql-server-linux-shared-disk-cluster-configure.md)<br/>[Operar](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server con el complemento de alta disponibilidad** |[Configurar](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>Pasos siguientes

[Configurar la instancia de clúster de conmutación por error: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/05-initiator.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/10-iscsiTargetSettings.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/15-iSCSITargetResults.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/20-iSCSITargetLogin.png
[5]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/25-iSCSIVerify.png
[6]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/7-setiscsinetwork.png
[7]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/30-iSCSIattachedDisks.png
[8]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/45-CopyMove.png
[9]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/50-ExampleCreateSSMS.png
[10]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/40-Create25GBVol.png
[11]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/55-ListOfVGs.png
