---
title: Tablas e índices con particiones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- partitioned tables [SQL Server], about partitioned tables
- partitioned indexes [SQL Server], architecture
- partitioned tables [SQL Server], architecture
- partitioned indexes [SQL Server], about partitioned indexes
ms.assetid: cc5bf181-18a0-44d5-8bd7-8060d227c927
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5f96f82919b9f4a130ce8a533e6ffcf31e765f5f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65092041"
---
# <a name="partitioned-tables-and-indexes"></a>Partitioned Tables and Indexes
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es compatible con la creación de particiones de tabla e índice. Los datos de tablas e índices con particiones se dividen en unidades que pueden propagarse por más de un grupo de archivos de la base de datos. Los datos se dividen en sentido horizontal, de forma que los grupos de filas se asignan a particiones individuales. Las particiones de un índice o una tabla deben encontrarse en la misma base de datos. La tabla o el índice se tratarán como una sola entidad lógica cuando se realicen consultas o actualizaciones en los datos. Las tablas e índices con particiones no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite hasta 15.000 particiones de forma predeterminada. En las versiones anteriores a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], el número de particiones está limitado a 1.000 de forma predeterminada. En sistemas basados en x86, se puede crear una tabla o un índice con más de 1000 particiones pero no se admite.  
  
## <a name="benefits-of-partitioning"></a>Ventajas de la creación de particiones  
 La creación de particiones de tablas o índices grandes puede tener las siguientes ventajas de administración y rendimiento.  
  
-   Se puede transferir u obtener acceso a subconjuntos de datos de forma rápida y eficaz, a la vez que mantiene la integridad de una recopilación de datos. Por ejemplo, una operación como la carga de datos desde un sistema OLTP a un sistema OLAP tarda solo unos segundos, en lugar de los minutos y las horas que se requieren cuando no se ha realizado una partición de los datos.  
  
-   Puede realizar operaciones de mantenimiento en una o más particiones más rápidamente. Las operaciones son más eficaces porque solo afectan a estos subconjuntos de datos, y no a toda la tabla. Por ejemplo, se puede elegir comprimir los datos en una o varias particiones o recompilar una o varias particiones de un índice.  
  
-   Se puede mejorar el rendimiento de las consultas, en función de los tipos de consultas que se suelen ejecutar y de la configuración del hardware. Por ejemplo, el optimizador de consultas puede procesar consultas de combinación de igualdad entre dos o más tablas con particiones más rápidamente cuando las columnas de partición de las tablas son iguales, porque las particiones se pueden combinar.  
  
     Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza una ordenación de los datos para operaciones de E/S, los ordena primero por partición. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene acceso a una unidad cada vez y esto podría reducir el rendimiento. Para mejorar el rendimiento de la ordenación de los datos, cree franjas de los archivos de datos de las particiones en más de un disco configurando una RAID. De este modo, aunque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siga ordenando los datos por partición, puede tener acceso a todas las unidades de cada partición al mismo tiempo.  
  
     Además, la partición permite mejorar el rendimiento habilitando la extensión de bloqueo en el nivel de partición y no en toda la tabla. Esto puede reducir la contención en la tabla por bloqueo.  
  
## <a name="components-and-concepts"></a>Componentes y conceptos  
 Los siguientes términos son aplicables para las particiones de tablas e índices.  
  
 Función de partición  
 Una función de partición define la forma de asignar las filas de una tabla o un índice a un conjunto de particiones a partir de los valores de una determinada columna, denominada columna de partición. Es decir, la función de partición define el número de particiones que la tabla tendrá y cómo se definen los límites de las particiones. Por ejemplo, dada una tabla con datos de pedidos de ventas, puede crear doce particiones (mensuales) de la tabla tomando como base una columna `datetime`, por ejemplo una fecha de ventas.  
  
 Esquema de partición  
 Objeto de base de datos que asigna las particiones de una función de partición a un conjunto de grupos de archivos. La principal razón para colocar las particiones en distintos grupos de archivos es garantizar que se puedan realizar operaciones de copia de seguridad en particiones de forma independiente. Esto se debe a que se pueden realizar copias de seguridad en grupos de archivos individuales.  
  
 Columna de partición  
 La columna de una tabla o índice que una función de partición usa para crear particiones en la tabla o índice. Las columnas calculadas que participan en una función de partición deben marcarse explícitamente como PERSISTED. Todos los tipos de datos válidos para el uso en columnas de índice pueden utilizarse como una columna de partición con la excepción de `timestamp`. Los tipos de datos `ntext`, `text`, `image`, `xml`, `varchar(max)`, `nvarchar(max)` o `varbinary(max)` no se pueden especificar. Tampoco se pueden especificar columnas de tipo de datos de alias y de tipo definido por el usuario de Common Language Runtime (CLR) de Microsoft .NET Framework.  
  
 Índices alineados  
 Un índice que se compila con el mismo esquema de partición que su tabla correspondiente. Cuando una tabla y sus índices están alineados, SQL Server puede dividir las particiones de forma rápida y eficaz al mismo tiempo que mantiene la estructura de la partición tanto en la tabla como en sus índices. Un índice no tiene por qué participar en la misma función de partición con nombre para alinearse con su tabla base. Sin embargo, la función de partición del índice y la tabla base debe ser básicamente la misma puesto que 1) los argumentos de las funciones de la partición tienen el mismo tipo de datos, 2) definen el mismo número de particiones y 3) definen los mismos valores de límite para las particiones.  
  
 Índice no alineado  
 Un índice con particiones independientemente de su tabla correspondiente. Es decir, el índice tiene un esquema de partición diferente o está colocado en un grupo de archivos independiente de la tabla base. El diseño de un índice con particiones no alineado puede ser útil en los siguientes casos:  
  
