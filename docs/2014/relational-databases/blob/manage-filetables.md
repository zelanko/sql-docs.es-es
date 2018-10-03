---
title: Administración de FileTables | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], security
- FileTables [SQL Server], managing access
ms.assetid: 93af982c-b4fe-4be0-8268-11f86dae27e1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 76a4c29d0fba58eb941bf26781b052966a0bd5b9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48186745"
---
# <a name="manage-filetables"></a>Administrar FileTables
  Describe las tareas administrativas comunes para administrar FileTables.  
  
##  <a name="HowToEnumerate"></a> Obtener una lista de FileTables y de objetos relacionados  
 Para obtener una lista de FileTables, consulte una de las siguientes vistas de catálogo:  
  
-   [sys.filetables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetables-transact-sql)  
  
-   [sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql) (consultar el valor de la columna **is_filetable**).  
  
```tsql  
SELECT * FROM sys.filetables;  
GO  
  
SELECT * FROM sys.tables WHERE is_filetable = 1;  
GO  
```  
  
 Para obtener una lista de los objetos definidos por el sistema que se crearon al mismo tiempo que las FileTables asociadas, vea la vista de catálogo [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql).  
  
```tsql  
SELECT object_id, OBJECT_NAME(object_id) AS 'Object Name'  
    FROM sys.filetable_system_defined_objects  
    WHERE object_id = filetable_object_id;  
GO  
```  
  
##  <a name="BasicsDisabling"></a> Deshabilitar o volver a habilitar el acceso no transaccional en el nivel de base de datos.  
 Con el fin de adquirir el acceso exclusivo necesario para ciertas tareas administrativas, quizá deba deshabilitar el acceso no transaccional temporalmente.  
  
 **Comportamiento de la instrucción ALTER DATABASE cuando se cambia el nivel del acceso no transaccional**  
  
