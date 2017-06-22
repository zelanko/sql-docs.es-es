---
title: "Administrar el tamaño de archivo de registro de transacciones | Documentos de Microsoft"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction logs [SQL Server], size management
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 6d75e0e40c5642993cb17b09e421fbfebf40f87a
ms.openlocfilehash: cd1931ef0f77c0a1e31c29833f38c51416e267c8
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="manage-the-size-of-the-transaction-log-file"></a>Administrar el tamaño del archivo de registro de transacciones
Este tema explica cómo supervisar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tamaño de registro de transacciones, reducir el registro de transacciones, agregar a o ampliar un archivo de registro de transacciones, optimizar el **tempdb** transacciones tasa de crecimiento del registro y controlar el crecimiento de un archivo de registro de transacciones.  

  ##  <a name="MonitorSpaceUse"></a> Supervisar el uso del espacio del registro  
Supervisar el uso del espacio del registro mediante [DBCC SQLPERF (LOGSPACE)](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql). Este comando devuelve información sobre la cantidad de espacio del registro actualmente en uso e indica cuándo es necesario el truncamiento del registro de transacciones. Para obtener más información, consulte [DBCC SQLPERF Transact-SQL](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md). Para obtener información acerca de la opción de crecimiento automático del archivo, su tamaño máximo y el tamaño de archivo de registro actual, también puede usar el **tamaño**, **max_size**, y **crecimiento** columnas de ese archivo de registro en **sys.database_files**. Para obtener más información, vea [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).  
  
**Importante** Evite la sobrecarga del disco del registro.  

  
##  <a name="ShrinkSize"></a> Reducir el tamaño del archivo de registro  
 Para reducir el tamaño físico de un archivo de registro físico, debe reducir el archivo de registro. Esto es útil cuando se sabe que un archivo de registro de transacciones contiene espacio no utilizado. Puede reducir un archivo de registro solo mientras la base de datos está en línea, y al menos un archivo de registro virtual libre. En algunos casos, no será posible reducir el registro hasta el siguiente truncamiento del registro.  
  
> [!NOTE]
>  Los factores que mantienen activos los archivos de registro virtuales por un periodo prolongado de tiempo, como puede ser una transacción de ejecución prolongada, pueden restringir la reducción del registro o incluso impedirla completamente. Para obtener información sobre los factores que pueden retrasar el truncamiento del registro, vea [Registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
 Con la reducción de un archivo de registro se quitan uno o varios archivos de registro virtuales que no contienen ninguna parte del registro lógico (es decir, los *archivos de registro virtuales inactivos*). Cuando se reduce un archivo de registro de transacciones, se quitan los archivos de registro virtuales inactivos del final del archivo de registro para reducirlo aproximadamente al tamaño de destino.  
  
 **Reducir un archivo de registro (sin reducir los archivos de base de datos)**  
  
-   [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
  
-   [Reducir un archivo](../../relational-databases/databases/shrink-a-file.md)  
  
 **Supervisar los eventos de reducción de un archivo de registro**  
  
-   [Log File Auto Shrink Event Class](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md).  
  
 **Supervisar el espacio del registro**  
  
-   [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)  
  
-   [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) (Vea las columnas **size**, **max_size** y **growth** de los archivos de registro).  
  
> [!NOTE]
>  Puede establecer los archivos de registro se reduzca automáticamente. Sin embargo, no recomendamos realizar una reducción automática, y la propiedad de base de datos **autoshrink** está establecida en FALSE de forma predeterminada. Si **autoshrink** está establecida en TRUE, el proceso de reducción automática solo reduce el tamaño de un archivo cuando más del 25% de su espacio está sin utilizar. El tamaño del archivo se reduce hasta un tamaño en el que solo el 25% del archivo corresponde al espacio sin utilizar o hasta el tamaño original del archivo (el que sea mayor). Para obtener información sobre cómo cambiar la configuración de la propiedad **autoshrink**, vea [Ver o cambiar las propiedades de una base de datos](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md): use la propiedad **Auto Shrink** de la página **Opciones**, u [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md): use la opción AUTO_SHRINK.  
  

##  <a name="AddOrEnlarge"></a> Agregar o ampliar un archivo de registro  
 Puede obtener espacio ampliando el archivo de registro existente (si lo permite el espacio en disco) o mediante la adición de un archivo de registro a la base de datos, normalmente en un disco diferente.  
  
-   Para agregar un archivo de registro a la base de datos, utilice la cláusula ADD LOG FILE de la instrucción ALTER DATABASE. El hecho de agregar un archivo de registro permite que crezca el existente.  
  
-   Para aumentar el tamaño del archivo de registro, use la cláusula MODIFY FILE de la instrucción ALTER DATABASE, especificando la sintaxis de SIZE y MAXSIZE. Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
    
  
##  <a name="tempdbOptimize"></a> Optimizar el tamaño del registro de transacciones tempdb  
 Al reiniciar una instancia del servidor se devuelve el tamaño del registro de transacciones de la base de datos **tempdb** a su tamaño original, antes del crecimiento automático. Esto puede reducir el rendimiento del registro de transacciones de **tempdb** . Para evitar esta sobrecarga, aumente el tamaño del registro de transacciones de **tempdb** después de iniciar o reiniciar la instancia de servidor. Para obtener más información, consulte [tempdb Database](../../relational-databases/databases/tempdb-database.md).  
  
  
##  <a name="ControlGrowth"></a> Controlar el crecimiento de un archivo de registro de transacciones  
 Use la [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md) instrucción para administrar el crecimiento de un archivo de registro de transacciones. Observe lo siguiente:  
  
-   Para cambiar el tamaño del archivo actual en unidades de KB, MB, GB y TB, use la opción SIZE.  
  -   Para cambiar el incremento de crecimiento, use la opción FILEGROWTH. El valor 0 indica que el aumento automático se establece en OFF y no se permite ningún espacio adicional. Un pequeño incremento del crecimiento automático de un archivo de registro puede reducir el rendimiento. El incremento del crecimiento de un archivo de registro debe ser lo suficientemente grande para evitar una expansión frecuente. El incremento de crecimiento predeterminado del 10% suele resultar adecuado.  

Para obtener información sobre cómo cambiar la propiedad de crecimiento de un archivo de registro, vea [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/ms174269.aspx).  
  
-   Para controlar el máximo el tamaño de un archivo de registro en unidades de KB, MB, GB y TB o establecer el crecimiento en UNLIMITED, use la opción MAXSIZE.  
  
  
## <a name="see-also"></a>Vea también  
 [Copia de seguridad (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [Solucionar problemas de un registro de transacciones lleno (Error 9002 de servidor SQL)](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
  

