---
title: Reorganización y nueva generación de índices | Microsoft Docs
ms.custom: ''
ms.date: 11/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql13.swb.index.rebuild.f1
- sql13.swb.indexproperties.fragmentation.f1
- sql13.swb.index.reorg.f1
helpviewer_keywords:
- large object defragmenting
- indexes [SQL Server], reorganizing
- index reorganization [SQL Server]
- reorganizing indexes
- defragmenting large object data types
- index fragmentation [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- indexes [SQL Server], rebuilding
- defragmenting indexes
- nonclustered indexes [SQL Server], defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
- LOB data [SQL Server], defragmenting
- clustered indexes, defragmenting
ms.assetid: a28c684a-c4e9-4b24-a7ae-e248808b31e9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ceef33cc9f2b463d9d6db18ef8b8a8982d52bf95
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67732388"
---
# <a name="reorganize-and-rebuild-indexes"></a>Reorganizar y volver a generar índices

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

En este artículo se describe cómo reorganizar o volver a generar un índice fragmentado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] modifica los índices automáticamente cada vez que se realizan operaciones de inserción, actualización o eliminación en los datos subyacentes. Con el tiempo, estas modificaciones pueden hacer que la información del índice se disperse por la base de datos (se fragmente). La fragmentación ocurre cuando los índices tienen páginas en las que la ordenación lógica, basada en el valor de clave, no coincide con la ordenación física dentro del archivo de datos. Los índices muy fragmentados pueden reducir el rendimiento de la consulta y ralentizar la respuesta de la aplicación, especialmente durante las operaciones de análisis.

Puede solucionar la fragmentación del índice reorganizándolo o volviéndolo a generar. Para los índices con particiones generados en un esquema de partición, puede usar cualquiera de estos métodos en un índice completo o en una sola partición de un índice.
El proceso de volver a crear un índice quita y vuelve a crear el índice. Quita la fragmentación, utiliza espacio en disco al compactar las páginas según el valor de factor de relleno especificado o existente y vuelve a ordenar las filas del índice en páginas contiguas. Cuando se especifica `ALL`, todos los índices de la tabla se quitan y se vuelven a generar en una única transacción.
La reorganización de un índice usa muy pocos recursos del sistema. Desfragmenta el nivel hoja de los índices agrupados y no clúster de las tablas y las vistas al volver a ordenar físicamente las páginas de nivel hoja para que coincidan con el orden lógico de los nodos hoja, de izquierda a derecha. La reorganización también compacta las páginas de índice. La compactación se basa en el valor de factor de relleno existente.

## <a name="BeforeYouBegin"></a> Antes de comenzar

### <a name="Fragmentation"></a> Detectar la fragmentación

El primer paso necesario para detectar qué método de desfragmentación utilizar es analizar el índice a fin de determinar la magnitud de la fragmentación. Si usa la función del sistema [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md), podrá detectar la fragmentación de un índice específico, de todos los índices de una tabla o vista indexada, de todos los índices de una base de datos o de todos los índices de todas las bases de datos. Para los índices con particiones, **sys.dm_db_index_physical_stats** también proporciona información de la fragmentación para cada partición.

El conjunto de resultados devuelto por la función **sys.dm_db_index_physical_stats** tiene las columnas siguientes.

|columna|Descripción|
|------------|-----------------|
|**avg_fragmentation_in_percent**|Porcentaje de fragmentación lógica (páginas de un índice que no funcionan correctamente).|
|**fragment_count**|Número de fragmentos (páginas hoja físicamente consecutivas) en el índice.|
|**avg_fragment_size_in_pages**|Número promedio de páginas en un fragmento del índice.|

Una vez determinada la magnitud de la fragmentación, utilice la siguiente tabla para determinar el mejor método para corregir la fragmentación propiamente dicha.

|Valor de**avg_fragmentation_in_percent**|Instrucción correctiva|
|-----------------------------------------------|--------------------------|
|> 5% y < = 30%|ALTER INDEX REORGANIZE|
|> 30%|ALTER INDEX REBUILD WITH (ONLINE = ON) <sup>1</sup>|

<sup>1</sup> La regeneración de un índice se puede ejecutar en línea o sin conexión. La reorganización de un índice siempre se ejecuta en línea. Para lograr una disponibilidad similar a la opción de reorganización, debe volver a generar los índices en línea.

