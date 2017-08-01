---
title: Base de datos tempdb | Microsoft Docs
ms.custom: 
ms.date: 03/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
caps.latest.revision: 66
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 003196d8c30ca45c54750587c03c8d7d6e5a358d
ms.contentlocale: es-es
ms.lasthandoff: 07/31/2017

---
# <a name="tempdb-database"></a>Base de datos tempdb
  La base de datos del sistema **tempdb** es un recurso global disponible para todos los usuarios conectados a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se utiliza para incluir lo siguiente:  
  
-   Objetos de usuario temporales creados explícitamente como: tablas temporales locales o globales, procedimientos almacenados temporales, variables de tabla o cursores.  
  
-   Objetos internos creados por [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], por ejemplo, tablas de trabajo para almacenar resultados intermedios para colas u ordenación.  
  
-   Versiones de fila generadas por las transacciones de modificación de datos en una base de datos que utiliza transacciones de lectura confirmada que usan transacciones de aislamiento de versiones de fila o de aislamiento de instantáneas.  
  
-   Versiones de fila que se generan mediante transacciones de modificación de datos para características como operaciones de índice en línea, conjuntos de resultados activos múltiples (MARS) y desencadenadores AFTER.  
  
 Las operaciones realizadas en **tempdb** se registran con un nivel mínimo. Esto habilita la reversión de las transacciones. **tempdb** se vuelve a crear cada vez que se inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , de forma que el sistema siempre se inicia con una copia limpia de la base de datos. Las tablas y los procedimientos almacenados temporales se quitan automáticamente en la desconexión y ninguna conexión permanece activa cuando se cierra el sistema. Por tanto, en la base de datos **tempdb** no hay nada que deba guardarse de una a otra sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No se permite realizar operaciones de copia de seguridad y restauración en **tempdb**.  
  
## <a name="physical-properties-of-tempdb"></a>Propiedades físicas de tempdb  
 En la tabla siguiente se muestran los valores iniciales de configuración de los archivos de datos y registro de **tempdb** . El tamaño de estos archivos puede variar ligeramente para diferentes ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Archivo|Nombre lógico|Nombre físico|Tamaño inicial|Crecimiento del archivo|  
|----------|------------------|-------------------|------------------|-----------------|  
|Datos principales|tempdev|tempdb.mdf|8 megabytes|Crecimiento automático de 64 MB hasta llenar el disco.|  
|Archivos de datos secundarios*|temp#|tempdb_mssql_ # .ndf|8 megabytes|Crecimiento automático de 64 MB hasta llenar el disco.|  
|Log|templog|templog.ldf|8 megabytes|Crecimiento automático de 64 megabytes hasta un máximo de 2 terabytes.|  
  
 \* El número de archivos depende del número de núcleos (lógicos) del equipo. El valor será el número de núcleos u 8, lo que sea menor.   