-   En la tabla base no se han creado particiones.  
  
-   La clave de índice es única y no contiene la columna de partición de la tabla.  
  
-   Desea que la tabla base participe en combinaciones por colocación con más tablas usando columnas de combinación diferentes.  
  
 Eliminación de particiones  
 El proceso por el que el optimizador de consultas tiene acceso únicamente a las particiones pertinentes para cumplir los criterios de filtro de la consulta.  
  
## <a name="performance-guidelines"></a>Instrucciones de rendimiento  
 El nuevo, mayor límite de 15.000 particiones afecta a la memoria, operaciones con particiones de índice, comandos DBCC, y consultas. Esta sección describe las implicaciones para el rendimiento de aumentar el número de particiones en 1.000 y proporciona soluciones según sea necesario. Con el límite en el número máximo de particiones ampliado a 15.000, puede almacenar los datos durante más tiempo. Sin embargo, debe conservar datos solo mientras sea necesario y mantener un equilibrio entre el rendimiento y el número de particiones.  
  
### <a name="memory-usage-and-guidelines"></a>Instrucciones y uso de la memoria  
 Se recomienda usar al menos 16 GB de RAM si un gran número de particiones están en uso. Si el sistema no tiene suficiente memoria, (DML) las instrucciones de lenguaje de manipulación de datos, (DDL) instrucciones de lenguaje de definición de datos y otras operaciones pueden generar errores debido a la memoria insuficiente. Los sistemas con 16 GB de RAM que funcionan con muchos procesos intensivos de memoria pueden quedarse sin memoria en operaciones que ejecutan en un gran número de particiones. Por consiguiente, cuanta más memoria se tenga por encima de 16 GB menor es la posibilidad de enfrentarse a problemas de rendimiento y de memoria.  
  
 Las limitaciones de memoria pueden afectar al rendimiento o capacidad de SQL Server para compilar un índice con particiones. Esto sucede especialmente cuando el índice no está alineado con su tabla base o no está alineado con su índice clúster si ya se ha aplicado un índice clúster a la tabla.  
  
### <a name="partitioned-index-operations"></a>Operaciones de índices con particiones  
 Las limitaciones de memoria pueden afectar al rendimiento o capacidad de SQL Server para compilar un índice con particiones. Esto es especialmente así con índices no alineados. La creación y regeneración de índices no alineados en una tabla con más de 1.000 particiones es posible, pero no se admite. Si se hace, se puede degradar el rendimiento o consumir excesiva memoria durante estas operaciones.  
  
 Crear y recompilar índices alineados podría tardar mucho más tiempo en ejecutarse cuando el número de particiones aumenta. Se recomienda que no ejecute varios comandos de crear y recompilar índices al mismo tiempo, ya que quizás se enfrente a problemas de rendimiento y memoria.  
  
 Cuando SQL Server realiza la ordenación para compilar índices con particiones, primero compila una tabla de orden para cada partición. A continuación, compila las tablas de orden en el grupo de archivos respectivo de cada partición o en `tempdb` si se ha especificado la opción de índice SORT_IN_TEMPDB. Cada tabla de orden requiere una cantidad mínima de memoria para su compilación. Cuando crea un índice con particiones que está alineado con su tabla base, las tablas de orden se crean de una en una con menos memoria. Sin embargo, cuando crea un índice con particiones no alineado, las tablas de orden se crean al mismo tiempo. En consecuencia, debe haber disponible memoria suficiente para permitir la realización de estas ordenaciones simultáneas. Cuanto mayor es el número de particiones, mayor es la cantidad de memoria necesaria. El tamaño mínimo para cada tabla de orden y para cada partición es de 40 páginas y 8 kilobytes por página. Por ejemplo, un índice con particiones no alineado con 100 particiones necesita memoria suficiente para ordenar en serie 4.000 (40 * 100) páginas al mismo tiempo. Si esta memoria está disponible, la operación de creación será satisfactoria, aunque ello afectará negativamente al rendimiento. Si esta memoria no está disponible, se producirá un error durante la operación de creación. De forma alternativa, un índice con particiones alineado con 100 particiones solo necesita memoria suficiente para ordenar 40 páginas, ya que las ordenaciones no se realizan al mismo tiempo.  
  
 Tanto para los índices alineados como para los no alineados, el requisito de memoria puede ser mayor si SQL Server está aplicando grados de paralelismo a la operación de compilación en un equipo con varios procesadores. Esto es así porque cuanto mayores son los grados de paralelismo, mayor es también el requisito de memoria. Por ejemplo, si SQL Server establece los grados de paralelismo en 4, un índice no alineado con 100 particiones necesitará memoria suficiente para que cuatro procesadores puedan ordenar 4.000 páginas al mismo tiempo o 16.000 páginas. Si el índice con particiones está alineado, el requisito de memoria se reduce a cuatro procesadores que ordenan 40 páginas o 160 (4 * 40) páginas. Puede usar la opción de índice MAXDOP para reducir manualmente los grados de paralelismo.  
  
