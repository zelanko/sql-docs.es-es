---
title: 'Las instancias de clúster de conmutación por error: SQL Server en Linux | Microsoft Docs'
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: bc689b96be7fbfcf348ec6d55e27abcceb2024d6
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2018
ms.locfileid: "51032672"
---
# <a name="failover-cluster-instances---sql-server-on-linux"></a>Instancias de clúster de conmutación por error: SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se explica los conceptos relacionados con instancias de clúster de conmutación por error (FCI) de SQL Server en Linux. 

Para crear una FCI de SQL Server en Linux, consulte [configurar FCI de SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>El nivel de agrupación en clústeres

* En RHEL, el nivel de agrupación en clústeres se basa en Red Hat Enterprise Linux (RHEL) [complemento de alta disponibilidad](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf). 

    > [!NOTE] 
    > Acceso a Red Hat alta disponibilidad de complementos y documentación requiere una suscripción. 

* En SLES, el nivel de agrupación en clústeres se basa en SUSE Linux Enterprise [extensión de alta disponibilidad (HAE)](https://www.suse.com/products/highavailability).

    Para obtener más información sobre la configuración del clúster, las opciones del agente de recursos, administración, procedimientos recomendados y recomendaciones, consulte [SUSE Linux Enterprise alta disponibilidad extensión 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

El complemento de alta disponibilidad de RHEL y el HAE SUSE se basan en [Pacemaker](http://clusterlabs.org/).

Como se muestra en el siguiente diagrama, almacenamiento se presenta en dos servidores. Componentes de agrupación en clústeres, Corosync y Pacemaker, coordinan las comunicaciones y administración de recursos. Uno de los servidores tiene la conexión activa a los recursos de almacenamiento y el servidor SQL Server. Cuando Pacemaker detecta un error de los componentes de agrupación en clústeres administran mover los recursos a otro nodo.  

![Red Hat Enterprise Linux 7 compartidos de clúster de disco de SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> En este momento, integración de SQL Server con Pacemaker en Linux no es tan acoplamiento como con WSFC en Windows. Desde dentro de SQL, no hay ningún conocimiento sobre la presencia del clúster, todas las orquestaciones está fuera de y Pacemaker controla el servicio como una instancia independiente. Además, nombre de red virtual es WSFC específico, no hay ningún equivalente de la misma en Pacemaker. Se espera que @@servername y sys.servers para devolver el nombre de nodo, mientras que el clúster DMV sys.dm_os_cluster_nodes y sys.dm_os_cluster_properties no hará ningún registro. Para usar una cadena de conexión que apunta a un nombre de servidor de la cadena y no usar la dirección IP, tendrá que registrar la dirección IP usada para crear el recurso IP virtual (como se explica en las secciones siguientes) en su servidor DNS con el nombre de servidor elegido.

## <a name="number-of-instances-and-nodes"></a>Número de instancias y nodos

Una diferencia clave con SQL Server en Linux es que sólo puede haber una instalación de SQL Server por cada servidor Linux. Dicha instalación se llama a una instancia. Esto significa que, a diferencia de Windows Server que admite hasta 25 fci por clúster de conmutación por error de Windows Server (WSFC), una FCI basado en Linux solo tendrá una sola instancia. Una instancia de este también es una instancia predeterminada; No hay ningún concepto de una instancia con nombre en Linux. 

Un clúster de Pacemaker solo puede tener hasta 16 nodos cuando está implicada en Corosync, por lo que un FCI solo puede abarcar hasta 16 servidores. Una FCI implementada con Standard Edition de SQL Server admite hasta dos nodos de un clúster, incluso si el clúster de Pacemaker tiene el máximo de 16 nodos.

En una FCI de SQL Server, la instancia de SQL Server está activa en un nodo o la otra.

## <a name="ip-address-and-name"></a>Nombre y dirección IP
En un clúster de Linux Pacemaker, cada FCI de SQL Server necesita su propia dirección IP única y el nombre. Si la configuración de FCI abarca varias subredes, se solicitará una dirección IP por subred. El nombre único y las direcciones IP se usan para tener acceso a la FCI para que las aplicaciones y los usuarios finales no es necesario saber qué servidor subyacente del clúster de Pacemaker.

El nombre de la FCI en DNS debe ser el mismo que el nombre del recurso FCI que se crea en el clúster de Pacemaker.
El nombre y la dirección IP deben estar registrados en DNS.

## <a name="shared-storage"></a>Almacenamiento compartido
Todas las fci, ya sean Linux o Windows Server, requieren algún tipo de almacenamiento compartido. Este almacenamiento se presenta a todos los servidores que posiblemente se pueden hospedar la FCI, pero solo un único servidor puede usar el almacenamiento para la FCI en un momento dado. Las opciones disponibles para el almacenamiento compartido en Linux son:

- iSCSI
- Network File System (NFS)
- Server Message Block (SMB) en Windows Server, hay opciones ligeramente diferentes. Una opción que no se admite actualmente para fci basado en Linux es la capacidad de usar un disco local en el nodo para TempDB, que es el área de trabajo temporal de SQL Server.

En una configuración que abarca varias ubicaciones, lo que se almacena en un centro de datos debe estar sincronizada con la otra. Si se produce una conmutación por error, la FCI podrán ponerse en línea y el almacenamiento suele ser el mismo. Para lograr esto requerirá algún método externo para la replicación de almacenamiento, si esto se ejecuta mediante el hardware de almacenamiento subyacente o alguna utilidad basada en software. 

>[!NOTE]
>Para SQL Server, deben tener el formato implementaciones basadas en Linux mediante discos presentados directamente a un servidor con XFS o EXT4. Actualmente no se admiten otros sistemas de archivos. Aquí se reflejarán los cambios.

El proceso para presentar el almacenamiento compartido es el mismo para los diferentes métodos admitidos:

- Configurar el almacenamiento compartido
- Montar el almacenamiento como una carpeta a los servidores que servirán como nodos del clúster de Pacemaker para la FCI
- Si es necesario, mover las bases de datos del sistema de SQL Server en el almacenamiento compartido
- Prueba de SQL Server trabaja desde cada servidor conectado al almacenamiento compartido

Una gran diferencia con SQL Server en Linux es que aunque puede configurar la ubicación del archivo de registro y datos de usuario de la predeterminada, las bases de datos del sistema siempre deben existir en `/var/opt/mssql/data`. En Windows Server, hay la capacidad para mover las bases de datos del sistema incluido TempDB. Este hecho se reproduce en almacenamiento compartido cómo está configurado para una FCI.

Las rutas de acceso predeterminada para bases de datos del sistema no se pueden cambiar mediante la `mssql-conf` utilidad. Para obtener información sobre cómo cambiar los valores predeterminados, [cambiar la ubicación del directorio de datos o de registro de forma predeterminada](sql-server-linux-configure-mssql-conf.md#datadir). También puede almacenar datos de SQL Server y la transacción en otras ubicaciones, siempre y cuando tengan la seguridad apropiada incluso si no es una ubicación predeterminada; la ubicación tendría que indicarse.

Los siguientes temas explican cómo configurar tipos de almacenamiento admitidos para una Linux basadas en la FCI de SQL Server:

- [Configurar la instancia de clúster de conmutación por error - iSCSI: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [Configurar la instancia de clúster de conmutación por error: NFS: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [Configurar la instancia de clúster de conmutación por error: SMB: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)
