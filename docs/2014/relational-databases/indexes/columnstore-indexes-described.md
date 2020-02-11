---
title: Índices de almacén de columnas descritos | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexes creation, columnstore
- indexes [SQL Server], columnstore
- columnstore index
- columnstore index, described
- xVelocity, columnstore indexes
ms.assetid: f98af4a5-4523-43b1-be8d-1b03c3217839
author: mikeraymsft
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 87d19bc837219b5573dd237310b11dab9f146406
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68811040"
---
# <a name="columnstore-indexes-described"></a>Columnstore Indexes Described
  El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] *Índice de almacén de columnas en memoria* almacena y administra los datos mediante el almacenamiento de datos basado en columnas y el procesamiento de consultas basado en columnas. Los índices de almacén de columnas funcionan correctamente para las cargas de trabajo de almacenamiento de datos que ejecutan principalmente cargas masivas y consultas de solo lectura. Use el índice de almacén de columnas para aumentar **hasta en diez veces el rendimiento de las consultas** en relación con el almacenamiento tradicional orientado a filas, y hasta **en siete veces la compresión de datos** en relación con el tamaño de los datos sin comprimir.  
  
> [!NOTE]  
>  Consideramos que el índice clúster de almacén de columnas es el estándar para el almacenamiento de grandes tablas de hechos de almacenamiento de datos, y esperamos que se use en la mayoría de los escenarios de almacenamiento de datos. Puesto que el índice de almacén de columnas clúster es actualizable, la carga de trabajo puede realizar un gran número operaciones de inserción, actualización y eliminación.  
  
## <a name="contents"></a>Contenido  
  
-   [Conceptos básicos](#basics)  
  
-   [Cargar datos](#dataload)  
  
-   [Sugerencias de rendimiento](#performance)  
  
-   [Temas y tareas relacionados](#related)  
  
##  <a name="basics"></a> Conceptos básicos  
 Un *Índice de almacén de columnas* es una tecnología para almacenar, recuperar y administrar datos mediante el uso de un formato de datos en columnas denominado almacén de columnas. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite índices clúster y no clúster de almacén de columnas. Ambos usan la misma tecnología de almacén de columnas en memoria, pero tienen algunas diferencias en cuanto a su propósito y las funciones que admiten.  
  
###  <a name="benefits"></a> Ventajas  
 Los índices de almacén de columnas funcionan correctamente con la mayoría de las consultas de solo lectura que realizan análisis en conjuntos de datos grandes. A menudo, se trata de consultas de cargas de trabajo de almacenamiento de datos. Los índices de almacén de columnas ofrecen alto rendimiento para las consultas que usan recorridos de tabla completos y no son adecuados para las consultas que buscan un valor concreto en los datos.  
  
 Ventajas de los índices de almacén de columnas:  
  
-   Las columnas a menudo tienen datos similares, lo que da como resultado factores de compresión altos.  
  
-   Los factores de compresión altos mejoran el rendimiento de las consultas mediante la utilización de una superficie en memoria menor. A su vez, el rendimiento de las consultas puede mejorar porque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede realizar más consultas y operaciones de datos en memoria.  
  
-   Se ha agregado a SQL Server un nuevo mecanismo de ejecución de consultas denominado ejecución en modo por lotes que reduce considerablemente el uso de CPU. La ejecución en modo por lotes está estrechamente integrada con el formato de almacenamiento de almacén de columnas y optimizada alrededor del mismo. La ejecución en modo por lotes se conoce en ocasiones como ejecución basada en vectores o vectorizada.  
  
-   Con frecuencia, las consultas seleccionan únicamente unas pocas columnas de una tabla, lo que reduce la E/S total desde los medios físicos.  
  
### <a name="columnstore-versions"></a>Versiones de almacén de columnas  
 SQL Server 2012, Almacenamiento de datos paralelos de SQL Server 2012 y SQL Server 2014 emplean índices de almacén de columnas para acelerar las consultas comunes de almacenamiento de datos. SQL Server 2012 presentó dos nuevas características: un índice no clúster de almacén de columnas y una capacidad de ejecución basada en vectores que procesa los datos en unidades denominadas "lotes". SQL Server 2014 cuenta con las características de SQL Server 2012, además de índices clúster de almacén de columnas actualizables.  
  
### <a name="key-characteristics"></a>Características clave  
  
||  
|-|  
|**Se aplica a** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] : [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]hasta.|  
  
 En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], un índice clúster de almacén de columnas:  
  
-   Está disponible en las ediciones Enterprise, Developer y Evaluation.  
  
-   Es actualizable.  
  
-   Es el método de almacenamiento principal de toda la tabla.  
  
-   No tiene ninguna columna de clave. Todas las columnas son columnas incluidas.  
  
-   Es el único índice de la tabla. No se puede combinar con ningún otro índice.  
  
-   Se puede configurar para usar almacén de columnas o compresión de archivo de almacén de columnas.  
  
-   No almacena físicamente las columnas de forma ordenada. En su lugar, almacena los datos para mejorar la compresión y el rendimiento.  
  
||  
|-|  
|**Se aplica a** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] : [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]hasta.|  
  
 En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], un índice no clúster de almacén de columnas:  
  
