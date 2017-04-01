---
title: "Carga de datos de &#237;ndices de almac&#233;n de columnas | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b29850b5-5530-498d-8298-c4d4a741cdaf
caps.latest.revision: 31
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 28
---
# Carga de datos de &#237;ndices de almac&#233;n de columnas
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Cargue datos en un índice de almacén de columnas mediante los métodos de inserción gradual y carga masiva SQL estándar. Estos métodos incluyen la herramienta bcp, Integration Services y la instrucción Transact-SQL MERGE o INSERT.  
  
 ¿Es la primera vez que utiliza índices de almacén de columnas? Revise los términos y los conceptos en la [Guía de índices de almacén de columnas](../Topic/Columnstore%20Indexes%20Guide.md).  
  
 ¿Necesita una explicación más detallada? Consulte esta [entrada de blog](http://blogs.msdn.com/b/sqlcat/archive/2015/03/11/data-loading-performance-considerations-on-tables-with-clustered-columnstore-index.aspx).  
  
##  <a name="dataload_cci"></a> Carga de datos en un índice de almacén de columnas agrupado  
 Para cargar filas de forma masiva en un índice de almacén de columnas agrupado, puede usar la herramienta de línea de comandos bcp o Integration Services, o bien seleccionar las filas de una tabla de almacenamiento provisional.  
  
 ![Cargar en un índice de almacén de columnas en clúster](../../relational-databases/indexes/media/sql-server-pdw-columnstore-loadprocess.gif "Cargar en un índice de almacén de columnas en clúster")  
  
 Tal y como se recomienda en el diagrama, una carga masiva:  
  
1.  No ordena los datos previamente. Los datos se insertan en grupos de filas en el orden en que se reciben.  
  
2.  Si el tamaño de lote es mayor o igual que 102400, las filas estarán directamente en el grupo de filas comprimido. Se recomienda elegir un tamaño de lote mayor o igual que 102400 para que la importación en bloque se realice de forma eficaz, ya que puede evitar que se muevan las filas de datos a un grupo de filas delta antes de que las filas se terminan moviendo a grupos de filas comprimidos mediante un subproceso en segundo plano, el motor de tupla (TM).  
  
3.  Si el tamaño de lote o el de las filas restantes es menor que 102400, las filas se cargarán en grupos de filas delta.  
  
 Las siguientes optimizaciones están disponibles con la carga masiva en índices de almacén de columnas agrupados.  
  
-   Carga en paralelo: puede realizar varias importaciones simultáneas en bloque (bcp o inserción masiva) cargando un archivo de datos independiente. A diferencia del almacén de filas, no hay que especificar TABLOCK, ya que cada subproceso de importación en bloque cargará los datos solamente en grupos de filas independientes (grupos de filas delta o comprimidos) aplicando un bloqueo exclusivo.   Al usar TABLOCK, se forzará un bloqueo exclusivo en la tabla y no podrá importar los datos en paralelo.  
  
-   Optimización del registro: la carga masiva se registrará mínimamente cuando se carguen los datos en el grupo de filas comprimido. No existe ningún registro mínimo cuando se cargan datos en el grupo de filas delta con un tamaño de lote menor que 102400.  
  
-   Optimización de bloqueo: cuando se cargan datos en un grupo de filas comprimido, se obtiene el bloqueo X en el grupo de filas. Sin embargo, cuando la carga masiva se realiza en el grupo de filas delta, se obtiene un bloqueo X en el grupo de filas, pero SQL Server continúa bloqueando los bloqueos de página y extensión, ya que el bloqueo de grupos de filas X no forma parte de la jerarquía de bloqueo.  
  
 Si tiene uno o varios índices no agrupados, no habrá ninguna optimización de registro o bloqueo para el propio índice; sin embargo, las optimizaciones en el índice de almacén de columnas agrupado siguen estando disponibles, tal y como se describió anteriormente.  
  
## Cómo funciona el almacén delta  
 Los índices de almacén de columnas agrupados recopilan hasta 1 048 576 filas en el almacén delta antes de comprimirlas en el grupo de filas comprimido. De este modo, se mejora la compresión del índice de almacén de columnas. Cuando un grupo de filas de almacén delta contiene 1 048 576 filas, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo marca como cerrado. Un proceso en segundo plano denominado *tuple-mover* identifica cada grupo de filas marcado como cerrado y lo comprime en el almacén de columnas.  
  
 Para cada índice clúster del almacén de columnas puede haber varios almacenes delta.  
  
-   Si un almacén delta está bloqueado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intentará obtener un bloqueo en otro almacén delta. Si no hay almacenes delta disponibles, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creará uno nuevo.  
  
-   En una tabla con particiones, puede haber uno o varios almacenes delta en cada partición.  
  
 En estos escenarios siguientes se describe cuándo las filas cargadas pasan directamente al almacén de columnas o cuándo van al almacén delta.  
  
 En este ejemplo, cada grupo de filas puede tener de 102.400 a 1.048.576 filas. En la práctica, el tamaño máximo de un grupo de filas puede ser inferior a 1 048 576 filas cuando hay presión de memoria.  
  
|Filas que se cargarán de forma masiva|Filas agregadas al grupo de filas comprimido|Filas agregadas al grupo de filas delta|  
|-----------------------|-------------------------------------------|--------------------------------------|  
|102,000|0|102,000|  
|145,000|145,000<br /><br /> Tamaño del grupo de filas: 145.000|0|  
|1,048,577|1,048,576<br /><br /> Tamaño del grupo de filas: 1.048.576|1|  
|2,252,152|2,252,152<br /><br /> Tamaños de los grupos de filas: 1.048.576, 1.048.576, 155.000|0|  
  
 En el ejemplo siguiente se muestran los resultados de cargar 1 048 577 filas en una tabla. Los resultados muestran un grupo de filas COMPRESSED en el almacén de columnas (como segmentos de columna comprimidos) y una fila en el almacén delta.  
  
```  
SELECT object_id, index_id, partition_number, row_group_id, delta_store_hobt_id, state state_desc, total_rows, deleted_rows, size_in_bytes   
FROM sys.dm_db_column_store_row_group_physical_stats  
```  
  
 ![Rowgroup and deltastore for a batch load](../../relational-databases/indexes/media/sql-server-pdw-columnstore-batchload.gif "Rowgroup and deltastore for a batch load")  
  
## Carga desde una tabla de almacenamiento provisional.  
 Un patrón común de carga de datos consiste en cargar los datos en una tabla de almacenamiento provisional, realizar alguna transformación y, después, cargarlos en la tabla de destino con el siguiente comando:  
  
```  
INSERT INTO <columnstore index>  SELECT <list of columns> FROM <Staging Table>  
  
```  
  
 Este comando carga los datos en el índice de almacén de columnas de una forma similar a bcp o la tarea de inserción masiva, solo que en un único lote. Si el número de filas de la tabla de almacenamiento provisional es menor que 102400, las filas se cargarán en un grupo de filas delta; en caso contrario, se cargarán directamente en un grupo de filas comprimido.  Antes existía una limitación importante: esta operación INSERT era de un solo subproceso. Para cargar los datos en paralelo, podía crear varias tablas de almacenamiento provisional o ejecutar INSERT o SELECT con intervalos no superpuestos de filas desde la tabla de almacenamiento provisional.  Esta limitación desaparece en SQL Server 2016. El siguiente comando carga los datos en paralelo de la tabla de almacenamiento provisional, pero tendrá que especificar TABLOCK.  
  
```  
INSERT INTO <columnstore index>  WITH (TABLOCK)  SELECT <list of columns> FROM <Staging Table>  
```  
  
 Las siguientes optimizaciones están disponibles cuando se cargan datos en índices de almacén de columnas agrupados desde tablas de almacenamiento provisional.  
  
-   Optimización del registro: se registra mínimamente cuando los datos se cargan en el grupo de filas comprimido. No existe ningún registro mínimo cuando se cargan datos en el grupo de filas delta.  
  
-   Optimización de bloqueo: cuando se cargan datos en un grupo de filas comprimido, se obtiene el bloqueo X en el grupo de filas. Sin embargo, con el grupo de filas delta, se obtiene un bloqueo X en el grupo de filas, pero SQL Server continúa bloqueando los bloqueos de página y extensión, ya que el bloqueo de grupos de filas X no forma parte de la jerarquía de bloqueo.  
  
 Si tiene uno o varios índices no agrupados, no habrá ninguna optimización de registro o bloqueo para el propio índice; sin embargo, las optimizaciones en el índice de almacén de columnas agrupado siguen estando disponibles, tal y como se describió anteriormente.  
  
## Carga con inserción gradual  
 Con*inserción gradual* nos referimos a la forma en que se cargan filas en el almacén de columnas mediante INSERT INTO. Cada fila se agrega a un grupo de filas delta. Las filas que se insertan pasan directamente a un grupo de filas de almacén delta, donde se acumulan hasta que se cierra el grupo de filas tras alcanzar las 1 048 576 filas, o bien hasta que se vuelva a generar el índice de almacén de columnas.  
  
```  
INSERT INTO <table-name> VALUES (<set of values>)  
```  
  
 Tenga en cuenta que los subprocesos simultáneos que usan INSERT INTO para insertar valores en un índice de almacén de columnas agrupado pueden insertar filas en el mismo grupo de filas de almacén delta.  
  
 Una vez que el grupo de filas contiene 1 048 576 filas, el grupo de filas delta se marca como cerrado, pero sigue estando disponible para las consultas y las operaciones de actualización o eliminación. No obstante, las filas recién insertadas se pasan a un grupo de filas de almacén delta existente o recién creado. Hay un subproceso en segundo plano, el *motor de tupla (TM)*, que comprime los grupos de filas delta cerrados cada 5 minutos aproximadamente. Puede invocar expresamente el siguiente comando para comprimir el grupo de filas delta cerrado.  
  
```  
ALTER INDEX <index-name> on <table-name> REORGANIZE  
```  
  
 Si desea forzar el cierre o la compresión de un grupo de filas delta, ejecute el siguiente comando. Se recomienda ejecutar este comando si ha terminado de cargar las filas y no espera insertar nuevas filas. Al cerrar y comprimir expresamente el grupo de filas delta, puede ahorrar más espacio de almacenamiento y mejorar el rendimiento de las consultas de análisis. Sugerimos invocar este comando si no espera insertar nuevas filas.  
  
```  
ALTER INDEX <index-name> on <table-name> REORGANIZE with (COMPRESS_ALL_ROW_GROUPS = ON)  
```  
  
## Carga en una tabla con particiones  
 Para los datos con particiones, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] primero asigna cada fila a una partición y después realiza operaciones del almacén de columnas con los datos de la partición. Cada partición tiene sus propios grupos de filas y un almacén delta por lo menos.  
  
## Carga en un índice de almacén de columnas no agrupado  
 En una tabla de almacén de filas con datos de índices de almacén de columnas no agrupados, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siempre inserta los datos en la tabla base. Nunca se insertan directamente en el índice de almacén de columnas.  
  
## Vea también  
 [Guía de índices de almacén de columnas](../Topic/Columnstore%20Indexes%20Guide.md)   
 [Resumen de las características de los índices de almacén de columnas para cada versión](../Topic/Columnstore%20Indexes%20Versioned%20Feature%20Summary.md)   
 [Rendimiento de las consultas de índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Introducción al almacén de columnas para análisis operativos en tiempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [Índices de almacén de columnas para el almacenamiento de datos](../Topic/Columnstore%20Indexes%20for%20Data%20Warehousing.md)   
 [Desfragmentación de índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  