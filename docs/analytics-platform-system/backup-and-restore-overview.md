---
title: "Copias de seguridad y restauración"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Describe cómo los datos de copia de seguridad y restauración funciona para almacenamiento de datos paralelos de SQL Server (PDW)."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: d4669957-270a-4e50-baf3-14324ca63049
caps.latest.revision: "50"
ms.openlocfilehash: 06863b600ed62d795db82aa5aa3ae5c88578833a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="backup-and-restore"></a>Copias de seguridad y restauración
Describe cómo los datos de copia de seguridad y restauración funciona para almacenamiento de datos paralelos de SQL Server (PDW). Operaciones de copia de seguridad y restauración se utilizan para la recuperación ante desastres. También se pueden utilizar copia de seguridad y restauración para copiar una base de datos de un dispositivo a otro dispositivo.  
    
## <a name="BackupRestoreBasics"></a>Conceptos básicos de copia de seguridad y restauración  
Un PDW *copia de seguridad de base de datos* es una copia de una base de datos del dispositivo, almacenada en un formato para que se puede utilizar para restaurar la base de datos original en un dispositivo.  
  
Se crea una copia de seguridad de la base de datos PDW con el [copia de seguridad de la base de datos](../t-sql/statements/backup-database-parallel-data-warehouse.md) instrucción t-SQL y con formato para su uso con el [RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md) instrucción; está inutilizable para otros fines. La copia de seguridad sólo puede restaurarse en una aplicación con el mismo número o un gran número de nodos de cálculo.  
  
<!-- MISSING LINKS

The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  

-->
  
PDW usa tecnología de copia de seguridad de SQL Server para copia de seguridad y restaurar bases de datos del dispositivo. Opciones de copia de seguridad de SQL Server están preconfigurados para utilizar la compresión de copia de seguridad. No se puede establecer opciones de copia de seguridad como la compresión, suma de comprobación, tamaño de bloque y recuento de búfer.  
  
Las copias de seguridad de base de datos se almacenan en uno o más servidores copia de seguridad, que existen en su propia red de cliente.  PDW escribe una copia de seguridad de base de datos de usuario en paralelo directamente desde los nodos de proceso en un servidor de copia de seguridad y restaura una copia de seguridad de base de datos de usuario en paralelo directamente desde el servidor de copia de seguridad en los nodos de proceso.  
  
Las copias de seguridad se almacenan en el servidor de copia de seguridad como un conjunto de archivos en el sistema de archivos de Windows. Una copia de seguridad de la base de datos PDW sólo puede restaurarse con PDW. Sin embargo, puede archivar copias de seguridad de base de datos desde el servidor de copia de seguridad en otra ubicación mediante el uso de procesos de copia de seguridad de archivos de Windows estándares. Para obtener más información acerca de los servidores de copia de seguridad, consulte [adquirir y configurar un servidor de copia de seguridad](acquire-and-configure-backup-server.md).  
  
## <a name="BackupTypes"></a>Tipos de copia de seguridad de base de datos  
Hay dos tipos de datos que requieren una copia de seguridad: bases de datos de usuario y las bases de datos del sistema (por ejemplo, la base de datos maestra). PDW no copia de seguridad del registro de transacciones.  
  
Una copia de seguridad completa de la base de datos es una copia de seguridad de una base de datos completa de PDW. Este es el tipo de copia de seguridad predeterminado. Una copia de seguridad completa de una base de datos de usuario incluye usuarios de base de datos y roles de base de datos. Una copia de seguridad de master incluye inicios de sesión.  
  
Una copia de seguridad diferencial contiene todos los cambios desde la última copia de seguridad completa. Una copia de seguridad diferencial normalmente tarda menos tiempo que una copia de seguridad completa y se puede realizar con más frecuencia. Cuando varias copias de seguridad diferenciales se basan en la misma copia de seguridad completa, cada diferencial incluye todos los cambios en la copia diferencial anterior.  
  
Por ejemplo, podría crear una copia de seguridad completa semanal y una copia de seguridad diferencial diaria. Para restaurar la base de datos de usuario, la copia de seguridad completa más el último diferencial (si existe) debe restaurarse.  
  