### <a name="dbcc-commands"></a>Comandos DBCC  
 Con un número de particiones mayor, los comandos DBCC pueden tardar más tiempo en ejecutarse cuando el número de particiones aumenta.  
  
### <a name="queries"></a>Consultas  
 Las consultas en que se usa la eliminación de particiones podrían tener un rendimiento comparable o mejorado con un número de particiones mayor. Las consultas que no usan eliminación de particiones podrían tardar más tiempo en ejecutarse cuando el número de particiones aumenta.  
  
 Por ejemplo, suponga que una tabla tiene 100 millones de filas y columnas `A`, `B`y `C`. En el escenario 1, la tabla se divide en 1000 particiones en la columna `A`. En el escenario 2, la tabla se dividen en 10.000 particiones en la columna `A`. Una consulta en la tabla que contiene una filtrado de cláusula WHERE en la columna `A` realizará la eliminación de la partición y examinará una partición. La misma consulta puede ejecutarse con mayor rapidez en el escenario 2 al haber menos filas para examinar en una partición. Una consulta que tiene una cláusula de filtrado WHERE en la columna B examina todas las particiones. La consulta puede ejecutarse con mayor rapidez en el escenario 1 que en el escenario 2 ya que hay menos particiones para examinar.  
  
 Las consultas que usan operadores como TOP o MAX/MIN en columnas distintas de la columna de partición pueden experimentar un menor rendimiento con las particiones porque se deben evaluar todas las particiones.  
  
## <a name="behavior-changes-in-statistics-computation-during-partitioned-index-operations"></a>Cambios de comportamiento en el cálculo de estadísticas durante operaciones con particiones de índice  
 A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], las estadísticas no se crean examinando todas las filas de la tabla cuando se crea o se vuelve a generar un índice con particiones. En su lugar, el optimizador de consultas usa el algoritmo de muestreo predeterminado para generar estadísticas. Después de actualizar una base de datos con índices con particiones, puede observar una diferencia en los datos del histograma para estos índices. Este cambio de comportamiento puede no afectar al rendimiento de las consultas. Para obtener estadísticas sobre índices con particiones examinando todas las filas de la tabla, use CREATE STATISTICS o UPDATE STATISTICS con la cláusula FULLSCAN.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Tareas**|**Tema**|  
|Describe cómo crear funciones de partición y esquemas de partición y cómo aplicarlos a una tabla o índice.|[Crear tablas e índices con particiones](create-partitioned-tables-and-indexes.md)|  
|||  
  
## <a name="related-content"></a>Contenido relacionado  
 Puede encontrar las siguientes notas del producto en la tabla con particiones y estrategias e implementaciones de índices útiles.  
  
-   [Estrategias de la tabla con particiones e índices con SQL Server 2008](https://msdn.microsoft.com/library/dd578580\(SQL.100\).aspx)  
  
-   [Cómo implementar una ventana automática deslizante](https://msdn.microsoft.com/library/aa964122\(SQL.90\).aspx)  
  
-   [Carga masiva en una tabla con particiones](https://msdn.microsoft.com/library/cc966380.aspx)  
  
-   [Mejoras de procesamiento de consultas en las tablas e índices con particiones](https://msdn.microsoft.com/library/ms345599.aspx)  
  
-   [Los 10 mejores procedimientos recomendados para compilar un almacén de datos relacionales a gran escala](http://sqlcat.com/top10lists/archive/2008/02/06/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse.aspx)  
  
  
