---
title: Configuración de clúster de disco compartido de SLES para SQL Server | Microsoft Docs
description: Implementar la alta disponibilidad mediante la configuración de clúster de disco compartido de SUSE Linux Enterprise Server (SLES) para SQL Server.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: e5ad1bdd-c054-4999-a5aa-00e74770b481
ms.openlocfilehash: f9608d4a36d8fb29185a9da949caf561f5fb1734
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39084248"
---
# <a name="configure-sles-shared-disk-cluster-for-sql-server"></a>Configuración de clúster de disco compartido de SLES para SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Esta guía proporciona instrucciones para crear un clúster de disco compartido de dos nodos para SQL Server en SUSE Linux Enterprise Server (SLES). El nivel de agrupación en clústeres se basa en SUSE [extensión de alta disponibilidad (HAE)](https://www.suse.com/products/highavailability) construidos sobre [Pacemaker](http://clusterlabs.org/). 

Para obtener más información sobre la configuración del clúster, las opciones del agente de recursos, administración, procedimientos recomendados y recomendaciones, consulte [SUSE Linux Enterprise alta disponibilidad extensión 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

## <a name="prerequisites"></a>Requisitos previos

Para completar el siguiente escenario de extremo a otro, debe tener dos máquinas para implementar el clúster de dos nodos y otro servidor para configurar el recurso compartido NFS. Los pasos siguientes describen cómo se configurará estos servidores.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Instalar y configurar el sistema operativo en cada nodo del clúster

El primer paso es configurar el sistema operativo en los nodos del clúster. Para este tutorial, use SLES con una suscripción válida para el complemento de alta disponibilidad.

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>Instalar y configurar SQL Server en cada nodo del clúster

1. Instalar y configurar SQL Server en ambos nodos. Para obtener instrucciones detalladas, consulte [instalar SQL Server en Linux](sql-server-linux-setup.md).
2. Designar un nodo como principal y el otro como secundario para fines de configuración. Usar estos términos para los siguientes elementos en esta guía. 
3. En el nodo secundario, detenga y deshabilite a SQL Server. El ejemplo siguiente se detiene y deshabilita el SQL Server:

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE]
    > Durante la instalación, se genera para la instancia de SQL Server y se coloca en una clave maestra del servidor `/var/opt/mssql/secrets/machine-key`. En Linux, SQL Server siempre se ejecuta como una cuenta local denominada mssql. Dado que es una cuenta local, su identidad no se comparte entre los nodos. Por lo tanto, deberá copiar la clave de cifrado del nodo principal en cada nodo secundario para cada cuenta local mssql pueda acceder a él para descifrar la clave maestra del servidor.
4. En el nodo principal, cree un inicio de sesión SQL server para Pacemaker y conceda el permiso de inicio de sesión para ejecutar `sp_server_diagnostics`. Pacemaker usa esta cuenta para comprobar qué nodo se está ejecutando SQL Server.

    ```bash
    sudo systemctl start mssql-server
    ```
    Conéctese a la base de datos maestra de SQL Server con la cuenta 'sa' y ejecute lo siguiente:

    ```tsql
    USE [master]
    GO
    CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
    GRANT VIEW SERVER STATE TO <loginName>
    ```
