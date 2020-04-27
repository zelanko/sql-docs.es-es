---
title: Base de datos tempdb | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0b1265d3ef58f6ef0946937b15411b0cb79a3c20
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62916895"
---
# <a name="tempdb-database"></a>Base de datos tempdb
  La base de datos del sistema **tempdb** es un recurso global disponible para todos los usuarios conectados a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se utiliza para incluir lo siguiente:  
  
-   Objetos de usuario temporales creados explícitamente como: tablas temporales locales o globales, procedimientos almacenados temporales, variables de tabla o cursores.  
  
-   Objetos internos creados por [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], por ejemplo, tablas de trabajo para almacenar resultados intermedios para colas u ordenación.  
  
-   Versiones de fila generadas por las transacciones de modificación de datos en una base de datos que utiliza transacciones de lectura confirmada que usan transacciones de aislamiento de versiones de fila o de aislamiento de instantáneas.  
  
-   Versiones de fila que se generan mediante transacciones de modificación de datos para características como operaciones de índice en línea, conjuntos de resultados activos múltiples (MARS) y desencadenadores AFTER.  
  
 Las operaciones realizadas en **tempdb** se registran con un nivel mínimo. Esto habilita la reversión de las transacciones. **tempdb** se vuelve a crear cada vez [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se inicia, de modo que el sistema siempre se inicia con una copia limpia de la base de datos. Las tablas y los procedimientos almacenados temporales se quitan automáticamente en la desconexión y ninguna conexión permanece activa cuando se cierra el sistema. Por lo tanto, nunca se guardará nada en **tempdb** de una sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otra. No se permite realizar operaciones de copia de seguridad y restauración en **tempdb**.  
  
## <a name="physical-properties-of-tempdb"></a>Propiedades físicas de tempdb  
 En la tabla siguiente se muestran los valores iniciales de configuración de los archivos de datos y registro de **tempdb** . El tamaño de estos archivos puede variar ligeramente para diferentes ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Archivo|Nombre lógico|Nombre físico|Crecimiento del archivo|  
|----------|------------------|-------------------|-----------------|  
|Datos principales|tempdev|tempdb.mdf|Crecimiento automático del 10 por ciento hasta llenar el disco|  
|Log|templog|templog.ldf|Crecimiento automático del 10 por ciento hasta un máximo de 2 terabytes|  
  
 El tamaño de **tempdb** puede afectar al rendimiento de un sistema. Por ejemplo, si el tamaño de **tempdb** es demasiado pequeño, el procesamiento del sistema puede estar demasiado ocupado con el crecimiento automático de la base de datos para admitir los requisitos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de carga de trabajo cada vez que se inicia. Puede evitar esta sobrecarga si aumenta el tamaño de **tempdb**.  
  
## <a name="performance-improvements-in-tempdb"></a>Mejoras en el rendimiento de tempdb  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el rendimiento de **tempdb** se mejora de las siguientes maneras:  
  
-   Las tablas temporales y las variables de tabla se pueden almacenar en caché. El almacenamiento en caché permite que las operaciones que quitan y crean los objetos temporales se ejecuten muy rápidamente y reduce la contención de la asignación de páginas  
  
-   Se mejora el protocolo de bloqueo temporal de página de asignación. Esto reduce el número de bloqueos temporales UP (de actualización) utilizados.  
  
-   Se reduce la sobrecarga de registro para **tempdb** . Esto reduce el consumo de ancho de banda de E/S del disco en el archivo de registro de **tempdb** .  
  
-   Se ha mejorado el algoritmo para asignar páginas mixtas en **tempdb** .  
  
### <a name="moving-the-tempdb-data-and-log-files"></a>Mover los archivos de datos y registro de tempdb  
 Para trasladar los archivos de datos y de registro de **tempdb** , vea [Move System Databases](system-databases.md).  
  
### <a name="database-options"></a>Opciones de base de datos  
 En la tabla siguiente se muestra el valor predeterminado de cada opción de base de datos en la base de datos **tempdb** y se indica si la opción se puede modificar. Para ver la configuración actual de estas opciones, utilice la vista de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
|Opción de base de datos|Valor predeterminado|Se puede modificar|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|Apagado|Sí|  
|ANSI_NULL_DEFAULT|Apagado|Sí|  
|ANSI_NULLS|Apagado|Sí|  
|ANSI_PADDING|Apagado|Sí|  
|ANSI_WARNINGS|Apagado|Sí|  
|ARITHABORT|Apagado|Sí|  
|AUTO_CLOSE|Apagado|No|  
|AUTO_CREATE_STATISTICS|ACTIVAR|Sí|  
|AUTO_SHRINK|Apagado|No|  
|AUTO_UPDATE_STATISTICS|ACTIVAR|Sí|  
|AUTO_UPDATE_STATISTICS_ASYNC|Apagado|Sí|  
|CHANGE_TRACKING|Apagado|No|  
|CONCAT_NULL_YIELDS_NULL|Apagado|Sí|  
|CURSOR_CLOSE_ON_COMMIT|Apagado|Sí|  
|CURSOR_DEFAULT|GLOBAL|Sí|  
|Opciones de disponibilidad de la base de datos|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|No<br /><br /> Sin<br /><br /> Sin|  
|DATE_CORRELATION_OPTIMIZATION|Apagado|Sí|  
|DB_CHAINING|ACTIVAR|No|  
|ENCRYPTION|Apagado|No|  
|NUMERIC_ROUNDABORT|Apagado|Sí|  
|PAGE_VERIFY|CHECKSUM para las nuevas instalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> NONE para las actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Sí|  
|PARAMETERIZATION|SIMPLE|Sí|  
|QUOTED_IDENTIFIER|Apagado|Sí|  
|READ_COMMITTED_SNAPSHOT|Apagado|No|  
|RECOVERY|SIMPLE|No|  
|RECURSIVE_TRIGGERS|Apagado|Sí|  
|Opciones de Service Broker|ENABLE_BROKER|Sí|  
|TRUSTWORTHY|Apagado|No|  
  
 Para obtener una descripción de estas opciones de la base de datos, vea [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
## <a name="restrictions"></a>Restricciones  
 No se pueden realizar las siguientes operaciones en la base de datos **tempdb** :  
  
-   Agregar grupos de archivos.  
  
-   Realizar una copia de seguridad o restaurar la base de datos.  
  
-   Cambiar intercalaciones. La intercalación predeterminada es la intercalación de servidor.  
  
-   Cambiar el propietario de la base de datos. **tempdb** es propiedad de **SA**.  
  
-   Crear una instantánea de base de datos.  
  
-   Eliminar la base de datos.  
  
-   Quitar el usuario **Guest** de la base de datos.  
  
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
 [Opción SORT_IN_TEMPDB para índices](../indexes/indexes.md)  
  
 [Bases de datos del sistema](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [Mover archivos de base de datos](move-database-files.md)  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con tempdb en SQL Server 2005](https://chresandro.wordpress.com/2014/09/29/working-with-tempdb-in-sql-server-2005/)  
  
  
