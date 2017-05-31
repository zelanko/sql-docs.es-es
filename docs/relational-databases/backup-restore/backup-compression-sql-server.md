---
title: "Compresión de copia de seguridad (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- log shipping [SQL Server], backup compression
- backup compression [SQL Server], about backup compression
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- backing up [SQL Server], backup compression
- backup compression [SQL Server]
ms.assetid: 05bc9c4f-3947-4dd4-b823-db77519bd4d2
caps.latest.revision: 51
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 08936c44013d5494c72500f3230a1c90da1e4325
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="backup-compression-sql-server"></a>Compresión de copia de seguridad (SQL Server)
  En este tema se describe la compresión de copias de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluidas las restricciones, las ventajas y desventajas de la compresión de las copias de seguridad respecto al rendimiento, la configuración de la compresión de copias de seguridad y la razón de compresión.  La compresión de copia de seguridad es compatible las ediciones Enterprise, Standard y Developer de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  Cada edición de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y posteriores pueden restaurar una copia de seguridad cifrada. 
 
  
##  <a name="Benefits"></a> Ventajas  
  
-   Dado que el tamaño de una copia de seguridad comprimida es menor que el de una sin comprimir de los mismos datos, normalmente la compresión de una copia de seguridad requiere menos operaciones de E/S en los dispositivos y, por consiguiente, suele aumentar significativamente la velocidad de creación de la copia.  
  
     Para obtener más información, vea [Impacto en el rendimiento de la compresión de las copias de seguridad](#PerfImpact), más adelante en este tema.  
  
  
##  <a name="Restrictions"></a> Restricciones  
 La compresión de las copias de seguridad está sujeta a las siguientes restricciones:  
  
-   Las copias de seguridad comprimidas y sin comprimir no pueden coexistir al mismo tiempo en un mismo conjunto de medios.  
  
-   Las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pueden leer copias de seguridad comprimidas.  
  
-   NTbackups no puede compartir una cinta con copias de seguridad comprimidas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
##  <a name="PerfImpact"></a> Impacto en el rendimiento de la compresión de las copias de seguridad  
 De forma predeterminada, la compresión aumenta significativamente el uso de CPU y la CPU adicional que consume el proceso de compresión puede afectar adversamente a las operaciones simultáneas. Por consiguiente, podría ser conveniente crear copias de seguridad comprimidas de prioridad baja en una sesión en la que el[regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)limite el uso de CPU. Para obtener más información, vea [Usar el regulador de recursos para limitar el uso de CPU mediante compresión de copia de seguridad &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)limite el uso de CPU.  
  
 Para hacerse una idea acertada del rendimiento de la E/S de su copia de seguridad, puede aislar la E/S de la copia de seguridad realizada hacia o desde los dispositivos evaluando los siguientes tipos de contadores de rendimiento:  
  
-   Contadores de rendimiento de la E/S de Windows, tales como los contadores de disco físico  
  
-   El contador **Rendimiento del dispositivo en bytes/s** del objeto [SQLServer:Backup Device](../../relational-databases/performance-monitor/sql-server-backup-device-object.md)  
  
-   El contador **Rendimiento de copia de seguridad o restauración/s** del objeto [SQLServer:Databases](../../relational-databases/performance-monitor/sql-server-databases-object.md)  
  
 Para obtener más información acerca de los contadores de Windows, vea la ayuda de Windows. Para obtener información sobre el trabajo con contadores de SQL Server, vea [Usar objetos de SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
   
##  <a name="CompressionRatio"></a> Calcular la razón de compresión de una copia de seguridad comprimida  
 Para calcular la razón de compresión de una copia de seguridad, use los valores de la copia de seguridad de las columnas **backup_size** y **compressed_backup_size** de la tabla de historial [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) , de la manera siguiente:  
  
 **backup_size**:**compressed_backup_size**  
  
 Por ejemplo, una razón de compresión de 3:1 indica que está ahorrando aproximadamente un 66% del espacio en disco. Para consultar estas columnas, puede utilizar la siguiente instrucción de Transact-SQL:  
  
```  
SELECT backup_size/compressed_backup_size FROM msdb..backupset;  
```  
  
 La razón de compresión de una copia de seguridad comprimida depende de los datos que se hayan comprimido. La razón de compresión obtenida puede verse influenciada por diversos factores. Entre los factores más importantes tenemos:  
  
-   El tipo de datos.  
  
     El texto se comprime más que otros tipos de datos.  
  
-   La coherencia de los datos entre las filas de una página.  
  
     Normalmente, si una página contiene varias filas en las que un campo contiene el mismo valor, se podría producir una compresión significativa para ese valor. En contraste, para una base de datos que contiene datos aleatorios o que contiene solo una fila de gran tamaño por página, la copia de seguridad comprimida sería casi tan grande como la copia de seguridad sin comprimir.  
  
-   Si los datos están o no cifrados.  
  
     Los datos cifrados se comprimen mucho menos que los datos no cifrados equivalentes. Si se usa el cifrado transparente de los datos para cifrar una base de datos completa, al comprimir las copias de seguridad, podría no reducirse mucho su tamaño, o nada en absoluto.  
  
-   Si la base de datos está comprimida.  
  
     Si la base de datos está comprimida, puede que la compresión de las copias de seguridad no reduzca demasiado su tamaño, si es que logra alguna reducción.  
  
  
##  <a name="Allocation"></a> Asignación de espacio para el archivo de copia de seguridad.  
 Para las copias de seguridad comprimidas, el tamaño del archivo de copia de seguridad final depende de en qué grado puedan comprimirse los datos y esto no se conoce antes de que la operación de copia de seguridad finalice.  Por lo tanto, de forma predeterminada al hacer una copia de seguridad de un abase de datos usando la compresión, el Motor de base de datos usa un algoritmo de preasignación para el archivo de copia de seguridad. Este algoritmo preasigna una porcentaje predefinido del tamaño de la base de datos para el archivo de copia de seguridad. Si se necesita más espacio durante la operación de copia de seguridad, el Motor de base de datos hace crecer el archivo. Si el tamaño final es menor que el espacio asignado, al final de la operación de copia de seguridad, el Motor de base de datos reduce el archivo hasta el tamaño final real de la copia de seguridad.  
  
 Para que el archivo de copia de seguridad crezca solo lo necesario para alcanzar su tamaño final, use la marca de seguimiento 3042. La marca de seguimiento 3042 hace que la operación de copia de seguridad omita el algoritmo de preasignación de compresión de copia de seguridad predeterminada. Esta marca de seguimiento es útil si tiene que ahorrar espacio asignando solo el tamaño real requerido para la copia de seguridad comprimida. No obstante, el uso de esta marca de seguimiento podría ocasionar una ligera reducción en el rendimiento (un posible aumento de la duración de la operación de copia de seguridad).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Configurar la compresión de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/configure-backup-compression-sql-server.md)  
  
-   [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
-   [Usar el regulador de recursos para limitar el uso de CPU mediante compresión de copia de seguridad &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
  
-   [DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Información general de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Marcas de seguimiento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
  

