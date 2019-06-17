---
title: Reorganización y nueva generación de índices | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.indexproperties.fragmentation.f1
- sql12.swb.index.reorg.f1
- sql12.swb.index.rebuild.f1
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
ms.openlocfilehash: af52376ae4749d42c8d746a64518632e6a047591
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63036239"
---
# <a name="reorganize-and-rebuild-indexes"></a>Reorganizar y volver a generar índices
  En este tema se describe cómo reorganizar o volver a generar un índice fragmentado en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] mantiene los índices automáticamente cada vez que se realizan operaciones de inserción, actualización o eliminación en los datos subyacentes. Con el tiempo, estas modificaciones pueden hacer que la información del índice se disperse por la base de datos (se fragmente). La fragmentación ocurre cuando los índices tienen páginas en las que la ordenación lógica, basada en el valor de clave, no coincide con la ordenación física dentro del archivo de datos. Los índices muy fragmentados pueden reducir el rendimiento de la consulta y ralentizar la respuesta de la aplicación.  
  
 Puede solucionar la fragmentación del índice reorganizándolo o volviéndolo a generar. Para los índices con particiones generados en un esquema de partición, puede usar cualquiera de estos métodos en un índice completo o en una sola partición de un índice. El proceso de volver a crear un índice quita y vuelve a crear el índice. Quita la fragmentación, utiliza espacio en disco al compactar las páginas según el valor de factor de relleno especificado o existente y vuelve a ordenar las filas del índice en páginas contiguas. Cuando se especifica ALL, todos los índices de la tabla se quitan y se vuelven a generar en una única transacción. La reorganización de un índice usa muy pocos recursos del sistema. Desfragmenta el nivel hoja de los índices agrupados y no clúster de las tablas y las vistas al volver a ordenar físicamente las páginas de nivel hoja para que coincidan con el orden lógico de los nodos hoja, de izquierda a derecha. La reorganización también compacta las páginas de índice. La compactación se basa en el valor de factor de relleno existente.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Detectar la fragmentación](#Fragmentation)  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para comprobar la fragmentación de un índice, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedureFrag)  
  
     [Transact-SQL](#TsqlProcedureFrag)  
  
-   **Para reorganizar o volver a generar un índice, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedureReorg)  
  
     [Transact-SQL](#TsqlProcedureReorg)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Fragmentation"></a> Detectar la fragmentación  
 El primer paso necesario para detectar qué método de desfragmentación utilizar es analizar el índice a fin de determinar la magnitud de la fragmentación. Si usa la función del sistema [sys.dm_db_index_physical_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql), podrá detectar la fragmentación de un índice específico, de todos los índices de una tabla o vista indexada, de todos los índices de una base de datos o de todos los índices de todas las bases de datos. Para los índices con particiones, **sys.dm_db_index_physical_stats** también proporciona información de la fragmentación para cada partición.  
  
 El conjunto de resultados devuelto por la función **sys.dm_db_index_physical_stats** tiene las columnas siguientes.  
  
|columna|Descripción|  
|------------|-----------------|  
|**avg_fragmentation_in_percent**|Porcentaje de fragmentación lógica (páginas de un índice que no funcionan correctamente).|  
|**fragment_count**|Número de fragmentos (páginas hoja físicamente consecutivas) en el índice.|  
|**avg_fragment_size_in_pages**|Número promedio de páginas en un fragmento del índice.|  
  
 Una vez determinada la magnitud de la fragmentación, utilice la siguiente tabla para determinar el mejor método para corregir la fragmentación propiamente dicha.  
  
|Valor de**avg_fragmentation_in_percent**|Instrucción correctiva|  
|-----------------------------------------------|--------------------------|  
|> 5% y \< = 30%|ALTER INDEX REORGANIZE|  
|> 30%|ALTER INDEX REBUILD WITH (ONLINE = ON)*|  
  
 \* La regeneración de un índice se puede ejecutar en línea o sin conexión. La reorganización de un índice siempre se ejecuta en línea. Para lograr una disponibilidad similar a la opción de reorganización, debe volver a generar los índices en línea.  
  
 Estos valores proporcionan directrices generales para la determinación del punto en el que debe cambiar entre ALTER INDEX REORGANIZE y ALTER INDEX REBUILD. No obstante, los valores reales pueden variar de un caso a otro. Es importante que experimente la determinación del mejor umbral para su entorno. Los niveles de fragmentación muy bajos (inferiores al 5 por ciento) no deben tratarse con ninguno de estos comandos, dado que el beneficio de quitar una cantidad de fragmentación tan pequeña es casi siempre ampliamente superado por el costo de reorganizar o volver a generar el índice.  
  
> [!NOTE]  
>  En general, la fragmentación en índices pequeños normalmente no se puede controlar. Las páginas de índices pequeños se almacenan en extensiones mixtas. Las extensiones mixtas pueden estar compartidas por hasta ocho objetos, de modo que es posible que no se pueda reducir la fragmentación en un índice pequeño después de reorganizar o volver a generar dicho índice.  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Los índices que tienen más de 128 extensiones se vuelven a generar en dos fases independientes: lógica y física. En la fase lógica, las unidades de asignación existentes que utiliza el índice están señaladas para cancelación de asignación las filas de datos se copian y ordenan y luego se mueven a las nuevas unidades de asignación creadas para almacenar el índice recompilado. En la fase física, las unidades de asignación previamente señaladas para cancelación de asignación se quitan físicamente de las transacciones breves que se realizan en segundo plano y no requieren demasiados bloqueos.  
  
-   Las opciones del índice no se pueden especificar al reorganizar un índice.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla o la vista. El usuario debe ser miembro del rol fijo de servidor **sysadmin** o de los roles fijos de base de datos **db_ddladmin** y **db_owner** .  
  
##  <a name="SSMSProcedureFrag"></a> Usar SQL Server Management Studio  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>Para comprobar la fragmentación de un índice  
  
1.  En el Explorador de objetos, expanda la base de datos que contiene la tabla en la que quiera comprobar la fragmentación de un índice.  
  
2.  Expanda la carpeta **Tablas** .  
  
3.  Expanda la tabla en la que quiera comprobar la fragmentación de un índice.  
  
4.  Expanda la carpeta **Índices** .  
  
5.  Haga clic con el botón derecho en el índice en el que quiere comprobar la fragmentación y seleccione **Propiedades**.  
  
6.  Bajo **Seleccionar una página**, seleccione **Fragmentación**.  
  
     La siguiente información está disponible en la página **Fragmentación** :  
  
     **Llenado de página**  
     Indica el promedio de llenado de las páginas de índice como un porcentaje. 100% indica que las páginas de índice están completamente llenas. 50% indica que, como promedio, las páginas de índice están llenas a la mitad.  
  
     **Fragmentación total**  
     Porcentaje de fragmentación lógica. Indica el número de páginas de un índice que no están almacenadas en orden.  
  
     **Promedio de tamaño de fila**  
     Tamaño medio de una fila de nivel hoja.  
  
     **Profundidad**  
     Número de niveles del índice, incluido el nivel hoja.  
  
     **Registros reenviados**  
     Número de registros de un montón que han reenviado punteros a otra ubicación de datos. Este estado se produce durante una actualización, cuando no existe suficiente espacio para almacenar la nueva fila en la ubicación original.  
  
     **Filas fantasma**  
     Número de filas marcadas como eliminadas que todavía no se han quitado. Estas filas se quitarán en un subproceso de limpieza, cuando el servidor no esté ocupado. Este valor no incluye las filas que se retienen debido a una transacción pendiente de aislamiento de instantáneas.  
  
     **Tipo de índice**  
     Tipo de índice. Los valores posibles son **Índice clúster**, **Índice no clúster**y **XML principal**. Las tablas también se pueden almacenar como un montón (sin índices), pero en tal caso la página Propiedades del índice no puede abrirse.  
  
     **Filas de nivel de hoja**  
     Número de filas de nivel hoja.  
  
     **Tamaño máximo de la fila**  
     Tamaño máximo de la fila de nivel de hoja.  
  
     **Tamaño mínimo de la fila**  
     Tamaño mínimo de la fila de nivel de hoja.  
  
     **Páginas**  
     Número total de páginas de datos.  
  
     **Id. de partición**  
     Id. de partición del árbol b que contiene el índice.  
  
     **Filas fantasma de la versión**  
     Número de registros fantasma que se retienen debido a una transacción de aislamiento de instantánea pendiente.  
  
##  <a name="TsqlProcedureFrag"></a> Usar Transact-SQL  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>Para comprobar la fragmentación de un índice  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Find the average fragmentation percentage of all indexes  
    -- in the HumanResources.Employee table.   
    SELECT a.index_id, name, avg_fragmentation_in_percent  
    FROM sys.dm_db_index_physical_stats (DB_ID(N'AdventureWorks2012'), OBJECT_ID(N'HumanResources.Employee'), NULL, NULL, NULL) AS a  
        JOIN sys.indexes AS b ON a.object_id = b.object_id AND a.index_id = b.index_id;   
    GO  
    ```  
  
     La instrucción anterior puede devolver un conjunto de resultados similar al siguiente:  
  
    ```  
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
  
 Para obtener más información, vea [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql).  
  
##  <a name="SSMSProcedureReorg"></a> Usar SQL Server Management Studio  
  
#### <a name="to-reorganize-or-rebuild-an-index"></a>Para reorganizar o volver a generar un índice  
  
1.  En el Explorador de objetos, expanda la base de datos que contiene la tabla en la que desea reorganizar un índice.  
  
2.  Expanda la carpeta **Tablas** .  
  
3.  Expanda la tabla en la que desea reorganizar un índice.  
  
4.  Expanda la carpeta **Índices** .  
  
5.  Haga clic con el botón derecho en el índice que quiera reorganizar y seleccione **Reorganizar**.  
  
6.  En el cuadro de diálogo **Reorganizar índices** , compruebe que el índice correcto se encuentra en la cuadrícula **Índices que se van a reorganizar** y haga clic en **Aceptar**.  
  
7.  Active la casilla **Compactar datos de columnas de objetos de gran tamaño** para especificar que se compacten también todas las páginas que contengan datos de objetos grandes (LOB).  
  
8.  Haga clic en **Aceptar.**  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>Para reorganizar todos los índices de una tabla  
  
1.  En el Explorador de objetos, expanda la base de datos que contiene la tabla en la que desea reorganizar los índices.  
  
2.  Expanda la carpeta **Tablas** .  
  
3.  Expanda la tabla en la que desea reorganizar los índices.  
  
4.  Haga clic con el botón derecho en la carpeta **Índices** y seleccione **Reorganizar todo**.  
  
5.  En el cuadro de diálogo **Reorganizar índices** , compruebe que los índices adecuados están en **Índices que se van a reorganizar**. Para quitar un índice de la cuadrícula **Índices que se van a reorganizar** , seleccione el índice y, a continuación, presione la tecla SUPR.  
  
6.  Active la casilla **Compactar datos de columnas de objetos de gran tamaño** para especificar que se compacten también todas las páginas que contengan datos de objetos grandes (LOB).  
  
7.  Haga clic en **Aceptar.**  
  
#### <a name="to-rebuild-an-index"></a>Para volver a generar un índice  
  
1.  En el Explorador de objetos, expanda la base de datos que contiene la tabla en la que desea reorganizar un índice.  
  
2.  Expanda la carpeta **Tablas** .  
  
3.  Expanda la tabla en la que desea reorganizar un índice.  
  
4.  Expanda la carpeta **Índices** .  
  
5.  Haga clic con el botón derecho en el índice que quiera reorganizar y seleccione **Reorganizar**.  
  
6.  En el cuadro de diálogo **Volver a generar índices** , compruebe que el índice correcto se encuentra en la cuadrícula **Índices que se van a volver a generar** y haga clic en **Aceptar**.  
  
7.  Active la casilla **Compactar datos de columnas de objetos de gran tamaño** para especificar que se compacten también todas las páginas que contengan datos de objetos grandes (LOB).  
  
8.  Haga clic en **Aceptar.**  
  
##  <a name="TsqlProcedureReorg"></a> Usar Transact-SQL  
  
#### <a name="to-reorganize-a-defragmented-index"></a>Para reorganizar un índice desfragmentado  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize the IX_Employee_OrganizationalLevel_OrganizationalNode index on the HumanResources.Employee table.   
  
    ALTER INDEX IX_Employee_OrganizationalLevel_OrganizationalNode ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>Para reorganizar todos los índices de una tabla  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize all indexes on the HumanResources.Employee table.  
    ALTER INDEX ALL ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-rebuild-a-defragmented-index"></a>Para volver a generar un índice desfragmentado  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En el ejemplo se vuelve a generar un único índice en la tabla `Employee` .  
  
     [!code-sql[IndexDDL#AlterIndex1](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex1)]  
  
#### <a name="to-rebuild-all-indexes-in-a-table"></a>Para volver a generar todos los índices de una tabla  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el ejemplo siguiente en la ventana de consulta. En el ejemplo se especifica la palabra clave `ALL`. Así se regeneran todos los índices asociados a la tabla. Se especifican tres opciones.  
  
     [!code-sql[IndexDDL#AlterIndex2](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex2)]  
  
 Para obtener más información, vea [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [Prácticas recomendadas de desfragmentación de índices de Microsoft SQL Server 2000](https://technet.microsoft.com/library/cc966523.aspx)  
  
  
