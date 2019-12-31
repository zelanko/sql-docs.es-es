---
title: Copia de seguridad y restauración
description: Describe cómo funciona la copia de seguridad y restauración de datos para el almacenamiento de datos paralelos (PDW). Las operaciones de copia de seguridad y restauración se utilizan para la recuperación ante desastres. Las copias de seguridad y restauración también se pueden usar para copiar una base de datos de un dispositivo a otro.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 01/19/2019
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 75399480879623a39da542c68f036389c645f6ab
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401348"
---
# <a name="backup-and-restore"></a>Copia de seguridad y restauración

Describe cómo funciona la copia de seguridad y restauración de datos para el almacenamiento de datos paralelos (PDW). Las operaciones de copia de seguridad y restauración se utilizan para la recuperación ante desastres. Las copias de seguridad y restauración también se pueden usar para copiar una base de datos de un dispositivo a otro.  
    
## <a name="BackupRestoreBasics"></a>Conceptos básicos de copias de seguridad y restauración

Una *copia de seguridad de base de datos* de PDW es una copia de una base de datos de la aplicación, que se almacena en un formato para que se pueda usar para restaurar la base de datos original en un dispositivo.  
  
Una copia de seguridad de la base de datos de PDW se crea con [la instrucción de](../t-sql/statements/restore-database-parallel-data-warehouse.md) t-SQL de la base de [datos de copia](../t-sql/statements/backup-database-parallel-data-warehouse.md) no se puede usar para ningún otro propósito. La copia de seguridad solo se puede restaurar en un dispositivo con el mismo número o un número mayor de nodos de proceso.  
  
<!-- MISSING LINKS
The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  
-->
  
PDW usa SQL Server tecnología de copia de seguridad para realizar copias de seguridad y restaurar bases de datos del dispositivo. SQL Server opciones de copia de seguridad están preconfiguradas para usar la compresión de copia de seguridad. No se pueden establecer opciones de copia de seguridad como la compresión, suma de comprobación, tamaño de bloque y recuento de búferes.  
  
Las copias de seguridad de base de datos se almacenan en uno o varios servidores de copia de seguridad, que existen en su propia red de clientes.  PDW escribe una copia de seguridad de base de datos de usuario en paralelo directamente desde los nodos de proceso en un servidor de copia de seguridad y restaura una copia de seguridad de base de datos de usuario en paralelo directamente desde el servidor de copia de seguridad a los nodos de proceso.  
  
Las copias de seguridad se almacenan en el servidor de copia de seguridad como un conjunto de archivos en el sistema de archivos de Windows. Una copia de seguridad de base de datos de PDW solo se puede restaurar en PDW. Sin embargo, puede archivar las copias de seguridad de base de datos del servidor de copia de seguridad en otra ubicación mediante procesos de copia de seguridad de archivos estándar de Windows. Para obtener más información sobre los servidores de copia de seguridad, vea [adquirir y configurar un servidor de copia de seguridad](acquire-and-configure-backup-server.md).  
  
## <a name="BackupTypes"></a>Tipos de copia de seguridad Database

Hay dos tipos de datos que requieren una copia de seguridad: las bases de datos de usuario y las bases de datos del sistema (por ejemplo, la base de datos maestra). PDW no realiza una copia de seguridad del registro de transacciones.  
  
Una copia de seguridad completa de la base de datos es una copia de seguridad de toda la base de datos de PDW. Este es el tipo de copia de seguridad predeterminado. Una copia de seguridad completa de una base de datos de usuario incluye usuarios de base de datos y roles de base de datos. Una copia de seguridad de Master incluye inicios de sesión.  
  
Una copia de seguridad diferencial contiene todos los cambios realizados desde la última copia de seguridad completa. Una copia de seguridad diferencial normalmente tarda menos tiempo que una copia de seguridad completa y se puede realizar con más frecuencia. Cuando varias copias de seguridad diferenciales se basan en la misma copia de seguridad completa, cada diferencial incluye todos los cambios de la diferencia diferencial anterior.  
  