-   Puede indizar un subconjunto de columnas del índice clúster o el montón. Por ejemplo, puede indizar las columnas usadas con frecuencia.  
  
-   Necesita almacenamiento adicional para almacenar una copia de las columnas en el índice.  
  
-   Se actualiza regenerando el índice o cambiando las particiones dentro y fuera. No se actualiza mediante el uso de las operaciones DML, como INSERT, Update y DELETE.  
  
-   Se puede combinar con otros índices de la tabla.  
  
-   Se puede configurar para usar almacén de columnas o compresión de archivo de almacén de columnas.  
  
-   No almacena físicamente las columnas de forma ordenada. En su lugar, almacena los datos para mejorar la compresión y el rendimiento. No es necesario ordenar los datos antes de crear el índice de almacén de columnas, pero si se hace puede mejorar la compresión de almacén de columnas.  
  
###  <a name="Concepts"></a>Conceptos y términos clave  
 Los términos y conceptos clave siguientes están asociados a los índices de almacén de columnas.  
  
 índice de almacén de columnas  
 Un *Índice de almacén de columnas* es una tecnología para almacenar, recuperar y administrar datos mediante el uso de un formato de datos en columnas denominado almacén de columnas. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite índices clúster y no clúster de almacén de columnas. Ambos usan la misma tecnología de almacén de columnas en memoria, pero tienen algunas diferencias en cuanto a su propósito y las funciones que admiten.  
  
 almacén de columnas  
 Un *almacén de columnas* son datos organizados lógicamente como una tabla con filas y columnas, y almacenados físicamente en un formato de columnas.  
  
 almacén de filas  
 Un *almacén de filas* son datos organizados lógicamente como una tabla con filas y columnas, y almacenados físicamente después en un formato de filas. Esta ha sido la forma tradicional de almacenar los datos de una tabla relacional.  
  
 grupos de filas y segmentos de columna  
 Para conseguir unas tasas elevadas de rendimiento y compresión, el índice de almacén de columnas segmenta la tabla en grupos de filas y comprime cada grupo de filas a modo de columna. El número de filas del grupo de filas debe ser suficientemente grande como para mejorar las tasas de compresión y suficientemente pequeño como para beneficiarse de las operaciones en memoria.  
  
 grupo de filas  
 Un *filas* es un grupo de filas que se comprimen al mismo tiempo en el formato de almacén de columnas.  
  
 segmento de columna  
 Un *segmento de columna* es una columna de datos de dentro de filas.  
  
-   Un grupo de filas suele contener el número máximo de filas por grupo, que es 1.048.576 filas.  
  
-   Cada grupo de filas contiene un segmento de cada columna de la tabla.  
  