El valor predeterminado para el número de archivos de datos se basa en las directrices [KB 2154845](https://support.microsoft.com/en-us/kb/2154845/).  
  
## <a name="performance-improvements-in-tempdb"></a>Mejoras en el rendimiento de tempdb  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el rendimiento de **tempdb** se mejora de las siguientes maneras:  
  
-   Las tablas temporales y las variables de tabla se pueden almacenar en caché. El almacenamiento en caché permite que las operaciones que quitan y crean los objetos temporales se ejecuten muy rápidamente y reduce la contención de la asignación de páginas  
  
-   Se mejora el protocolo de bloqueo temporal de página de asignación. Esto reduce el número de bloqueos temporales UP (de actualización) utilizados.  
  
-   Se reduce la sobrecarga de registro para **tempdb** . Esto reduce el consumo de ancho de banda de E/S del disco en el archivo de registro de **tempdb** .  
  
-   El programa de instalación agrega varios archivos de datos tempdb durante una instalación nueva de la instancia. Esta tarea puede realizarse con el nuevo control de entrada de la IU en la sección **Configuración del motor de base de datos** y un parámetro de línea de comandos /SQLTEMPDBFILECOUNT. De manera predeterminada, la configuración agregará tantos archivos tempdb como el número de CPU u 8, lo que sea menor.  
  
-   Si hay varios archivos de datos **tempdb** , todos crecerán automáticamente al mismo tiempo y la misma cantidad en función de la configuración de crecimiento.  La marca de seguimiento 1117 ya no es necesaria.  
  
-   Todas las asignaciones de **tempdb** usarán extensiones uniformes. La marca de seguimiento 1118 ya no es necesaria.  
  
-   Para el grupo de archivos principal, la propiedad AUTOGROW_ALL_FILES se activa y la propiedad no se puede modificar.  
  
### <a name="moving-the-tempdb-data-and-log-files"></a>Mover los archivos de datos y registro de tempdb  
 Para mover los archivos de registro y de datos de **tempdb** , vea [Mover bases de datos del sistema](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options"></a>Opciones de base de datos  
 En la siguiente tabla se muestra el valor predeterminado de las opciones de base de datos de la base de datos **tempdb** y se indica si la opción se puede modificar. Para ver la configuración actual de estas opciones, utilice la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Opción de base de datos|Valor predeterminado|Se puede modificar|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|Sí|  
|ANSI_NULL_DEFAULT|OFF|Sí|  
|ANSI_NULLS|OFF|Sí|  
|ANSI_PADDING|OFF|Sí|  
|ANSI_WARNINGS|OFF|Sí|  
|ARITHABORT|OFF|Sí|  
|AUTO_CLOSE|OFF|No|  
|AUTO_CREATE_STATISTICS|ON|Sí|  
|AUTO_SHRINK|OFF|No|  
|AUTO_UPDATE_STATISTICS|ON|Sí|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sí|  
|CHANGE_TRACKING|OFF|No|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sí|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sí|  
|CURSOR_DEFAULT|GLOBAL|Sí|  
|Opciones de disponibilidad de la base de datos|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|No<br /><br /> No<br /><br /> No|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sí|  
|DB_CHAINING|ON|No|  
|ENCRYPTION|OFF|No|  
|MIXED_PAGE_ALLOCATION|OFF|No|  
|NUMERIC_ROUNDABORT|OFF|Sí|  
|PAGE_VERIFY|CHECKSUM para las nuevas instalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> NONE para las actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Sí|  
|PARAMETERIZATION|SIMPLE|Sí|  
|QUOTED_IDENTIFIER|OFF|Sí|  
|READ_COMMITTED_SNAPSHOT|OFF|No|  
|RECOVERY|SIMPLE|No|  
|RECURSIVE_TRIGGERS|OFF|Sí|  
|Opciones de Service Broker|ENABLE_BROKER|Sí|  
|TRUSTWORTHY|OFF|No|  
  
 Para obtener una descripción de estas opciones de la base de datos, vea [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="restrictions"></a>Restricciones  
 En la base de datos **tempdb** no se pueden realizar las siguientes operaciones:  
  
-   Agregar grupos de archivos.  
  
-   Realizar una copia de seguridad o restaurar la base de datos.  
  
-   Cambiar intercalaciones. La intercalación predeterminada es la intercalación de servidor.  
  
-   Cambiar el propietario de la base de datos. **tempdb** es propiedad de **sa**.  
  
-   Crear una instantánea de base de datos.  
  
-   Eliminar la base de datos.  
  
-   Eliminar el usuario **guest** de la base de datos.  
  
-   Habilitar el mecanismo de captura de cambios en los datos.  
  
-   Participar en el reflejo de la base de datos.  
  
-   Quitar el grupo de archivos principal, el archivo de datos principal o el archivo de registro.  
  
-   Cambiar el nombre de la base de datos o del grupo de archivos principal.  
  
-   Ejecutar DBCC CHECKALLOC.  
  
-   Ejecutar DBCC CHECKCATALOG.  
  
-   Establecer la base de datos en OFFLINE.  
  
-   Establecer la base de datos o el grupo de archivos principal en READ_ONLY.  
  
## <a name="permissions"></a>Permisos  
 Cualquier usuario puede crear objetos temporales en tempdb. Los usuarios solo pueden acceder a sus propios objetos, a menos que reciban permisos adicionales. Es posible revocar el permiso de conexión a tempdb para impedir que un usuario use tempdb, pero no es una práctica recomendada ya que algunas operaciones rutinarias necesitan el uso de tempdb.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Opción SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)  
  
 [Bases de datos del sistema](../../relational-databases/databases/system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
 [Mover archivos de base de datos](../../relational-databases/databases/move-database-files.md)  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con tempdb en SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81216)  
  
  

