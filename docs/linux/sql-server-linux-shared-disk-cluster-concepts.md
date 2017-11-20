---
title: "Instancias de clúster de conmutación por error: SQL Server en Linux | Documentos de Microsoft"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 229c6a989a4707921eae3046e3c9707b05bb0306
ms.contentlocale: es-es
ms.lasthandoff: 10/02/2017

---

# <a name="failover-cluster-instances---sql-server-on-linux"></a>Instancias de clúster de conmutación por error: SQL Server en Linux

En este artículo se explica los conceptos relacionados con instancias de clúster de conmutación por error (FCI) de SQL Server en Linux. 

Para crear una FCI de SQL Server en Linux, consulte [configurar FCI de SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>El nivel de agrupación en clústeres

* En RHEL, el nivel de agrupación en clústeres se basa en los servicios de Red Hat Enterprise Linux (RHEL) [complemento HA](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf). 

    > [!NOTE] 
    > Acceso a documentación y HA de Red Hat complemento requiere una suscripción. 

* En SLES, el nivel de agrupación en clústeres se basa en SUSE Linux Enterprise [extensión de alta disponibilidad (HAE)](https://www.suse.com/products/highavailability).

    Para obtener más detalles sobre la configuración de clúster, opciones de recurso del agente, administración, prácticas recomendadas y recomendaciones, consulte [SUSE Linux Enterprise alta disponibilidad extensión 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

El complemento HA de RHEL y el SUSE HAE se compilan en [marcapasos](http://clusterlabs.org/).

Como muestra el diagrama siguiente se presenta el almacenamiento a dos servidores. Componentes de agrupación en clústeres - Corosync y marcapasos - coordinan las comunicaciones y administración de recursos. Uno de los servidores tiene la conexión activa a los recursos de almacenamiento y el servidor SQL Server. Cuando marcapasos detecta un error de los componentes de agrupación en clústeres administran mover los recursos a otro nodo.  

![Red Hat Enterprise Linux 7 compartido de clúster de disco de SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> En este momento, la integración de SQL Server con marcapasos en Linux no es como acoplamiento como con WSFC en Windows. Desde dentro de SQL, no hay ningún conocimiento sobre la presencia del clúster, todas las orquestaciones está fuera de y marcapasos controla el servicio como una instancia independiente. Además, el nombre de red virtual es específico de WSFC, no hay ningún equivalente de la misma en marcapasos. Se espera que @@servername y sys.servers para devolver el nombre del nodo, mientras que el clúster DMV sys.dm_os_cluster_nodes y sys.dm_os_cluster_properties no trabajará en ningún registro. Para usar una cadena de conexión que apunta a un nombre de servidor de cadena y no usar la dirección IP, tendrá que registrar en su servidor DNS la dirección IP utilizada para crear el recurso IP virtual (tal y como se explica más adelante) con el nombre del servidor seleccionado.

## <a name="number-of-instances-and-nodes"></a>Número de instancias y nodos

Una diferencia fundamental con SQL Server en Linux es que sólo puede haber una instalación de SQL Server por cada servidor Linux. Esa instalación se denomina una instancia. Esto significa que, a diferencia de Windows Server que admite hasta 25 fci por clúster de conmutación por error de Windows Server (WSFC), una FCI basado en Linux, solo tendrá una sola instancia. Esta una instancia también es una instancia predeterminada; No hay ningún concepto de una instancia con nombre en Linux. 

Un clúster marcapasos solo puede tener hasta 16 nodos cuando está implicada Corosync, por lo que un FCI solo puede abarcar hasta 16 servidores. Una FCI implementada con la edición Standard de SQL Server admite un máximo de dos nodos de un clúster incluso si el clúster marcapasos tiene el máximo de 16 nodos.

En una FCI de SQL Server, la instancia de SQL Server está activa en un nodo o la otra.

## <a name="ip-address-and-name"></a>Nombre y dirección IP
En un clúster de Linux marcapasos, cada FCI de SQL Server tendrá su propia dirección IP única y el nombre. Si la configuración de FCI abarca varias subredes, se requerirá una dirección IP por subred. El nombre único y direcciones IP se utilizan para tener acceso a la FCI para que las aplicaciones y los usuarios finales no es necesario saber qué servidor del clúster marcapasos subyacente.

El nombre de la FCI en DNS debe ser el mismo que el nombre del recurso FCI que se crea en el clúster marcapasos.
El nombre y la dirección IP deben estar registrados en DNS.

## <a name="shared-storage"></a>Almacenamiento compartido
Todas las fci, independientemente de si están en Linux o Windows Server, requiere algún tipo de almacenamiento compartido. Este almacenamiento se presenta a todos los servidores que posiblemente se pueden hospedar la FCI, pero sólo un servidor puede usar el almacenamiento para la FCI en cualquier momento. Las opciones disponibles para el almacenamiento compartido en Linux son:

- iSCSI
- Network File System (NFS)
- Servidor bloque de mensajes (SMB) en Windows Server, hay opciones ligeramente distintas. Una opción que no se admite actualmente para fci basados en Linux es la capacidad para usar un disco local en el nodo para TempDB, que es el área de trabajo temporal de SQL Server.

En una configuración que abarca varias ubicaciones, lo que está almacenado en un centro de datos debe estar sincronizado con las demás. Si se produce una conmutación por error, la FCI podrán ponerse en línea y el almacenamiento de información suele ser el mismo. Para lograr esto requerirá algún método externo para la replicación de almacenamiento, si se realiza a través de alguna utilidad basada en software o el hardware de almacenamiento subyacente. 

>[!NOTE]
>Para SQL Server 2017, implementaciones basadas en Linux con discos presentados directamente a un servidor deben tener el formato XFS o EXT4. Actualmente no se admiten otros sistemas de archivos. Aquí se reflejará los cambios.

El proceso para presentar el almacenamiento compartido es el mismo para los diferentes métodos admitidos:

- Configurar el almacenamiento compartido
- Montar el almacenamiento como una carpeta para los servidores que servirá como nodos del clúster marcapasos para la FCI
- Si es necesario, mover las bases de datos del sistema de SQL Server en el almacenamiento compartido
- Prueba de SQL Server funciona desde cada servidor conectado al almacenamiento compartido

Una diferencia principal con SQL Server en Linux es que aunque puede configurar la ubicación del archivo de registro y datos de usuario de la predeterminada, las bases de datos de sistema siempre deben existir en `/var/opt/mssql/data`. En Windows Server, hay la capacidad para mover las bases de datos del sistema incluido TempDB. Este hecho se reproduce en el almacenamiento compartido cómo está configurado para una FCI.

Las rutas de acceso predeterminada para las bases de datos del sistema no se pueden cambiar mediante la `mssql-conf` utilidad. Para obtener información sobre cómo cambiar los valores predeterminados, [cambiar la ubicación del directorio de datos o de registro de forma predeterminada](sql-server-linux-configure-mssql-conf.md#datadir). También puede almacenar datos de SQL Server y la transacción en otras ubicaciones mientras tengan la seguridad apropiada, incluso si no es una ubicación predeterminada; la ubicación tendría que se ha indicado.

Los temas siguientes explican cómo configurar tipos de almacenamiento admitidos para FCI de SQL Server que basa una Linux:

- [Configurar la instancia de clúster de conmutación por error - iSCSI: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [Configurar la instancia de clúster de conmutación por error - NFS: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [Configurar la instancia de clúster de conmutación por error - SMB - SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)