5. En el nodo principal, detenga y deshabilite a SQL Server.
6. Siga las instrucciones [en la documentación de SUSE](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) para configurar y actualizar el archivo de hosts para cada nodo del clúster. La dirección IP y el nombre de cada nodo del clúster, debe incluir el archivo "hosts".

    Para comprobar la dirección IP del nodo actual que se ejecute:

    ```bash
    sudo ip addr show
    ```

    Establezca el nombre del equipo en cada nodo. Asigne a cada nodo un nombre único que es de 15 caracteres o menos. Establece el nombre del equipo mediante la adición a `/etc/hostname` mediante [yast](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) o [manualmente](https://www.suse.com/documentation/sled11/book_sle_admin/data/sec_basicnet_manconf.html).

    El ejemplo siguiente muestra `/etc/hosts` con adiciones de dos nodos denominados `SLES1` y `SLES2`.

    ```
    127.0.0.1   localhost
    10.128.18.128 SLES1
    10.128.16.77 SLES2
    ```

    > [!NOTE]
    > Todos los nodos del clúster deben poder tener acceso entre sí a través de SSH. Herramientas como hb_report o crm_report (para solucionar problemas) y explorador de historial de Hawk requieren el acceso con SSH sin contraseña entre los nodos, ya que, de lo contrario, puede que solo recopilen datos desde el nodo actual. En caso de usar un puerto SSH no estándar, use la opción -X ([consulte la página man](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)). Por ejemplo, si el puerto SSH es 3479, invoque un crm_report con:
    >
    >```bash
    >crm_report -X "-p 3479" [...]
    >```
    >Para obtener más información, consulte [Administration Guide]. (https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)

En la siguiente sección configurará el almacenamiento compartido y mover los archivos de base de datos a la que el almacenamiento.  

## <a name="configure-shared-storage-and-move-database-files"></a>Configurar el almacenamiento compartido y mover archivos de base de datos

Hay una variedad de soluciones para proporcionar almacenamiento compartido. Este tutorial muestra cómo configurar el almacenamiento compartido NFS. Se recomienda seguir los procedimientos recomendados y utilizar Kerberos para proteger NFS: 

- [Uso compartido de los sistemas de archivos con NFS](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.nfs)

Si no sigue esta guía, cualquier persona que puede tener acceso a la red y suplantar la identidad de la dirección IP de un nodo de SQL podrán acceder a los archivos de datos. Como siempre, asegúrese de modelamos amenazas de su sistema antes de usarlo en producción. 

Otra opción de almacenamiento es usar el recurso compartido de archivos SMB:

- [Sección de Samba de documentación de SUSE](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.samba)

### <a name="configure-an-nfs-server"></a>Configurar un servidor NFS

Para configurar un servidor NFS, consulte los pasos siguientes en la documentación de SUSE: [configuración del servidor NFS](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-server).

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>Configurar todos los nodos del clúster para conectarse al almacenamiento compartido NFS

Antes de configurar el cliente NFS para montar la ruta de acceso de los archivos de base de datos de SQL Server para que apunte a la ubicación de almacenamiento compartido, asegúrese de que guardar los archivos de base de datos en una ubicación temporal para poder copiarlos posterior en el recurso compartido:

1. **En el nodo principal solo**, guardar los archivos de base de datos en una ubicación temporal. El siguiente script, crea un nuevo directorio temporal, copia los archivos de base de datos en el nuevo directorio y quita los archivos de base de datos antiguos. Como SQL Server se ejecuta como usuario local mssql, deberá asegurarse de que después de transferencia de datos para el recurso compartido montado, usuario local tiene acceso de lectura y escritura al recurso compartido. 

    ```bash
    su mssql
    mkdir /var/opt/mssql/tmp
    cp /var/opt/mssql/data/* /var/opt/mssql/tmp
    rm /var/opt/mssql/data/*
    exit
    ```

    Configurar al cliente para NFS en todos los nodos del clúster:

    - [Configuración de clientes](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-clients)

    > [!NOTE]
    > Se recomienda seguir los procedimientos recomendados y recomendaciones de almacenamiento altamente disponible NFS de SUSE: [altamente disponible almacenamiento NFS con DRBD y Pacemaker](https://www.suse.com/documentation/sle-ha-12/book_sleha_techguides/data/art_ha_quick_nfs.html).

2. Compruebe que SQL Server se inicia correctamente con la nueva ruta de acceso. Hacer esto en cada nodo. En este momento sólo un nodo debe ejecutar SQL Server a la vez. No pueden ambos ejecutar al mismo tiempo ya que ambos intentará tener acceso a los archivos de datos al mismo tiempo (para evitar accidentalmente iniciar SQL Server en ambos nodos, use un recurso de clúster del sistema de archivos para asegurarse de que no se monta el recurso compartido de dos veces por los diferentes nodos). Los siguientes comandos iniciar SQL Server, comprueban el estado y, a continuación, detener SQL Server.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    sudo systemctl stop mssql-server
    ```

En este punto, ambas instancias de SQL Server configuradas para ejecutarse con los archivos de base de datos en el almacenamiento compartido. El siguiente paso es configurar SQL Server para Pacemaker. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalación y configuración de Pacemaker en cada nodo del clúster

1. **En ambos nodos del clúster, cree un archivo para almacenar el nombre de usuario y la contraseña de SQL Server para el inicio de sesión de Pacemaker**. Con el siguiente comando se crea y rellena este archivo:

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd
    ```
2. **Todos los nodos del clúster deben poder tener acceso entre sí a través de SSH**. Herramientas como hb_report o crm_report (para solucionar problemas) y explorador de historial de Hawk requieren el acceso con SSH sin contraseña entre los nodos, ya que, de lo contrario, puede que solo recopilen datos desde el nodo actual. En caso de usar un puerto de SSH no estándar, use la opción -X (vea la página man). Por ejemplo, si el puerto SSH es 3479, invoque un hb_report del siguiente modo:

    ```bash
    crm_report -X "-p 3479" [...]
    ```

    Para más información, vea los [requisitos de sistema y recomendaciones en la documentación de SUSE](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html).

3. **Instale la extensión de alta disponibilidad**. Para instalar la extensión, siga los pasos descritos en el siguiente tema de SUSE:
    
    [Installation and Setup Quick Start](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html) (Inicio rápido de instalación y configuración)

4. **Instale el agente de recursos de FCI para SQL Server**. Ejecute los siguientes comandos en ambos nodos:

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
    sudo zypper --gpg-auto-import-keys refresh
    sudo zypper install mssql-server-ha
    ```

5. **Configure automáticamente el primer nodo**. El siguiente paso consiste en configurar un clúster de un nodo en ejecución, para lo cual configuraremos el primer nodo, SLES1. Siga las instrucciones del tema de SUSE [Setting Up the First Node](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node) (Configurar el primer nodo).

    Cuando acabe, compruebe el estado del clúster con `crm status`:
    ```bash
    crm status
    ```

    Debe mostrar que un nodo, SLES1, está configurado.

6. **Agregue nodos a un clúster existente**. A continuación, una el nodo SLES2 al clúster. Siga las instrucciones del tema de SUSE [Adding the Second Node](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.2nd-node) (Agregar el segundo nodo).
    
    Cuando acabe, compruebe el estado del clúster con **crm status**. Si ha agregado el segundo nodo correctamente, el resultado debería parecerse al siguiente:
        
    ```
    2 nodes configured
    1 resource configured
    Online: [ SLES1 SLES2 ]
    Full list of resources:
    admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
    ```

    > [!NOTE]
    > **admin_addr** es el recurso de clúster IP virtual que se configura durante la configuración inicial de un clúster de un nodo.

7.  **Procedimientos de eliminación**. Si necesita quitar un nodo del clúster, use el script de arranque **ha-cluster-remove**. Para más información, vea [Overview of the Bootstrap Scripts](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.bootstrap) (Información general de los scripts de arranque).  

## <a name="configure-the-cluster-resources-for-sql-server"></a>Configurar los recursos de clúster de SQL Server

Los pasos siguientes explican cómo configurar el recurso de clúster de SQL Server. Hay dos opciones de configuración que necesita para personalizar.

- **Nombre del recurso de SQL Server**: un nombre para el recurso de SQL Server en clúster. 
- **Valor de tiempo de espera**: el valor de tiempo de espera es la cantidad de tiempo que el clúster de espera mientras se conecta un recurso. Para SQL Server, este es el tiempo que necesita SQL Server debe tomar para mejorar la `master` en línea de base de datos. 

Actualice los valores de la siguiente secuencia de comandos para su entorno. Ejecutar en un nodo para configurar e iniciar el servicio en clúster.

```bash
sudo crm configure
primitive <sqlServerResourceName> ocf:mssql:fci op start timeout=<timeout_in_seconds>
colocation <constraintName> inf: <virtualIPResourceName> <sqlServerResourceName>
show
commit
exit
```

Por ejemplo, el script siguiente crea un recurso de SQL Server en clúster denominado mssqlha. 

```bash
sudo crm configure
primitive mssqlha ocf:mssql:fci op start timeout=60s
colocation admin_addr_mssqlha inf: admin_addr mssqlha
show
commit
exit
```

Una vez confirmada la configuración, SQL Server se iniciará en el mismo nodo que el recurso IP virtual. 

Para obtener más información, consulte [configuración y administración de recursos de clúster (línea de comandos)](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config). 

### <a name="verify-that-sql-server-is-started"></a>Compruebe que se inició SQL Server. 

Para comprobar que se inició SQL Server, ejecute el **crm estado** comando:

```bash
crm status
```

Los ejemplos siguientes muestran los resultados cuando se ha iniciado correctamente como recurso en clúster Pacemaker. 
```
2 nodes configured
2 resources configured

Online: [ SLES1 SLES2 ]

Full list of resources:

 admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
 mssqlha        (ocf::mssql:fci):       Started SLES1
```

## <a name="managing-cluster-resources"></a>Administración de recursos de clúster

Para administrar los recursos del clúster, consulte el siguiente tema SUSE: [administración de recursos de clúster](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm )

### <a name="manual-failover"></a>conmutación por error manual

Aunque los recursos están configurados para conmutar por error automáticamente (o migrar) a otros nodos del clúster si se produce un error de hardware o software, puede mover manualmente un recurso a otro nodo del clúster mediante la GUI de Pacemaker o la línea de comandos . 

Use el comando migrate para esta tarea. Por ejemplo, para migrar el recurso de SQL a un nombres de nodo de clúster SLES2 ejecutar: 

```bash
crm resource
migrate mssqlha SLES2
```

## <a name="additional-resources"></a>Recursos adicionales

[Extensión de alta disponibilidad SUSE Linux Enterprise - Guía de administración](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html) 