Estos valores proporcionan directrices generales para la determinación del punto en el que debe cambiar entre `ALTER INDEX REORGANIZE` y `ALTER INDEX REBUILD`. No obstante, los valores reales pueden variar de un caso a otro. Es importante que experimente la determinación del mejor umbral para su entorno.
Los niveles de fragmentación muy bajos (inferiores al 5 por ciento) normalmente no deben tratarse con ninguno de estos comandos, dado que el beneficio de quitar una cantidad de fragmentación tan pequeña es casi siempre ampliamente superado por el costo de reorganizar o volver a generar el índice. Para obtener más información acerca de `ALTER INDEX REORGANIZE` y `ALTER INDEX REBUILD`, consulte [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).

> [!NOTE]
> Con frecuencia, cuando se vuelven a generar o se reorganizan los índices pequeños no se reduce la fragmentación. Las páginas de índices pequeños a veces se almacenan en extensiones mixtas. Las extensiones mixtas pueden estar compartidas por hasta ocho objetos, de modo que es posible que no se pueda reducir la fragmentación en un índice pequeño después de reorganizar o volver a generar dicho índice.

### <a name="Restrictions"></a> Limitaciones y restricciones

Los índices que tienen más de 128 extensiones se vuelven a generar en dos fases independientes: lógica y física. En la fase lógica, las unidades de asignación existentes que utiliza el índice están señaladas para cancelación de asignación las filas de datos se copian y ordenan y luego se mueven a las nuevas unidades de asignación creadas para almacenar el índice recompilado. En la fase física, las unidades de asignación previamente señaladas para cancelación de asignación se quitan físicamente de las transacciones breves que se realizan en segundo plano y no requieren demasiados bloqueos. Para obtener más información acerca de las extensiones, consulte la [Guía de arquitectura de páginas y extensiones](../../relational-databases/pages-and-extents-architecture-guide.md).

La instrucción `ALTER INDEX REORGANIZE` requiere que el archivo de datos que contiene el índice tenga espacio disponible, ya que la operación solo puede asignar páginas de trabajo temporales en el mismo archivo, no en otro archivo del grupo de archivos. Debido a esto, aunque el grupo de archivos tenga páginas libres disponibles, puede que al usuario le siga apareciendo el error 1105: `Could not allocate space for object '###' in database '###' because the '###' filegroup is full. Create disk space by deleting unneeded files, dropping objects in the filegroup, adding additional files to the filegroup, or setting autogrowth on for existing files in the filegroup.`

Se pueden crear y regenerar índices no alineados en una tabla con más de 1000 particiones, pero no se recomienda. Si se hace, se puede degradar el rendimiento o consumir excesiva memoria durante estas operaciones.

No es posible volver a organizar o generar un índice si el grupo de archivos en el que se encuentra está sin conexión o está definido como de solo lectura. Cuando se especifica la palabra clave `ALL` y hay uno o más índices en un grupo de archivos sin conexión o de solo lectura, se produce un error en la instrucción.

> [!IMPORTANT]
> Cuando se crea o se vuelve a generar un índice en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], las estadísticas se crean o se actualizan examinando todas las filas de la tabla.
>
> Pero a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], las estadísticas no se crean o actualizan examinando todas las filas de la tabla cuando se crea o se vuelve a generar un índice con particiones. En su lugar, el optimizador de consultas usa el algoritmo de muestreo predeterminado para generar estas estadísticas. Para obtener estadísticas sobre índices con particiones examinando todas las filas de la tabla, use `CREATE STATISTICS` o `UPDATE STATISTICS` con la cláusula `FULLSCAN`.

### <a name="Security"></a> Seguridad

#### <a name="Permissions"></a> Permisos

Requiere el permiso ALTER en la tabla o la vista. El usuario debe ser miembro de al menos uno de los siguientes roles:

- Rol de base de datos **db_ddladmin**<sup>1</sup>
- Rol de base de datos **db_owner**
- Rol de servidor **sysadmin**

<sup>1</sup>El rol de base de datos **db_ddladmin** es el que tiene [menos privilegios](/windows-server/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models).

## <a name="SSMSProcedureFrag"></a>Comprobación de la fragmentación de un índice con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]

### <a name="to-check-the-fragmentation-of-an-index"></a>Para comprobar la fragmentación de un índice