Por ejemplo, podría crear una copia de seguridad completa semanal y una copia de seguridad diferencial diariamente. Para restaurar la base de datos de usuario, es necesario restaurar la copia de seguridad completa más la última diferencial (si existe).  
  
Una copia de seguridad diferencial solo se admite para las bases de datos de usuario. Una copia de seguridad de Master es siempre una copia de seguridad completa.  
  
Para hacer una copia de seguridad de toda la aplicación, debe realizar una copia de seguridad de todas las bases de datos de usuario y una copia de seguridad de la base de datos maestra.  
  
## <a name="BackupProc"></a>Proceso copia de seguridad de base de datos

En el diagrama siguiente se muestra el flujo de datos durante una copia de seguridad de base de datos.  
  
![Proceso de copia de seguridad de PDW](media/backup-process.png "Proceso de copia de seguridad de PDW")  
  
El proceso de copia de seguridad funciona de la siguiente manera:  
  
1.  El usuario envía una instrucción TSQL de copia de seguridad de base de datos al nodo de control.  
  
    -   La copia de seguridad es una copia de seguridad completa o diferencial.  
  
2.  En el caso de las bases de datos de usuario, el nodo de control (motor MPP) crea un plan de consulta distribuida para realizar una copia de seguridad de base de datos en paralelo.  
  
3.  Cada nodo implicado en la copia de seguridad copia su archivo de copia de seguridad en el servidor de copia de seguridad utilizando SQL Server funcionalidad de copia de seguridad.  
  
    -   Cada nodo implicado copia un archivo de copia de seguridad en el servidor de copia de seguridad.  
  
    -   La copia de seguridad de base de datos de usuario (completa o diferencial) incluye una copia de seguridad de la parte de la base de datos almacenada en cada nodo de proceso y una copia de seguridad de los usuarios y roles de base de datos.  
  
4.  El dispositivo realiza la copia de seguridad en paralelo mediante la red InfiniBand.  
  
    -   PDW realiza cada copia de seguridad completa y diferencial en paralelo. Sin embargo, las copias de seguridad de varias bases de datos no se ejecutan simultáneamente. Cada solicitud de copia de seguridad debe esperar a que finalicen las copias de seguridad enviadas previamente.  
  
    -   Una copia de seguridad de la base de datos maestra solo realiza copias de seguridad del nodo de control. Este tipo de copia de seguridad se realiza en serie.  
  
5.  Una copia de seguridad de base de datos de PDW es un grupo de archivos almacenados en un directorio que reside fuera del dispositivo. El nombre del directorio se especifica como una ruta de acceso de red y un nombre de directorio. El directorio no puede ser una ruta de acceso local y no puede estar en el dispositivo.  
  
6.  Una vez finalizada la copia de seguridad, puede usar el sistema de archivos de Windows para copiar el directorio de copia de seguridad en otra ubicación, si lo desea.  
  
    -   Una copia de seguridad solo se puede restaurar en un dispositivo PDW que tenga un número igual o mayor de nodos de proceso.  
  
    -   No se puede cambiar el nombre de la copia de seguridad antes de realizar una restauración. El nombre del directorio de copia de seguridad debe coincidir con el nombre original de la copia de seguridad. El nombre original de la copia de seguridad se encuentra en el archivo backup. XML dentro del directorio de copia de seguridad. Para restaurar una base de datos a un nombre diferente, puede especificar el nuevo nombre en el comando restore. Por ejemplo: `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ`.  
  
## <a name="RestoreModes"></a>Modos de restauración de bases de datos

Una restauración completa de la base de datos vuelve a crear la base de datos de PDW mediante los datos de la copia de seguridad de base de datos. La restauración de la base de datos se realiza restaurando primero una copia de seguridad completa y, a continuación, opcionalmente restaurando una copia de seguridad diferencial. La restauración de la base de datos incluye los usuarios y los roles de base de datos.  
  
Una restauración de encabezado solo devuelve la información de encabezado de una base de datos. No restaura los datos en el dispositivo.  
  