-   Cada sector de columna se comprime junto y se almacena en un medio físico.  
  
 ![Segmento de columna](../../database-engine/media/sql-server-pdw-columnstore-columnsegment.gif "segmento de columna")  
  
 índice no clúster de almacén de columnas  
 Un *nonclustered columnstore index* es un índice de solo lectura creado sobre un índice clúster o una tabla del montón existente. Contiene una copia de un subconjunto de columnas, hasta incluir todas las columnas de la tabla. La tabla es de solo lectura mientras contiene un índice no clúster de almacén de columnas.  
  
 Un índice no clúster de almacén de columnas proporciona una manera de tener un índice de almacén de columnas para ejecutar consultas de análisis al tiempo que se realizan operaciones de solo lectura en la tabla original.  
  
 ![Índice de almacén de columnas no agrupado](../../database-engine/media/sql-server-pdw-columnstore-physicalstorage-nonclustered.gif "índice no clúster de almacén de columnas")  
  
 Índice clúster de almacén de columnas  
 Un *clustered columnstore index* es el almacenamiento físico para toda la tabla y es el único índice de la tabla. El índice clúster se puede actualizar. Puede realizar operaciones de inserción, eliminación y actualización del índice y puede cargar datos de forma masiva en el índice.  
  
 ![Índice de almacén de columnas agrupado](../../database-engine/media/sql-server-pdw-columnstore-physicalstorage.gif "Índice de almacén de columnas agrupado")  
  
 Para reducir la fragmentación de los segmentos de columna y mejorar el rendimiento, el índice de almacén de columnas puede almacenar temporalmente algunos datos en una tabla de almacén de filas, denominada almacén delta, así como un árbol B de los identificadores de las filas eliminadas. Las operaciones del almacén delta se administran en segundo plano. Para devolver los resultados correctos de la consulta, el índice clúster de almacén de columnas combina los resultados de la consulta tanto del almacén de columnas como del almacén delta.  
  
 almacén delta  
 Un *almacén delta* , que solo se usa con índices clúster de almacén de columnas, es una tabla de almacén de filas donde se almacenan las filas hasta que el número de estas es lo suficientemente grande como para trasladarlas al almacén de columnas. Un almacén delta se usa con índices clúster de almacén de columnas para mejorar el rendimiento de carga y de otras operaciones DML.  
  
 Durante una gran carga masiva, la mayoría de las filas van directamente al almacén de columnas sin pasar por el almacén delta. Al final de la carga masiva, podría quedar un número de filas menor que el tamaño mínimo de un grupo de filas, que es 102.400 filas. Cuando esto sucede, las últimas filas van al almacén delta en lugar de al almacén de columnas. En el caso de cargas masivas pequeñas con menos de 102.400 filas, todas las filas van directamente al almacén delta.  
  
 Cuando el almacén delta alcanza el número máximo de filas, se cierra. Un proceso de tupla motriz comprueba si hay grupos de filas cerrados. Cuando encuentra el grupo de filas cerrado, lo comprime y lo almacena en el almacén de columnas.  
  
##  <a name="dataload"></a>Cargar datos  
  
###  <a name="dataload_nci"></a>Cargar datos en un índice de almacén de columnas no agrupado  
 Para cargar datos en un índice de almacén de columnas no agrupado, cargue primero los datos en una tabla de almacén tradicional almacenada como un montón o un índice clúster y, a continuación, cree el índice de almacén de columnas no agrupado con [Create de índice de almacén de columnas &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql).  
  
 ![Cargar datos en un índice de almacén de columnas](../../database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "Cargar datos en un índice de almacén de columnas")  
  
 Una tabla con un índice no clúster de almacén de columnas es de solo lectura hasta que se quita o se deshabilita el índice. Para actualizar la tabla y el índice de almacén de columnas no agrupado, puede cambiar las particiones dentro y fuera. También puede deshabilitar el índice, actualizar la tabla y, a continuación, volver a generar el índice.  
  
 Para obtener más información, vea [Using Nonclustered Columnstore Indexes](indexes.md)  
  
###  <a name="dataload_cci"></a>Cargar datos en un índice de almacén de columnas agrupado  
 ![Cargar en un índice de almacén de columnas en clúster](../../database-engine/media/sql-server-pdw-columnstore-loadprocess.gif "Cargar en un índice de almacén de columnas en clúster")  
  
 Como se muestra en el diagrama, para cargar datos en un índice clúster de almacén de columnas, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