Una copia de seguridad diferencial solo se admite para bases de datos de usuario. Una copia de seguridad de master siempre es una copia de seguridad completa.  
  
Para la aplicación completa de copia de seguridad, debe realizar una copia de seguridad de todas las bases de datos de usuario y una copia de seguridad de la base de datos maestra.  
  
## <a name="BackupProc"></a>Proceso de copia de seguridad de base de datos  
El siguiente diagrama muestra el flujo de datos durante una copia de seguridad de base de datos.  
  
![Proceso de copia de seguridad PDW](media/backup-process.png "proceso de copia de seguridad de PDW")  
  
El proceso de copia de seguridad funciona del siguiente modo:  
  
1.  El usuario envía una instrucción tsql de base de datos de copia de seguridad al nodo de Control.  
  
    -   La copia de seguridad es una copia de seguridad completa o diferencial.  
  
2.  Para las bases de datos de usuario, el nodo de Control (motor de MPP) crea un plan de consulta distribuida para realizar una copia de seguridad de bases de datos paralelas.  
  
3.  Cada nodo había implicado en las copias de seguridad de su archivo de copia de seguridad para el servidor de copia de seguridad mediante la funcionalidad de copia de seguridad de SQL Server.  
  
    -   Cada nodo había implicado copia un archivo de copia de seguridad para el servidor de copia de seguridad.  
  
    -   La copia de seguridad de usuario (completa o diferencial) incluye una copia de seguridad de la parte de la base de datos almacenado en cada nodo de proceso y una copia de seguridad de los usuarios de base de datos y roles de base de datos.  
  
4.  El dispositivo realiza la copia de seguridad en paralelo mediante la red InfiniBand.  
  
    -   PDW realiza cada copia de seguridad completa y diferencial en paralelo. Sin embargo, varias copias de seguridad de base de datos no se ejecutan simultáneamente. Cada solicitud de copia de seguridad debe esperar a que las copias de seguridad enviados anteriormente Finalizar.  
  
    -   Una copia de seguridad de la base de datos maestra solo copia los datos desde el nodo de Control. Este tipo de copia de seguridad se realiza en serie.  
  
5.  Una copia de seguridad de la base de datos PDW es un grupo de archivos almacenados en un directorio en el que reside el dispositivo. El nombre del directorio se especifica como un nombre de ruta de acceso y el directorio de red. El directorio no puede ser una ruta de acceso local y no puede estar en el dispositivo.  
  
6.  Una vez finalizada la copia de seguridad, puede usar el sistema de archivos de Windows para copiar el directorio de copia de seguridad a otra ubicación, si lo desea.  
  
    -   Una copia de seguridad sólo puede restaurarse a un dispositivo PDW que tiene un número igual o mayor de nodos de cálculo.  
  
    -   No se puede cambiar el nombre de la copia de seguridad antes de realizar una restauración. El nombre del directorio de copia de seguridad debe coincidir con el nombre del nombre original de la copia de seguridad. El nombre original de la copia de seguridad se encuentra en el archivo CopiaDeSeguridad.XML dentro del directorio de copia de seguridad. Para restaurar una base de datos a un nombre diferente, puede especificar el nuevo nombre en el comando restore. Por ejemplo: `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ`.  
  
## <a name="RestoreModes"></a>Modos de restauración de base de datos  
Una restauración completa de la base de datos vuelve a crea la base de datos PDW mediante el uso de los datos en la copia de seguridad de base de datos. La restauración de base de datos se realiza por primera vez restaurar una copia de seguridad completa y, a continuación, si lo desea restaurar una copia de seguridad diferencial. La restauración de base de datos incluye los usuarios de base de datos y roles de base de datos.  
  
Una restauración solo encabezado devuelve la información de encabezado de una base de datos. No se restaura datos a la aplicación.  
  
Una restauración de dispositivo es una restauración de la aplicación completa. Esto incluye la restauración de todas las bases de datos de usuario y la base de datos maestra.  
  
