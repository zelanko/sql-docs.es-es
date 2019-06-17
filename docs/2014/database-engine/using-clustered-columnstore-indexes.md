---
title: El uso de índices de almacén de columnas agrupado | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 5af6b91c-724f-45ac-aff1-7555014914f4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1e65c3e277eb9a3e5e3703525b9c1ac06b423c96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773747"
---
# <a name="using-clustered-columnstore-indexes"></a>Usar índices clúster de almacén de columnas
  Tareas para utilizar índices clúster de almacén de columnas en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Para obtener información general acerca de los índices de almacén de columnas, vea [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md).  
  
 Para obtener información acerca de los índices clúster de almacén de columnas, vea [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md).  
  
## <a name="contents"></a>Contenido  
  
-   [Crear un índice agrupado de almacén de columnas](#create)  
  
-   [Quitar un índice de almacén de columnas en clúster](#drop)  
  
-   [Cargar datos en un índice agrupado de almacén de columnas](#load)  
  
-   [Cambiar los datos de un índice agrupado de almacén de columnas](#change)  
  
-   [Volver a generar un índice agrupado de almacén de columnas](#rebuild)  
  
-   [Reorganizar un índice agrupado de almacén de columnas](#reorganize)  
  
##  <a name="create"></a> Crear un índice agrupado de almacén de columnas  
 Para crear un índice agrupado, primero cree una tabla de almacén de filas como un índice agrupado o montón y, a continuación, utilice el [CREATE CLUSTERED COLUMNSTORE INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql) instrucción para convertir la tabla en un clúster índice de almacén de columnas. Si desea que el índice clúster de almacén de columnas tenga el mismo nombre que el índice clúster, use la opción DROP_EXISTING.  
  
 En este ejemplo se crea una tabla como un montón y después se convierte en un índice clúster de almacén de columnas denominado cci_Simple. Esto cambia el almacenamiento de la tabla de un almacén de filas a un almacén de columnas.  
  
```  
CREATE TABLE T1(  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_T1 ON T1;  
GO  
```  
  
 Para obtener más ejemplos, vea la sección de ejemplos en [CREATE CLUSTERED COLUMNSTORE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql).  
  
##  <a name="drop"></a> Quitar un índice de almacén de columnas en clúster  
 Use la [DROP INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/drop-index-transact-sql) instrucción para quitar un índice de almacén de columnas agrupado. Esta operación quitará el índice y convertirá la tabla de almacén de columnas en un montón de almacenes de filas.  
  
##  <a name="load"></a> Cargar datos en un índice agrupado de almacén de columnas  
 Puede agregar datos a un índice clúster de almacén de columnas existente mediante cualquiera de los métodos estándar de carga.  Por ejemplo, la carga masiva bcp herramienta, los servicios de integración e INSERT... SELECT puede cargar todos los datos en un índice agrupado.  
  
 Los índices clúster de almacén de columnas aprovechan el almacén delta para evitar la fragmentación de segmentos de columna en el almacén de columnas.  
  
### <a name="loading-into-a-partitioned-table"></a>Carga en una tabla con particiones  
 Para los datos con particiones, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] primero asigna cada fila a una partición y después realiza operaciones del almacén de columnas con los datos de la partición. Cada partición tiene sus propios grupos de filas y un almacén delta por lo menos.  
  
### <a name="deltastore-loading-scenarios"></a>Escenarios de carga de almacén delta  
 Las filas se acumulan en el almacén delta hasta que su número alcanza el máximo permitido para formar un grupo de filas. Cuando el almacén delta contiene el número máximo de filas por grupo, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] marca como "CLOSED". Un proceso en segundo plano, denominado el "motor de tupla", busca el grupo de filas cerrado y se mueve al almacén de columnas, donde el grupo de filas se comprime en segmentos de columna y los segmentos de columna se almacenan en el almacén de columnas.  
  
 Para cada índice clúster del almacén de columnas puede haber varios almacenes delta.  
  
-   Si un almacén delta está bloqueado, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] intentará obtener un bloqueo en otro almacén delta. Si no hay almacenes delta disponibles, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] creará uno nuevo.  
  
-   En una tabla con particiones, puede haber uno o varios almacenes delta para cada partición.  
  
 Para los índices clúster de almacén de columnas solo, en los escenarios siguientes se describe cuándo las filas cargadas pasan directamente al almacén de columnas o cuándo van al almacén delta.  
  
 En este ejemplo, cada grupo de filas puede tener de 102.400 a 1.048.576 filas.  
  
|Filas que se cargarán de forma masiva|Filas agregadas al almacén de columnas|Filas agregadas al almacén delta|  
|-----------------------|-----------------------------------|----------------------------------|  
|102,000|0|102,000|  
|145,000|145,000<br /><br /> Tamaño del grupo de filas: 145,000|0|  
|1,048,577|1,048,576<br /><br /> Tamaño del grupo de filas: 1 048 576.|1|  
|2,252,152|2,252,152<br /><br /> Tamaños de los grupos de filas: 1 048 576, 1 048 576, 155 000.|0|  
  
 En el ejemplo siguiente se muestran los resultados de cargar 1.048.577 filas en una partición. Los resultados muestran un grupo de filas COMPRESSED en el almacén de columnas (como segmentos de columna comprimidos) y una fila en el almacén delta.  
  
```  
SELECT * FROM sys.column_store_row_groups  
```  
  
 ![Grupo de filas y almacenamiento delta para una carga por lotes](../../2014/database-engine/media/sql-server-pdw-columnstore-batchload.gif "Grupo de filas y almacenamiento delta para una carga por lotes")  
  

  
##  <a name="change"></a> Cambiar los datos de un índice agrupado de almacén de columnas  
 Los índices clúster de almacén de columnas admiten las operaciones del DML INSERT, UPDATE y DELETE.  
  
 Use [insertar &#40;Transact-SQL&#41; ](/sql/t-sql/statements/insert-transact-sql) para insertar una fila. Se agregará la fila al almacén delta.  
  
 Use [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql) para eliminar una fila.  
  
-   Si la fila se encuentra en el almacén de columnas, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] marca la fila como eliminada lógicamente, pero no recupera el almacenamiento físico de la fila hasta que se vuelve a generar el índice.  
  
-   Si la fila se encuentra en el almacén delta, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] elimina la fila lógica y físicamente.  
  
 Use [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql) para actualizar una fila.  
  
-   Si la fila se encuentra en el almacén de columnas, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] marca la fila como eliminada lógicamente y, a continuación, inserta la fila actualizada en el almacén delta.  
  
