---
title: Operar clúster compartido de Red Hat Enterprise Linux para SQL Server | Microsoft Docs
description: Implementar la alta disponibilidad mediante la configuración de clúster de disco compartido de Red Hat Enterprise Linux para SQL Server.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 075ab7d8-8b68-43f3-9303-bbdf00b54db1
ms.openlocfilehash: 2fdccaf93ad53e6fda7671b734dc1ce12caa652c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47641683"
---
# <a name="operate-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Operar el clúster de disco compartido de Red Hat Enterprise Linux para SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento describe cómo realizar las tareas siguientes para SQL Server en un clúster de conmutación por error de disco compartido con Red Hat Enterprise Linux.

- Conmutación por error manual del clúster
- Supervisar un servicio de SQL Server del clúster de conmutación por error
- Agregar un nodo de clúster
- Quitar un nodo de clúster
- Cambiar la frecuencia de supervisión de recursos de SQL Server

## <a name="architecture-description"></a>Descripción de la arquitectura

El nivel de agrupación en clústeres se basa en Red Hat Enterprise Linux (RHEL) [complemento de alta disponibilidad](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) construidos sobre [Pacemaker](http://clusterlabs.org/). Corosync y Pacemaker coordinan las comunicaciones del clúster y la administración de recursos. La instancia de SQL Server está activa en un nodo o la otra.

El siguiente diagrama ilustra los componentes de un clúster de Linux con SQL Server. 

![Red Hat Enterprise Linux 7 compartidos de clúster de disco de SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

Para obtener más información sobre la configuración del clúster, las opciones de los agentes de recursos y administración, visite [documentación de referencia RHEL](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).

## <a name = "failManual"></a>Clúster de conmutación por error manualmente

El `resource move` comando crea una restricción de forzar el recurso para iniciarse en el nodo de destino.  Después de ejecutar el `move` comando, ejecutando el recurso `clear` quitará la restricción, por lo que es posible mover el recurso nuevo o que el recurso se conmutarán por error automáticamente. 

```bash
sudo pcs resource move <sqlResourceName> <targetNodeName>  
sudo pcs resource clear <sqlResourceName> 
```

En el ejemplo siguiente se mueve el **mssqlha** recursos a un nodo denominado **sqlfcivm2**y, a continuación, quita la restricción para que el recurso puede mover a otro nodo más adelante.  

```bash
sudo pcs resource move mssqlha sqlfcivm2 
sudo pcs resource clear mssqlha 
```

## <a name="monitor-a-failover-cluster-sql-server-service"></a>Supervisar un servicio de SQL Server del clúster de conmutación por error

Ver el estado actual del clúster:

```bash
sudo pcs status  
```

Ver el estado activo del clúster y recursos:

```bash
sudo crm_mon 
```

Ver los registros del agente de recursos en `/var/log/cluster/corosync.log`

## <a name="add-a-node-to-a-cluster"></a>Agregar un nodo a un clúster

1. Compruebe la dirección IP para cada nodo. El siguiente script muestra la dirección IP del nodo actual. 

   ```bash
   ip addr show
   ```

3. El nuevo nodo necesita un nombre único que es de 15 caracteres o menos. De forma predeterminada en Red Hat Linux es el nombre del equipo `localhost.localdomain`. Este nombre predeterminado puede no ser única y es demasiado largo. Establezca el nombre de equipo del nuevo nodo. Establece el nombre del equipo mediante la adición a `/etc/hosts`. El siguiente script le permite editar `/etc/hosts` con `vi`. 

   ```bash
   sudo vi /etc/hosts
   ```

   El ejemplo siguiente muestra `/etc/hosts` con adiciones de tres nodos denominados `sqlfcivm1`, `sqlfcivm2`, y`sqlfcivm3`.

   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1         localhost localhost6 localhost6.localdomain6
   10.128.18.128 fcivm1
   10.128.16.77 fcivm2
   10.128.14.26 fcivm3
    ```
    
   El archivo debe ser el mismo en todos los nodos. 

1. Detenga el servicio de SQL Server en el nuevo nodo.

1. Siga las instrucciones para montar el directorio de archivos de base de datos a la ubicación compartida:

   Desde el servidor NFS, instalar `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils 
   ``` 

   Abra el firewall de los clientes y el servidor NFS 

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

   Edite el archivo/etc/fstab para incluir el comando de montaje: 

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr
   ```

   Ejecute `mount -a` para que los cambios surtan efecto.
   
1. En el nodo nuevo, cree un archivo para almacenar el nombre de usuario de SQL Server y la contraseña para el inicio de sesión de Pacemaker. Con el siguiente comando se crea y rellena este archivo:

   ```bash
   sudo touch /var/opt/mssql/passwd
   sudo echo "<loginName>" >> /var/opt/mssql/secrets/passwd
   sudo echo "<loginPassword>" >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/passwd
   sudo chmod 600 /var/opt/mssql/passwd
   ```

3. En el nuevo nodo, abra los puertos de firewall de Pacemaker. Para abrir estos puertos con `firewalld`, ejecute el comando siguiente:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > [!NOTE]
   > Si usa otro firewall que no tiene una configuración de alta disponibilidad integrada, deberán abrirse los puertos siguientes para que Pacemaker pueda comunicarse con otros nodos del clúster.
   >
   > * TCP: puertos 2224, 3121, 21064
   > * UDP: puerto 5405

1. Instale los paquetes de Pacemaker en el nuevo nodo.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
 
2. Establezca la contraseña para el usuario predeterminado que se crea al instalar paquetes de Pacemaker y Corosync. Usar la misma contraseña que los nodos existentes. 

   ```bash
   sudo passwd hacluster
   ```
 
3. Habilite e inicie el servicio `pcsd` y Pacemaker. Esto permitirá que el nuevo nodo se unan al clúster después del reinicio. Ejecute el siguiente comando en el nuevo nodo.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Instale el agente de recursos de FCI para SQL Server. Ejecute los comandos siguientes en el nuevo nodo. 

   ```bash
   sudo yum install mssql-server-ha
   ```

1. En un nodo existente desde el clúster, autenticar el nuevo nodo y agregarlo al clúster:

    ```bash
    sudo pcs    cluster auth <nodeName3> -u hacluster 
    sudo pcs    cluster node add <nodeName3> 
    ```

    En el ejemplo siguiente se agrega un nodo denominado **vm3** al clúster.

    ```bash
    sudo pcs    cluster auth  
    sudo pcs    cluster start 
    ```

## <a name="remove-nodes-from-a-cluster"></a>Quitar nodos de un clúster

Para quitar un nodo de un clúster que ejecute el siguiente comando:

```bash
sudo pcs    cluster node remove <nodeName>  
```

## <a name="change-the-frequency-of-sqlservr-resource-monitoring-interval"></a>Cambiar la frecuencia del intervalo de supervisión de recursos de sqlservr

```bash
sudo pcs    resource op monitor interval=<interval>s <sqlResourceName> 
```

El ejemplo siguiente establece el intervalo de supervisión a 2 segundos para el recurso mssql:

```bash
sudo pcs    resource op monitor interval=2s mssqlha 
```
## <a name="troubleshoot-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Solución de problemas de clúster de disco compartido de Red Hat Enterprise Linux para SQL Server

Para solucionar problemas del clúster puede ser útil para comprender cómo funcionan conjuntamente los demonios de tres para administrar recursos de clúster. 

| Demonio | Descripción 
| ----- | -----
| Corosync | Proporciona pertenencia de quórum y mensajería entre los nodos del clúster.
| Pacemaker | Reside en la parte superior Corosync y proporciona a las máquinas de estado para los recursos. 
| PCSD | Administra Pacemaker y Corosync a través de la `pcs` herramientas

Debe ejecutar PCSD para poder usar `pcs` herramientas. 

### <a name="current-cluster-status"></a>Estado actual del clúster 

`sudo pcs status` Devuelve información básica sobre el estado del clúster, quórum, nodos, recursos y el demonio para cada nodo. 

Un ejemplo de una salida de quórum en buen estado pacemaker sería:

```
Cluster name: MyAppSQL 
Last updated: Wed Oct 31 12:00:00 2016  Last change: Wed Oct 31 11:00:00 2016 by root via crm_resource on sqlvmnode1 
Stack: corosync 
Current DC: sqlvmnode1  (version 1.1.13-10.el7_2.4-44eb2dd) - partition with quorum 
3 nodes and 1 resource configured 

Online: [ sqlvmnode1 sqlvmnode2 sqlvmnode3] 

Full list of resources: 

mssqlha (ocf::sql:fci): Started sqlvmnode1 

PCSD Status: 
sqlvmnode1: Online 
sqlvmnode2: Online 
sqlvmnode3: Online 

Daemon Status: 
corosync: active/disabled 
pacemaker: active/enabled 
```

En el ejemplo, `partition with quorum` significa que un quórum de mayoría de nodos está en línea. Si el clúster pierde un quórum de mayoría de nodos, `pcs status` devolverá `partition WITHOUT quorum` y se detendrán todos los recursos. 

`online: [sqlvmnode1 sqlvmnode2 sqlvmnode3]` Devuelve el nombre de todos los nodos que participan actualmente en el clúster. Si todos los nodos no están participando, `pcs status` devuelve `OFFLINE: [<nodename>]`.

`PCSD Status` Muestra el estado del clúster para cada nodo.

### <a name="reasons-why-a-node-may-be-offline"></a>Motivos de por qué un nodo puede estar sin conexión

Compruebe los siguientes elementos cuando un nodo está sin conexión.

- **Firewall de**

    Necesitan los siguientes puertos estén abiertos en todos los nodos para que Pacemaker pueda comunicarse.
    
    - ** TCP: 2224, 3121, 21064

- **Pacemaker o servicios Corosync en ejecución**

- **Comunicación de nodo**

- **Asignaciones de nombres de nodo**

## <a name="additional-resources"></a>Recursos adicionales

* [Desde el principio del clúster](http://clusterlabs.org/doc/Cluster_from_Scratch.pdf) Guía de Pacemaker

## <a name="next-steps"></a>Pasos siguientes

[Configuración de clúster de disco compartido de Red Hat Enterprise Linux para SQL Server](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)