-   Cuando se establece el acceso no transaccional en READ_ONLY u OFF, el comando ALTER DATABASE no devuelve el control al usuario si hay identificadores de archivos abiertos en conflicto con la operación solicitada. Los identificadores de archivos que están en conflicto con esta operación incluyen:  
  
    -   Si está configurando el acceso en **NONE**, todos los identificadores de archivos abiertos.  
  
    -   Si está estableciendo acceso en **READ_ONLY**, todos los identificadores de archivos abiertos para el acceso de escritura.  
  
     Para obtener más información acerca de la eliminación de identificadores de archivos abiertos, vea la sección [Eliminar los identificadores de archivos abiertos asociados con FileTable](#BasicsKilling) de este tema.  
  
     Si se cancela el comando ALTER DATABASE o finaliza con un tiempo de espera, no se cambia el nivel de acceso transaccional.  
  
-   Si llama a la instrucción ALTER DATABASE con una cláusula WITH \<terminación> (ROLLBACK AFTER entero [ SECONDS ] | ROLLBACK IMMEDIATE | NO_WAIT), todos los identificadores de archivo no transaccionales abiertos se eliminan.  
  
> [!WARNING]  
>  Eliminar los identificadores de archivos abiertos puede hacer que los usuarios pierdan los datos no guardados. Este comportamiento es coherente con el comportamiento del propio sistema de archivos.  
  
 **Efectos de deshabilitar el acceso no transaccional**  
  
 La deshabilitación del acceso no transaccional tiene los siguientes efectos en la visibilidad de los directorios de FileTable del directorio de nivel de base de datos y al acceder a dichos directorios:  
  
-   Cuando el acceso establece en **NONE**, entonces todos los directorios de FileTable y su contenido ha no son accesibles o visibles.  
  
-   Cuando el acceso se establece en **READ_ONLY**, todos los directorios de FileTable y su contenido son también de solo lectura.  
  
 Deshabilitar FILESTREAM en el nivel de instancia tiene los siguientes efectos de los directorios de nivel de base de datos en esa instancia, y en los directorios de FileTable incluidos en ellos:  
  
-   Ninguno de los directorios de nivel de base de datos de la instancia se ve si se deshabilita FILESTREAM en el nivel de instancia.  
  
###  <a name="HowToDisable"></a> Cómo: deshabilitar o volver a habilitar el acceso no transaccional en el nivel de base de datos.  
 Para obtener más información, vea [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
 **Para deshabilitar el acceso no transaccional total**  
 Llame a la instrucción **ALTER DATABASE** y establezca el valor de **NON_TRANSACTED_ACCESS** en **READ_ONLY** o en **OFF**.  
  
```tsql  
-- Disable write access.  
ALTER DATABASE database_name  
    SET FILESTREAM ( NON_TRANSACTED_ACCESS = READ_ONLY );  
GO  
  
-- Disable non-transactional access.  
ALTER DATABASE database_name  
    SET FILESTREAM ( NON_TRANSACTED_ACCESS = OFF );  
GO  
```  
  
 **Para volver a habilitar el acceso no transaccional total**  
 Llame a la instrucción **ALTER DATABASE** y establezca el valor de **NON_TRANSACTED_ACCESS** en **FULL**.  
  
```tsql  
ALTER DATABASE database_name  
    SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL );  
GO  
```  
  
###  <a name="visible"></a> Cómo: asegurar la visibilidad de FileTables en una base de datos  
 Un directorio de nivel de base de datos y sus directorios FileTable cuando se cumplen todas las condiciones siguientes:  
  
1.  FILESTREAM se habilita en el nivel de instancia.  
  
2.  El acceso no transaccional se habilita en el nivel de base de datos.  
  
3.  Un directorio válido se ha especificado en la base de datos.  
  
##  <a name="BasicsEnabling"></a> Deshabilitar y volver a habilitar el espacio de nombres FileTable en el nivel de tabla  
 Si se deshabilita el espacio de nombres de FileTable, se deshabilitan todas las restricciones y los desencadenadores definidos por el sistema que se crearon con FileTable. Esto es útil en los casos en los que FileTable necesite reorganizarse a gran escala mediante operaciones [!INCLUDE[tsql](../../includes/tsql-md.md)] sin tener que aplicar la semántica de FileTable. Aunque estas operaciones pueden dejar FileTable en un estado incoherente, y pueden impedir volver a habilitar el espacio de nombres de FileTable.  
  
 Deshabilitar un espacio de nombres FileTable tiene los siguientes resultados:  
  
-   Las columnas y los datos de FileTable no se quitan físicamente de la tabla.  
  
-   El directorio de FileTable y los archivos y directorios que contiene desaparecen del sistema de archivos y no están disponibles para el acceso E/S de archivos.  
  
-   Las columnas FileTable definidas por el sistema no se pueden quitar ni volver a crear, otramente, sin embargo, se comportan como columnas normales para operaciones DML.  
  
-   Los identificadores de archivos abiertos impiden que las restricciones de FileTable se deshabiliten, puesto que esta operación requiere un bloqueo de esquema de la tabla.  
  
-   La aplicación de toda la semántica de FileTable, incluidas las restricciones y los desencadenadores definidos por el sistema, se detiene después de que se haya deshabilitado el espacio de nombres de FileTable.  
  
 Volver a habilitar un espacio de nombres FileTable tiene los siguientes resultados:  
  
-   Se comprueba la coherencia de FileTable. Si se detectan incoherencias, se produce un error y FileTable permanece deshabilitada; si no, se vuelve a habilitar FileTable.  
  
-   La aplicación de la semántica de FileTable, incluidas las restricciones y los desencadenadores definidos por el sistema, se restaura.  
  
-   El directorio de FileTable y los archivos y directorios que este contiene se vuelve visible en el sistema de archivos y están disponibles para el acceso E/S del archivo.  
  
###  <a name="HowToEnableNS"></a> Cómo: deshabilitar y volver a habilitar el espacio de nombres FileTable en el nivel de tabla  
 Se llama a la instrucción ALTER TABLE con la opción **{ ENABLE | DISABLE } FILETABLE_NAMESPACE** .  
  
 **Para deshabilitar el espacio de nombres de FileTable**  
 ```tsql  
ALTER TABLE filetable_name  
    DISABLE FILETABLE_NAMESPACE;  
GO  
```  
  
 **Para volver a habilitar el espacio de nombres de FileTable**  
 ```tsql  
ALTER TABLE filetable_name  
    ENABLE FILETABLE_NAMESPACE;  
GO  
```  
  
##  <a name="BasicsKilling"></a> Eliminar los identificadores de archivos abiertos asociados con FileTable  
 Los identificadores abiertos en los archivos almacenados en FileTable pueden impedir el acceso exclusivo necesario para ciertas tareas administrativas. Para habilitar tareas urgentes, quizá deba eliminar los identificadores de archivos abiertos asociados con una o más FileTables.  
  
> [!WARNING]  
>  Eliminar los identificadores de archivos abiertos puede hacer que los usuarios pierdan los datos no guardados. Este comportamiento es coherente con el comportamiento del propio sistema de archivos.  
  
###  <a name="HowToListOpen"></a> Cómo: obtener una lista de los identificadores de archivos abiertos asociados con FileTable  
 Consulte la vista de catálogo [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql).  
  
```tsql  
SELECT * FROM sys.dm_filestream_non_transacted_handles;  
GO  
```  
  
###  <a name="HowToKill"></a> Cómo: eliminar los identificadores de archivos abiertos asociados con FileTable  
 Llame al procedimiento almacenado [sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles) con los argumentos apropiados para eliminar todos los identificadores de archivo abiertos de la base de datos o de FileTable, o bien eliminar un identificador específico.  
  
```  
USE database_name;  
  
-- Kill all open handles in all the filetables in the database.  
EXEC sp_kill_filestream_non_transacted_handles;  
GO  
  
-- Kill all open handles in a single filetable.  
EXEC sp_kill_filestream_non_transacted_handles @table_name = 'filetable_name';  
GO  
  
-- Kill a single handle.  
EXEC sp_kill_filestream_non_transacted_handles @handle_id = integer_handle_id;  
GO  
```  
  
###  <a name="HowToIdentifyLocks"></a> Cómo: identificar los bloqueos de FileTables  
 La mayoría de los bloqueos de FileTables corresponden a archivos abiertos por aplicaciones.  
  
 **Para identificar los archivos abiertos y los bloqueos asociados**  
 Combine el campo **request_owner_id** de la vista de administración dinámica [sys.dm_tran_locks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql) con el campo **fcb_id** de [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql). En algunos casos, el bloqueo no se corresponde con ningún identificador de archivos abierto.  
  
```tsql  
SELECT opened_file_name  
    FROM sys.dm_filestream_non_transacted_handles  
    WHERE fcb_id IN  
        ( SELECT request_owner_id FROM sys.dm_tran_locks );  
GO  
```  
  
##  <a name="BasicsSecurity"></a> Seguridad de FileTable  
 Los archivos y directorios almacenados en FileTables están protegidos solo por la seguridad de SQL Server. La seguridad basada en tabla y columna se aplica para el acceso al sistema de archivos así como para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] . No se admiten las API de seguridad del sistema de archivo de Windows ni la configuración de ACL.  
  
 La seguridad y los permisos de acceso que son aplicables a los grupos de archivo y contenedores de FILESTREAM también son aplicables a FileTables, ya que los datos de archivos se almacenan como columna FILESTREAM en FileTable.  
  
 **Seguridad de FileTable y acceso a Transact-SQL**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] acceso a los datos de FileTables está protegido de la misma manera que en cualquier otra tabla. Se realizan comprobaciones de seguridad apropiadas en el nivel de tabla y de columna para cada operación que tenga acceso a los datos o que los modifique.  
  
 **Seguridad de FileTable y acceso al sistema de archivos**  
 Las API del sistema de archivos requieren los permisos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] apropiados para toda la fila de FileTable (es decir, permiso en el nivel de tabla) para abrir un identificador de un archivo o directorio almacenado en FileTable. Si el usuario no tiene el permiso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adecuado en alguna columna de FileTable, se deniega el acceso al sistema de archivos.  
  