1. En el Explorador de objetos, expanda la base de datos que contiene la tabla en la que quiera comprobar la fragmentación de un índice.
2. Expanda la carpeta **Tablas** .
3. Expanda la tabla en la que quiera comprobar la fragmentación de un índice.
4. Expanda la carpeta **Índices** .
5. Haga clic con el botón derecho en el índice en el que quiere comprobar la fragmentación y seleccione **Propiedades**.
6. Bajo **Seleccionar una página**, seleccione **Fragmentación**.

   La siguiente información está disponible en la página **Fragmentación** :

   **Llenado de página**: indica el promedio de llenado de las páginas de índice como un porcentaje. 100% indica que las páginas de índice están completamente llenas. 50% indica que, como promedio, las páginas de índice están llenas a la mitad.

   **Fragmentación total**: porcentaje de fragmentación lógica. Indica el número de páginas de un índice que no están almacenadas en orden.

   **Promedio de tamaño de fila**: tamaño promedio de una fila de nivel hoja.

   **Profundidad**: número de niveles del índice, incluido el nivel hoja.

   **Registros reenviados**: número de registros de un montón que han reenviado punteros a otra ubicación de datos. Este estado se produce durante una actualización, cuando no existe suficiente espacio para almacenar la nueva fila en la ubicación original.

   **Filas fantasma**: número de filas marcadas como eliminadas que todavía no se han quitado. Estas filas se quitarán en un subproceso de limpieza, cuando el servidor no esté ocupado. Este valor no incluye las filas que se retienen debido a una transacción pendiente de aislamiento de instantáneas.

   **Tipo de índice**: el tipo de índice. Los valores posibles son **Índice clúster**, **Índice no clúster**y **XML principal**. Las tablas también se pueden almacenar como un montón (sin índices), pero en tal caso la página Propiedades del índice no puede abrirse.

   **Filas de nivel de hoja**: el número de filas de nivel de hoja.

   **Tamaño máximo de la fila**: el tamaño máximo de la fila de nivel de hoja.

   **Tamaño mínimo de la fila**: el tamaño mínimo de la fila de nivel de hoja.

   **Páginas**: el número total de páginas de datos.

   **Id. de partición**: el id. de partición del árbol B que contiene el índice.

   **Filas fantasma de la versión**: el número de registros fantasma que se retienen debido a una transacción de aislamiento de instantánea pendiente.

## <a name="TsqlProcedureFrag"></a>Comprobación de la fragmentación de un índice con [!INCLUDE[tsql](../../includes/tsql-md.md)]

### <a name="to-check-the-fragmentation-of-an-index"></a>Para comprobar la fragmentación de un índice

En el ejemplo siguiente, se encuentra el porcentaje de fragmentación promedio de todos los índices de la tabla HumanResources.Employee de la base de datos de AdventureWorks.

```sql
SELECT a.index_id, name, avg_fragmentation_in_percent
   FROM sys.dm_db_index_physical_stats
      (DB_ID
         (N'AdventureWorks2012')
         , OBJECT_ID(N'HumanResources.Employee')
         , NULL
         , NULL
         , NULL) AS a
   JOIN sys.indexes AS b
      ON a.object_id = b.object_id
      AND a.index_id = b.index_id;
```

La instrucción anterior devuelve un conjunto de resultados similar al siguiente.

```cmd
index_id    name                                                  avg_fragmentation_in_percent
----------- ----------------------------------------------------- ----------------------------
1           PK_Employee_BusinessEntityID                          0
2           IX_Employee_OrganizationalNode                        0
3           IX_Employee_OrganizationalLevel_OrganizationalNode    0
5           AK_Employee_LoginID                                   66.6666666666667
6           AK_Employee_NationalIDNumber                          50
7           AK_Employee_rowguid                                   0

(6 row(s) affected)
```

Para más información, consulte [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md).

## <a name="SSMSProcedureReorg"></a> Eliminación de la fragmentación con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]

### <a name="to-reorganize-or-rebuild-an-index"></a>Para reorganizar o volver a generar un índice

1. En el Explorador de objetos, expanda la base de datos que contiene la tabla en la que desea reorganizar un índice.
2. Expanda la carpeta **Tablas** .
3. Expanda la tabla en la que desea reorganizar un índice.
4. Expanda la carpeta **Índices** .
5. Haga clic con el botón derecho en el índice que quiera reorganizar y seleccione **Reorganizar**.
6. En el cuadro de diálogo **Reorganizar índices** , compruebe que el índice correcto se encuentra en la cuadrícula **Índices que se van a reorganizar** y haga clic en **Aceptar**.
7. Active la casilla **Compactar datos de columnas de objetos de gran tamaño** para especificar que se compacten también todas las páginas que contengan datos de objetos grandes (LOB).
8. Haga clic en **Aceptar.**