1.  Inserta grupos de filas con el tamaño máximo directamente en el almacén de columnas. A medida que se cargan los datos, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] asigna las filas de datos a un grupo de filas abierto por orden de llegada.  
  
2.  Cuando cada grupo de filas alcanza el tamaño máximo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
    1.  Lo marca como CLOSED.  
  
    2.  Omite el almacén delta.  
  
    3.  Comprime cada segmento de columna del grupo de filas mediante la compresión Columnstore.  
  
    4.  Almacena físicamente cada segmento de columna comprimido en el almacén de columnas.  
  
3.  Inserta las filas restantes en el almacén de columnas o en el almacén delta del modo siguiente:  
  
    1.  Si el número de filas coincide con el número mínimo de filas necesario para formar un grupo de filas, las filas se agregan al almacén de columnas.  
  
    2.  Si el número de filas es menor que el número mínimo de filas necesario para formar un grupo de filas, las filas se agregan al almacén delta.  
  
 Para obtener más información acerca de las tareas y los procesos de almacén delta, vea [Using Clustered Columnstore Indexes](../../database-engine/using-clustered-columnstore-indexes.md).  
  
##  <a name="performance"></a>Sugerencias de rendimiento  
  
### <a name="plan-for-enough-memory-to-create-columnstore-indexes-in-parallel"></a>Planear para que haya suficiente memoria para crear índices de almacén de columnas en paralelo  
 La creación un índice de almacén de columnas es de forma predeterminada una operación paralela a menos que se restrinja la memoria. Crear el índice en paralelo requiere más memoria que crear el índice en serie. Cuando hay suficiente memoria, la creación de un índice de almacén de columnas tarda aproximadamente 1,5 más que generar un árbol B en las mismas columnas.  
  
 La memoria necesaria para crear un índice de almacén de columnas depende del número de columnas, el número de columnas de cadena, el grado de paralelismo (DOP) y las características de los datos. Por ejemplo, si la tabla tiene menos de un millón de filas, SQL Server solo usará un subproceso para crear el índice de almacén de columnas.  
  
 Si la tabla tiene más de un millón de filas pero SQL Server no puede obtener una concesión de memoria suficiente para crear el índice mediante MAXDOP, SQL Server reducirá automáticamente el valor de MAXDOP según sea necesario para ajustarse a la concesión de memoria disponible.  En algunos casos, se debe reducir a uno el DOP para generar el índice cuando la memoria está restringida.  
  
##  <a name="related"></a>Temas y tareas relacionados  
  
### <a name="nonclustered-columnstore-indexes"></a>Índices no clúster de almacén de columnas  
 Para las tareas comunes, vea [Using Nonclustered Columnstore Indexes](../../database-engine/using-nonclustered-columnstore-indexes.md).  
  
-   [CREAR índice de almacén de columnas &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql) con Rebuild.  
  
-   [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
### <a name="clustered-columnstore-indexes"></a>Índices clúster de almacén de columnas  
 Para las tareas comunes, vea [Using Clustered Columnstore Indexes](../../database-engine/using-clustered-columnstore-indexes.md).  
  
-   [CREAR índice clúster de almacén de columnas &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql) con Rebuild o reorganize.  
  
-   [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
-   [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)  
  
-   [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)  
  
-   [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql)  
  
### <a name="metadata"></a>Metadatos  
 Todas las columnas de un índice de almacén de columnas se almacenan en los metadatos como columnas incluidas. El índice de almacén de columnas no tiene columnas de clave.  
  
-   [sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)  
  
-   [sys.index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-index-columns-transact-sql)  
  
-   [Sys. partitions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-partitions-transact-sql)  
  
-   [Sys. column_store_segments &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-segments-transact-sql)  
  
-   [Sys. column_store_dictionaries &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql)  
  
-   [Sys. column_store_row_groups &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql)  
  
  