##  <a name="OtherBackup"></a> Copia de seguridad y FileTables  
 Cuando se utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para realizar una copia de seguridad en FileTable, se realiza una copia de seguridad de los datos de FILESTREAM con los datos estructurados en la base de datos. Si no desea realizar una copia de seguridad de los datos FILESTREAM con datos relacionales, puede usar una copia de seguridad parcial para excluir los grupos de archivos FILESTREAM.  
  
 **Coherencia transaccional de copias de seguridad de FileTable**  
  
 Muchas herramientas y operaciones administrativas, (incluidas la copia de seguridad, la copia de seguridad de registros y la replicación transaccional) leen datos coherentes transaccionalmente leyendo los registros de transacciones. En este momento, leen los datos FILESTREAM actualizados como parte de una transacción. Cuando no se habilita el acceso no transaccional en el nivel de base de datos, estas herramientas y operaciones funcionan con toda la coherencia transaccional.  
  
 No obstante, cuando se habilita el acceso no transaccional total, una FileTable podría contener datos actualizados más recientemente (a través de una actualización no transaccional) que la transacción que la herramienta o el proceso están leyendo desde el registro de transacciones. Es decir, una operación de restauración “a un momento dado” en una transacción específica puede contener datos de FILESTREAM más recientes que los de esa transacción. Este es el comportamiento esperado cuando se permiten actualizaciones no transaccionales en las FileTables.  
  
##  <a name="Monitor"></a> SQL Server Profiler y FileTables  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler puede capturar las operaciones de apertura y de cierre del archivo de Windows en el resultado de seguimiento de los archivos almacenados en una FileTable.  
  
##  <a name="OtherAuditing"></a> Auditoría y FileTables  
 La FileTable se puede auditar como cualquier otra tabla. Sin embargo, los modelos de acceso de Win32 no son operaciones basadas en conjunto. Una sola acción del sistema de archivos se traduce en varias operaciones DML de Transact-SQL. Por ejemplo, la apertura de un archivo en Microsoft Word se traduce en varias operaciones de apertura, cierre, creación, cambio de nombre o eliminación, así como en las actividades DML de Transact-SQL correspondientes. El resultado son registros de auditoría detallados en los que es difícil poner en correlación los registros entre las acciones del sistema de archivos y los registros de auditoría de DML de Transact-SQL correspondientes.  
  
##  <a name="OtherDBCC"></a> DBCC y FileTables  
 Puede usar DBCC CHECKCONSTRAINTS para validar las restricciones de una FileTable, incluidas las restricciones definidas por el sistema.  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad de FileTable con otras características de SQL Server](filetable-compatibility-with-other-sql-server-features.md)   
 [DDL de FileTable, funciones, procedimientos almacenados y vistas](../views/views.md)  
  
  
