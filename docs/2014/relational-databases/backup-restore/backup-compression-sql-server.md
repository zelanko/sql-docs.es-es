---
title: Compresión de copia de seguridad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], backup compression
- backup compression [SQL Server], about backup compression
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- backing up [SQL Server], backup compression
- backup compression [SQL Server]
ms.assetid: 05bc9c4f-3947-4dd4-b823-db77519bd4d2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: af3e8d9184b12a726361643c563402242c6b04cd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62876812"
---
# <a name="backup-compression-sql-server"></a>Compresión de copia de seguridad (SQL Server)
  En este tema se describe la compresión de copias de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluidas las restricciones, las ventajas y desventajas de la compresión de las copias de seguridad respecto al rendimiento, la configuración de la compresión de copias de seguridad y la razón de compresión.  
  
> [!NOTE]  
>  Para obtener información sobre las [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ediciones de que admiten la compresión de copia de seguridad, vea [características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Cada edición de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y posteriores pueden restaurar una copia de seguridad cifrada.  
  
  
##  <a name="benefits"></a><a name="Benefits"></a> Ventajas  
  
-   Dado que el tamaño de una copia de seguridad comprimida es menor que el de una sin comprimir de los mismos datos, normalmente la compresión de una copia de seguridad requiere menos operaciones de E/S en los dispositivos y, por consiguiente, suele aumentar significativamente la velocidad de creación de la copia.  
  
     Para obtener más información, vea [Impacto en el rendimiento de la compresión de las copias de seguridad](#PerfImpact), más adelante en este tema.  
  
  
##  <a name="restrictions"></a><a name="Restrictions"></a> Restricciones  
 La compresión de las copias de seguridad está sujeta a las siguientes restricciones:  
  
-   Las copias de seguridad comprimidas y sin comprimir no pueden coexistir al mismo tiempo en un mismo conjunto de medios.  
  
-   Las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pueden leer copias de seguridad comprimidas.  
  
-   NTbackups no puede compartir una cinta con copias de seguridad comprimidas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
##  <a name="performance-impact-of-compressing-backups"></a><a name="PerfImpact"></a> Impacto en el rendimiento de la compresión de las copias de seguridad  
 De forma predeterminada, la compresión aumenta significativamente el uso de CPU y la CPU adicional que consume el proceso de compresión puede afectar adversamente a las operaciones simultáneas. Por consiguiente, podría ser conveniente crear copias de seguridad comprimidas de prioridad baja en una sesión en la que el[regulador de recursos](../resource-governor/resource-governor.md)limite el uso de CPU. Para obtener más información, vea [Usar el regulador de recursos para limitar el uso de CPU mediante compresión de copia de seguridad &#40;Transact-SQL&#41;](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)limite el uso de CPU.  
  
 Para hacerse una idea acertada del rendimiento de la E/S de su copia de seguridad, puede aislar la E/S de la copia de seguridad realizada hacia o desde los dispositivos evaluando los siguientes tipos de contadores de rendimiento:  
  
-   Contadores de rendimiento de la E/S de Windows, tales como los contadores de disco físico  
  
-   El contador **Rendimiento del dispositivo en bytes/s** del objeto [SQLServer:Backup Device](../performance-monitor/sql-server-backup-device-object.md)  
  
-   El contador **Rendimiento de copia de seguridad o restauración/s** del objeto [SQLServer:Databases](../performance-monitor/sql-server-databases-object.md)  
  
 Para obtener más información acerca de los contadores de Windows, vea la ayuda de Windows. Para obtener información sobre el trabajo con contadores de SQL Server, vea [Usar objetos de SQL Server](../performance-monitor/use-sql-server-objects.md).  
  
  
##  <a name="calculate-the-compression-ratio-of-a-compressed-backup"></a><a name="CompressionRatio"></a> Calcular la razón de compresión de una copia de seguridad comprimida  
 Para calcular la razón de compresión de una copia de seguridad, use los valores de la copia de seguridad de las columnas **backup_size** y **compressed_backup_size** de la tabla de historial [backupset](/sql/relational-databases/system-tables/backupset-transact-sql) , de la manera siguiente:  
  
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
  
  
##  <a name="allocation-of-space-for-the-backup-file"></a><a name="Allocation"></a> Asignación de espacio para el archivo de copia de seguridad.  
 Para las copias de seguridad comprimidas, el tamaño del archivo de copia de seguridad final depende de en qué grado puedan comprimirse los datos y esto no se conoce antes de que la operación de copia de seguridad finalice.  Por lo tanto, de forma predeterminada al hacer una copia de seguridad de una base de datos usando la compresión, el Motor de base de datos usa un algoritmo de preasignación para el archivo de copia de seguridad. Este algoritmo preasigna una porcentaje predefinido del tamaño de la base de datos para el archivo de copia de seguridad. Si se necesita más espacio durante la operación de copia de seguridad, el Motor de base de datos hace crecer el archivo. Si el tamaño final es menor que el espacio asignado, al final de la operación de copia de seguridad, el Motor de base de datos reduce el archivo hasta el tamaño final real de la copia de seguridad.  
  
 Para que el archivo de copia de seguridad crezca solo lo necesario para alcanzar su tamaño final, use la marca de seguimiento 3042. La marca de seguimiento 3042 hace que la operación de copia de seguridad omita el algoritmo de preasignación de compresión de copia de seguridad predeterminada. Esta marca de seguimiento es útil si tiene que ahorrar espacio asignando solo el tamaño real requerido para la copia de seguridad comprimida. No obstante, el uso de esta marca de seguimiento podría ocasionar una ligera reducción en el rendimiento (un posible aumento de la duración de la operación de copia de seguridad).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Configurar la compresión de copia de seguridad &#40;SQL Server&#41;](backup-compression-sql-server.md)  
  
-   [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
-   [Usar el regulador de recursos para limitar el uso de CPU mediante compresión de copia de seguridad &#40;Transact-SQL&#41;](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [DBCC TRACEON &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-transact-sql)  
  
-   [DBCC TRACEOFF &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceoff-transact-sql)  
  
## <a name="see-also"></a>Consulte también  
 [Información general de copia de seguridad &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Marcas de seguimiento &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)  
  
  