-   Si la fila se encuentra en el almacén delta, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] la actualiza en ese almacén.  
  
##  <a name="rebuild"></a> Volver a generar un índice agrupado de almacén de columnas  
 Use [CREATE CLUSTERED COLUMNSTORE INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql) o [ALTER INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-index-transact-sql) para realizar una reconstrucción completa de un índice agrupado existente. Además, puede usar ALTER INDEX... REBUILD para volver a crear una partición específica.  
  
### <a name="rebuild-process"></a>Proceso de regeneración  
 Para volver a generar un índice de almacén de columnas clúster, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Adquiere un bloqueo exclusivo en la tabla o la partición mientras se produce la regeneración.  Los datos están “sin conexión” y no disponibles durante la regeneración.  
  
-   Desfragmenta el almacén de columnas físicamente eliminando filas que se han eliminado lógicamente de la tabla; los bytes eliminados se reclaman en los medios físicos.  
  
-   Antes de volver a generar el índice, combina los datos del almacén de filas del almacén delta con los datos del almacén de columnas. Una vez finalizada la regeneración, todos los datos se almacenan en el almacén de columnas y el almacén delta se queda vacío.  
  
-   Vuelve a comprimir todos los datos del almacén de columnas. Hay dos copias del índice de almacén de columnas mientras se está produciendo la regeneración. Cuando se finaliza la recopilación, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] elimina el índice original del almacén de columnas.  
  
### <a name="recommendations-for-rebuilding-a-clustered-columnstore-index"></a>Recomendaciones para volver a generar un índice clúster de almacén de columnas  
 Volver a generar un índice clúster de almacén de columnas es útil para quitar la fragmentación y para mover todas las filas al almacén de columnas. Siga estas recomendaciones:  
  
-   Vuelva a generar una partición en lugar de la tabla completa.  
  
    1.  Volver a generar la tabla completa tarda mucho si el índice es grande y requiere el espacio en disco suficiente para almacenar una copia adicional del índice durante la regeneración. Por lo general, solo es necesario volver a generar la partición que se ha usado más recientemente.  
  
    2.  Para las tablas con particiones, no es necesario que vuelva a generar el índice de almacén de columnas completo, ya que es probable que se produzca la fragmentación solo en las particiones que se han modificado recientemente. Las tablas de hechos y las tablas de dimensiones de gran tamaño normalmente tienen particiones para poder realizar operaciones de copia de seguridad y de administración con los fragmentos de la tabla.  
  
-   Vuelva a generar una partición después de haber realizado operaciones DML intensivas.  
  
     La regeneración de una partición desfragmentará la partición y reducirá el almacenamiento de disco. La regeneración eliminará todas las filas del almacén de columnas que están marcadas para eliminación y trasladará todas las filas de almacén delta al almacén de columnas.  
  
-   Vuelva a generar una partición después de cargar los datos.  
  
     Esto garantiza que todos los datos se almacenan en el almacén de columnas. Si se producen varias cargas al mismo tiempo, cada partición puede acabar teniendo varios almacenes delta. La regeneración trasladará todas las filas del almacén delta al almacén de columnas.  
  
##  <a name="reorganize"></a> Reorganizar un índice agrupado de almacén de columnas  
 La reorganización de un índice clúster de almacén de columnas desplaza todos los grupos de columnas marcados como CLOSED al almacén de columnas. Para realizar una reorganización, utilice [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)con la opción REORGANIZE.  
  
 No es necesario llevar a cabo la reorganización para mover grupos de filas CLOSED al almacén de columnas. El proceso de tupla motriz encontrará finalmente todos los grupos de filas CLOSED y los moverá. Sin embargo, la tupla motriz es de un solo subproceso y los grupos de filas pueden no moverse lo suficientemente rápido para la carga de trabajo.  
  
### <a name="recommendations-for-reorganizing"></a>Recomendaciones para reorganizar  
 Cuándo se debe reorganizar un índice clúster de almacén de columnas:  
  
-   Reorganice un índice clúster de almacén de columnas después de una o varias cargas de datos para obtener mejoras en el rendimiento de las consultas lo más rápidamente posible. Inicialmente, el proceso de reorganización requerirá recursos de CPU adicionales para comprimir los datos, lo que podría reducir el rendimiento general del sistema. Sin embargo, tan pronto como los datos están comprimidos, el rendimiento de las consultas puede mejorar.  
  
  