### <a name="to-reorganize-all-indexes-in-a-table"></a>Para reorganizar todos los índices de una tabla

1. En el Explorador de objetos, expanda la base de datos que contiene la tabla en la que desea reorganizar los índices.
2. Expanda la carpeta **Tablas** .
3. Expanda la tabla en la que desea reorganizar los índices.
4. Haga clic con el botón derecho en la carpeta **Índices** y seleccione **Reorganizar todo**.
5. En el cuadro de diálogo **Reorganizar índices** , compruebe que los índices adecuados están en **Índices que se van a reorganizar**. Para quitar un índice de la cuadrícula **Índices que se van a reorganizar** , seleccione el índice y, a continuación, presione la tecla SUPR.
6. Active la casilla **Compactar datos de columnas de objetos de gran tamaño** para especificar que se compacten también todas las páginas que contengan datos de objetos grandes (LOB).
7. Haga clic en **Aceptar.**

### <a name="to-rebuild-an-index"></a>Para volver a generar un índice

1. En el Explorador de objetos, expanda la base de datos que contiene la tabla en la que desea reorganizar un índice.
2. Expanda la carpeta **Tablas** .
3. Expanda la tabla en la que desea reorganizar un índice.
4. Expanda la carpeta **Índices** .
5. Haga clic con el botón derecho en el índice que quiera reorganizar y seleccione **Volver a generar**.
6. En el cuadro de diálogo **Volver a generar índices** , compruebe que el índice correcto se encuentra en la cuadrícula **Índices que se van a volver a generar** y haga clic en **Aceptar**.
7. Active la casilla **Compactar datos de columnas de objetos de gran tamaño** para especificar que se compacten también todas las páginas que contengan datos de objetos grandes (LOB).
8. Haga clic en **Aceptar.**

## <a name="TsqlProcedureReorg"></a> Eliminación de la fragmentación con [!INCLUDE[tsql](../../includes/tsql-md.md)]

### <a name="to-reorganize-a-fragmented-index"></a>Para reorganizar un índice fragmentado

El ejemplo siguiente reorganiza el índice `IX_Employee_OrganizationalLevel_OrganizationalNode` de la tabla `HumanResources.Employee` en la base de datos de AdventureWorks.

```sql
ALTER INDEX IX_Employee_OrganizationalLevel_OrganizationalNode
   ON HumanResources.Employee
   REORGANIZE
;
```

### <a name="to-reorganize-all-indexes-in-a-table"></a>Para reorganizar todos los índices de una tabla

En el ejemplo siguiente, se reorganizan todos los índices de la tabla HumanResources.Employee de la base de datos de AdventureWorks.

```sql
ALTER INDEX ALL ON HumanResources.Employee
   REORGANIZE
;
```

### <a name="to-rebuild-a-fragmented-index"></a>Para volver a generar un índice fragmentado

En el ejemplo siguiente se recompila un índice único en la tabla `Employee` de la base de datos de AdventureWorks.

[!code-sql[IndexDDL#AlterIndex1](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_1.sql)]

### <a name="to-rebuild-all-indexes-in-a-table"></a>Para volver a generar todos los índices de una tabla

El ejemplo siguiente recompila todos los índices asociados con la tabla de la base de datos de AdventureWorks mediante la palabra clave `ALL`. Se especifican tres opciones.

[!code-sql[IndexDDL#AlterIndex2](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_2.sql)]

Para más información, consulte [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md).

### <a name="automatic-index-and-statistics-management"></a>Administración automática de índice y estadísticas

Aproveche soluciones como la [desfragmentación de índice adaptable](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) para administrar automáticamente las actualizaciones de estadísticas y la desfragmentación de índices para una o varias bases de datos. Este procedimiento elige automáticamente si se debe volver a generar o reorganizar un índice según su nivel de fragmentación, entre otros parámetros y actualiza las estadísticas con un umbral lineal.

## <a name="see-also"></a>Consulte también

- [Guía de diseño de índices de SQL Server](../../relational-databases/sql-server-index-design-guide.md)
- [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)
- [Desfragmentación de índice adaptable](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)
- [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)
- [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)