Una restauración de dispositivo es una restauración de todo el dispositivo. Esto incluye la restauración de todas las bases de datos de usuario y la base de datos maestra.  
  
## <a name="RestoreProc"></a>Proceso de restauración

En el diagrama siguiente se muestra el flujo de datos durante una restauración de la base de datos.  
  
![Proceso de restauración](media/restore-process.png "Proceso de restauración")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>Restaurar a un dispositivo con el mismo número de nodos de proceso * *  
  
Al restaurar los datos, el dispositivo detecta el número de nodos de proceso en el dispositivo de origen y el dispositivo de destino. Si ambos dispositivos tienen el mismo número de nodos de proceso, el proceso de restauración funciona de la siguiente manera:  
  
1.  La copia de seguridad de base de datos que se va a restaurar está disponible en un recurso compartido de archivos de Windows en un servidor que no es de aplicación. Para obtener el mejor rendimiento, este servidor se conecta a la red InfiniBand de la aplicación.  
  
2.  El usuario envía una instrucción TSQL [restore database](../t-sql/statements/restore-database-parallel-data-warehouse.md) al nodo de control.  
  
    -   La restauración es una restauración completa o una restauración de encabezado. La restauración completa restaura una copia de seguridad completa y, a continuación, opcionalmente restaura una copia de seguridad diferencial.  
  
3.  El nodo de control (motor MPP) crea un plan de consulta distribuida para realizar una restauración de base de datos en paralelo.  
  
    -   SQL ServerPDW realiza la restauración de una base de datos de usuario en paralelo. Sin embargo, no se ejecutan simultáneamente varias copias de seguridad y restauraciones de bases de datos. El motor MPP coloca cada instrucción restore en una cola; debe esperar a que finalicen las solicitudes de copia de seguridad y restauración enviadas previamente.  
  
    -   Una restauración de la base de datos maestra solo restaura los datos en el nodo de control; la restauración se realiza en serie.  
  
    -   Una restauración de la información del encabezado es una operación rápida y no restaura ningún dato en los nodos de proceso o de control. En su lugar, el nodo de control devuelve los resultados como resultado de la consulta.  
  
4.  Los archivos de copia de seguridad se copian en los nodos de proceso correctos en paralelo, normalmente a través de la red InfiniBand del dispositivo.  
  
5.  Cada nodo de proceso restaura su parte de la base de datos de usuario. Si alguna de las restauraciones no finaliza correctamente, se quitan todas las bases de datos y la restauración se completa sin éxito.  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>Restaurar a un dispositivo con más nodos de ejecución  
  
Restaurar una copia de seguridad en un dispositivo con un gran número de nodos de ejecución aumenta el tamaño de base de datos asignado en proporción al número de nodos de ejecución.  
  
Por ejemplo, al restaurar una base de datos de 60 GB desde un dispositivo de 2 nodos (30 GB por nodo) a un dispositivo de seis nodos, PDW de SQL Server crea una base de datos de 180 GB (6 nodos con 30 GB por nodo) en el dispositivo de 6 nodos. PDW de SQL Server restaura inicialmente la base de datos a 2 nodos para que coincida con la configuración de origen y, a continuación, redistribuye los datos a los 6 nodos.  
  
Después de la redistribución, cada nodo de proceso contendrá menos datos reales y más espacio libre que cada nodo de proceso en el dispositivo de origen más pequeño. Use el espacio extra para agregar más datos a la base de datos. Si el tamaño de la base de datos restaurada es mayor de lo que necesita, puede usar [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) para reducir el tamaño de los archivos de base de datos.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarea de copia de seguridad y restauración|Descripción|  
|---------------------------|---------------|  
|Preparar un servidor como servidor de copia de seguridad.|[Adquisición y configuración de servidores de copia de seguridad](acquire-and-configure-backup-server.md)|  
|Hacer copia de seguridad de una base de datos.|[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)|  
|Restaurar una base de datos.|[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)|    

<!-- MISSING LINKS

|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  

-->