## <a name="RestoreProc"></a>Proceso de restauración  
El siguiente diagrama muestra el flujo de datos durante una restauración de base de datos.  
  
![Proceso de restauración](media/restore-process.png "proceso de restauración")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>Restaurar a un dispositivo con el mismo número de nodos de proceso **  
  
Al restaurar los datos, el dispositivo detecta el número de nodos de proceso en el dispositivo de origen y el dispositivo de destino. Si ambos dispositivos tienen un número igual de nodos de proceso, el proceso de restauración funciona como sigue:  
  
1.  Puede restaurar la copia de seguridad de base de datos está disponible en un recurso compartido de archivos de Windows en un servidor de copia de seguridad no sea de dispositivo. Para obtener el mejor rendimiento, este servidor normalmente está conectado a la red InfiniBand de dispositivo.  
  
2.  El usuario envía una [RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md) instrucción tsql para el nodo de Control.  
  
    -   La restauración es una restauración completa o una restauración de encabezado. La restauración completa restaura una copia de seguridad completa y, a continuación, opcionalmente restaura una copia de seguridad diferencial.  
  
3.  El nodo de Control (motor de MPP) crea un plan de consulta distribuida para realizar una restauración de base de datos paralelos.  
  
    -   ServerPDW SQL realiza la restauración de una base de datos de usuario en paralelo. Sin embargo, varias copias de seguridad y restauraciones no se ejecutan simultáneamente. El motor de MPP coloca cada instrucción de restauración en una cola; debe esperar enviado anteriormente copia de seguridad y restaurar las solicitudes a finalizar.  
  
    -   Una restauración de la base de datos maestra solo restaura los datos en el nodo de Control; la restauración se realiza en serie.  
  
    -   Una restauración de la información de encabezado es una operación rápida y no restaura los datos a los nodos de proceso o Control. En su lugar, el nodo de Control devuelve los resultados como resultado de la consulta.  
  
4.  Los archivos de copia de seguridad se copian en los nodos de proceso correctos en paralelo, normalmente a través de la red InfiniBand de dispositivo.  
  
5.  Cada nodo de proceso restaura la parte de la base de datos de usuario. Si cualquiera de la restauración no finaliza correctamente, se quitan todas las bases de datos y la restauración se completa con éxito.  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>Restaurar a un dispositivo con un gran número de nodos de proceso  
  
Restaurar una copia de seguridad en un dispositivo con un gran número de nodos de proceso, aumenta el tamaño de base de datos asignado en proporción al número de nodos de cálculo.  
  
Por ejemplo, cuando se restaura una base de datos de 60 GB desde un dispositivo de 2 nodos (30 GB por nodo) en un dispositivo de 6 nodos, PDW de SQL Server crea una base de datos de 180 GB (6 nodos con 30 GB por nodo) en el dispositivo de 6 nodos. SQL Server PDW inicialmente restaura la base de datos en 2 nodos para que coincida con la configuración de origen y, a continuación, redistribuye los datos a todos los nodos de 6.  
  
Después de la redistribución cada nodo de proceso contiene menos datos reales y más espacio libre que cada nodo de ejecución en el dispositivo de origen más pequeño. Utilice el espacio adicional para agregar más datos a la base de datos. Si el tamaño de la base de datos restaurada es superior al necesario, puede usar [ALTER DATABASE](../t-sql/statements/alter-database-parallel-data-warehouse.md) para reducir los tamaños de archivo de base de datos.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Copia de seguridad y la tarea de restauración|Description|  
|---------------------------|---------------|  
|Prepare un servidor como un servidor de copia de seguridad.|[Adquirir y configurar un servidor de copia de seguridad](acquire-and-configure-backup-server.md)|  
|Copia de seguridad de una base de datos.|[BASE DE DATOS DE COPIA DE SEGURIDAD](../t-sql/statements/backup-database-parallel-data-warehouse.md)|  
|Restaurar una base de datos.|[RESTAURAR BASE DE DATOS](../t-sql/statements/restore-database-parallel-data-warehouse.md)|    
<!-- MISSING LINKS
|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  
-->
