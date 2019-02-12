---
title: Nivel de compatibilidad de ALTER DATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COMPATIBILITY_LEVEL_TSQL
- COMPATIBILITY_LEVEL
dev_langs:
- TSQL
helpviewer_keywords:
- 80 compatibility level
- ALTER DATABASE statement, compatibility levels
- 90 compatibility level
- compatibility levels [SQL Server]
- 100 compatibility level
- db compatibility level
- db compat level
ms.assetid: ca5fd220-d5ea-4182-8950-55d4101a86f6
author: CarlRabeler
ms.author: carlrab
manager: craigg'
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 40c7f7002bee5567037fbc2de223c292e46e4eba
ms.sourcegitcommit: 97340deee7e17288b5eec2fa275b01128f28e1b8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/30/2019
ms.locfileid: "55421392"
---
# <a name="alter-database-transact-sql-compatibility-level"></a>Nivel de compatibilidad de ALTER DATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Configura varios comportamientos de la base de datos de manera que sean compatibles con la versión especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información sobre otras opciones de ALTER DATABASE, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  

Para obtener más información sobre las convenciones de sintaxis, vea [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).
  
## <a name="syntax"></a>Sintaxis  
  
```  
ALTER DATABASE database_name   
SET COMPATIBILITY_LEVEL = { 150 | 140 | 130 | 120 | 110 | 100 | 90 }  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Es el nombre de la base de datos que se va a modificar.  
  
 COMPATIBILITY_LEVEL { 150 | 140 | 130 | 120 | 110 | 100 | 90 | 80 }  
 Es la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la que se va a hacer compatible la base de datos. Se pueden configurar los siguientes valores de nivel de compatibilidad (no todas las versiones admiten todo el nivel de compatibilidad mencionado anteriormente):  
  
|Product|Versión del motor de base de datos|Designación de nivel de compatibilidad|Valores de nivel de compatibilidad admitidos|  
|-------------|-----------------------------|-------------------------------------|------------------------------------------|  
|[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]|15|150|150, 140, 130, 120, 110, 100| 
|[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|14|140|140, 130, 120, 110, 100|
|Grupo elástico o base de datos única de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|12|130|150, 140, 130, 120, 110, 100|  
|Instancia administrada de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|12|130|150, 140, 130, 120, 110, 100|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|13|130|130, 120, 110, 100|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|12|120|120, 110, 100|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|11|110|110, 100, 90|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|10.5|100|100, 90, 80|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|10|100|100, 90, 80|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|9|90|90, 80|  
|SQL Server 2000|8|80|80|  
  
> [!NOTE]  
> En [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], a partir de **enero de 2018**, el nivel de compatibilidad predeterminado es 140 para las bases de datos recién creadas. No actualizamos el nivel de compatibilidad de las bases de datos existentes. Queda a la elección de los clientes. Dicho esto, recomendamos encarecidamente a los clientes que planeen pasarse al nivel de compatibilidad más reciente para que puedan aprovechar las últimas mejoras.
> 
> Si quiere aprovechar el nivel de compatibilidad de base de datos 140 para su base de datos global pero tiene motivos para quedarse con el modelo de **estimación de cardinalidad** de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], asignado al nivel de compatibilidad de base de datos 110, vea [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) y, en concreto, su palabra clave `LEGACY_CARDINALITY_ESTIMATION = ON`.
>  
> Para más información sobre cómo valorar las diferencias de rendimiento de las consultas más importantes entre dos niveles de compatibilidad de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], vea la [mejora en el rendimiento de las consultas con el nivel de compatibilidad 130 de Azure SQL Database](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/). Tenga en cuenta que en este artículo se hace referencia al nivel de compatibilidad 130 y a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aunque se aplica la misma metodología a los traslados al nivel de compatibilidad 140 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Ejecute la siguiente consulta para conocer la versión del [!INCLUDE[ssDE](../../includes/ssde-md.md)] al que está conectado.  
  
```sql  
SELECT SERVERPROPERTY('ProductVersion');  
```  
  
> [!NOTE]  
> No todas las características que varían según el nivel de compatibilidad se admiten en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  

 Para averiguar el nivel de compatibilidad actual, consulte la columna **compatibility_level** de [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
```sql  
SELECT name, compatibility_level FROM sys.databases;  
```  
  
## <a name="remarks"></a>Notas  
En todas las instalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el nivel de compatibilidad predeterminado se establece en la versión del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Las bases de datos se establecen en este nivel a menos que la base de datos **modelo** tenga un nivel de compatibilidad inferior. Cuando una base de datos se actualiza desde una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], dicha base de datos mantiene su nivel de compatibilidad si es al menos la versión mínima permitida para esa instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Actualizar una base de datos con un nivel de compatibilidad inferior al nivel permitido hace que la base de datos se establezca automáticamente en el nivel de compatibilidad más bajo permitido. Esto se aplica a las bases de datos del usuario y del sistema.   

Se prevén los siguientes comportamientos para [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] cuando se adjunta o se restaura una base de datos, así como después de una actualización local: 
- Si el nivel de compatibilidad de una base de datos de usuario era 100 o superior antes de la actualización, permanece igual después de la misma.    
- Si el nivel de compatibilidad de una base de datos de usuario era 90 antes de la actualización, en la base de datos actualizada el nivel de compatibilidad se establece en 100, que es el nivel de compatibilidad mínimo admitido en [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].    
- Los niveles de compatibilidad de las bases de datos tempdb, model, msdb y Resource quedan establecidos en el nivel de compatibilidad actual después de la actualización.  
- La base de datos del sistema maestra conserva el nivel de compatibilidad que tenía antes de la actualización.

Use `ALTER DATABASE` para cambiar el nivel de compatibilidad de la base de datos. El nuevo nivel de compatibilidad de una base de datos se hace efectivo cuando se emite un comando `USE <database>` o se procesa un nuevo inicio de sesión con esa base de datos como contexto de base de datos predeterminada.     
Para ver el nivel de compatibilidad actual de una base de datos, consulte la columna **compatibility_level** en la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  

> [!NOTE]  
> Una [base de datos de distribución](../../relational-databases/replication/distribution-database.md) creada en una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y que se actualiza a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] RTM o Service Pack 1 tiene el nivel de compatibilidad 90, que no es compatible con otras bases de datos. Esto no afecta a la funcionalidad de la replicación. Si se actualiza a un service pack o a una versión posterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el nivel de compatibilidad de la base de datos de distribución aumentará para coincidir con el de la base de datos **maestra**.

## <a name="compatibility-levels-and-sql-server-upgrades"></a>Niveles de compatibilidad y actualizaciones de SQL Server  
El nivel de compatibilidad de base de datos es una valiosa herramienta que sirve para modernizar las bases de datos, ya que permite actualizar el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] mientras se conserva el estado funcional de las aplicaciones conectadas manteniendo el mismo nivel de compatibilidad de base de datos previo a la actualización. Siempre y cuando la aplicación no necesite aprovechar las mejoras que solo están disponibles en un nivel de compatibilidad de base de datos superior, es un enfoque válido para actualizar el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y mantener el nivel de compatibilidad de base de datos anterior. Para más información sobre el uso del nivel de compatibilidad para la compatibilidad con versiones anteriores, vea la sección [Usar el nivel de compatibilidad para la compatibilidad con versiones anteriores](#using-compatibility-level-for-backward-compatibility), que aparece más adelante en este artículo.    

Para los nuevos trabajos de desarrollos, o en el caso de que una aplicación existente requiera el uso de características nuevas, así como las mejoras de rendimiento efectuadas en el espacio del optimizador de consultas, plantéese actualizar el nivel de compatibilidad de base de datos a la versión más reciente disponible en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y certifique la aplicación para que funcione con ese nivel de compatibilidad. Para obtener más información detallada sobre cómo actualizar el nivel de compatibilidad de base de datos, vea [Prácticas recomendadas para actualizar el nivel de compatibilidad de base de datos](#best-practices-for-upgrading-database-compatibility-level), que aparece más adelante en el artículo.     

> [!TIP] 
> Si una aplicación se ha probado y certificado en una determinada versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quiere decir que se ha probado y certificado implícitamente en ese nivel de compatibilidad de base de datos nativo de la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
> 
> Por lo tanto, el nivel de compatibilidad de base de datos proporciona una ruta de acceso de certificación sencilla para una aplicación existente cuando se usa el nivel de compatibilidad de base de datos correspondiente a la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] probada.
>
> Para más información sobre las diferencias existentes entre los niveles de compatibilidad, vea las secciones correspondientes de este artículo. 

Para actualizar el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] a la versión más reciente manteniendo el nivel de compatibilidad de base de datos que había antes de la actualización y su estado de compatibilidad, se recomienda llevar a cabo una validación del área expuesta funcional estática del código de aplicación en la base de datos. Para ello, debe usar la herramienta [Microsoft Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA). La ausencia de errores en la salida de la herramienta DMA, sobre funcionalidades incompatibles o ausentes, protege la aplicación de cualquier regresión funcional en la nueva versión de destino. Para obtener más información sobre la herramienta DMA, vaya [aquí](https://blogs.msdn.microsoft.com/datamigration/dma).

> [!NOTE] 
> DMA admite el nivel de compatibilidad de base de datos 100 y posterior. Queda excluido [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] como versión de origen. 

> [!IMPORTANT] 
> Microsoft recomienda que se lleven a cabo algunas pruebas mínimas para validar el éxito de una actualización, mientras se mantiene el nivel de compatibilidad de base de datos anterior. Debe determinar qué comprenderían estas pruebas mínimas para su aplicación y su escenario. 

> [!NOTE] 
> Microsoft ofrece protección de formas de los planes de consulta cuando:
> - La nueva versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (destino) se ejecuta en un hardware comparable al hardware en el que se ejecutaba la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior (origen). 
> - Se usa el mismo [nivel de compatibilidad de base de datos admitido](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#remarks) tanto en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino como en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de origen. 
> 
> Se corregirán todas las regresiones de forma de los planes de consulta (en comparación con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de origen) que se produzcan en las condiciones anteriores. Póngase en contacto con el servicio de atención al cliente de Microsoft si es el caso.

## <a name="using-compatibility-level-for-backward-compatibility"></a>Usar el nivel de compatibilidad para la compatibilidad con versiones anteriores  
El valor de configuración de *nivel de compatibilidad de base de datos* afecta solo al comportamiento de la base de datos especificada, y no a todo el servidor. El nivel de compatibilidad de base de datos solo proporciona compatibilidad parcial con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].   

> [!TIP]
> Como el *nivel de compatibilidad de la base de datos* es una configuración de nivel de base de datos, una aplicación que se ejecuta en un [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] más reciente mientras usa un nivel de compatibilidad de la base de datos anterior, de todos modos se pueden aprovechar las mejoras de nivel de servidor sin ningún requisito de cambio de aplicación.
>
> Estos incluyen una supervisión enriquecida y mejoras en la solución de problemas, con nuevas [vista de administración dinámica del sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) y [eventos extendidos](../../relational-databases/extended-events/extended-events.md). Y también mejora la escalabilidad, por ejemplo, con [soft-NUMA automático](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa).

A partir del modo de compatibilidad 130, todas las características nuevas que afectan a los planes de consulta se han agregado únicamente al nuevo nivel de compatibilidad de forma intencionada. La finalidad es minimizar el riesgo durante las actualizaciones que surgen de la disminución del rendimiento debido a cambios en el plan de consulta.   
Desde el plano de las aplicaciones, el objetivo debería seguir siendo actualizar al nivel de compatibilidad más reciente en algún momento para heredar algunas de las nuevas características, así como las mejoras de rendimiento efectuadas en el espacio del optimizador de consultas, pero hacerlo de un modo controlado. Use el nivel de compatibilidad inferior como ayuda más segura para la migración para solucionar diferencias de comportamiento entre las versiones que se controlan con el valor de nivel de compatibilidad correspondiente. Para obtener más información detallada, así como el flujo de trabajo recomendado para actualizar el nivel de compatibilidad de base de datos, vea [Prácticas recomendadas para actualizar el nivel de compatibilidad de base de datos](#best-practices-for-upgrading-database-compatibility-level), que aparece más adelante en el artículo.  
  
> [!IMPORTANT]
> La funcionalidad descontinuada incluida en una determinada versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no está protegida por el nivel de compatibilidad. Esto hace referencia a una funcionalidad que se quitó del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].
> 
> Por ejemplo, la sugerencia `FASTFIRSTROW` está descontinuada en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y se ha reemplazado por la sugerencia `OPTION (FAST n )`. Establecer el nivel de compatibilidad de base de datos en 110 no hará que la sugerencia descontinuada se restaure.
> Para obtener más información sobre las funcionalidades no incluidas, vea [Funcionalidad del motor de base de datos no incluida en SQL Server 2016](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md), [Funcionalidad del motor de base de datos no incluida en SQL Server 2014](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md), [Funcionalidad del motor de base de datos no incluida en SQL Server 2012](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md) y [Funcionalidad del motor de base de datos no incluida en SQL Server 2008](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md).

> [!IMPORTANT]
> Los cambios importantes incluidos en una determinada versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **pueden** no estar protegidos por el nivel de compatibilidad. Esto hace referencia a cambios de comportamiento entre las versiones del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. El comportamiento de [!INCLUDE[tsql](../../includes/tsql-md.md)] suele estar protegido por el nivel de compatibilidad. En cambio, los objetos del sistema eliminados o modificados **no** están protegidos por el nivel de compatibilidad.
>
> Un ejemplo de cambio importante **protegido** por el nivel de compatibilidad es una conversión implícita del tipo de datos datetime a datetime2. En el nivel de compatibilidad de base de datos 130, esto muestra una mayor precisión al reflejar las fracciones de milisegundos, lo que se traduce en diferentes valores convertidos. Para restaurar el comportamiento de conversión anterior, establezca el nivel de compatibilidad de base de datos en 120 o en uno inferior.
>
> Estos son algunos ejemplos de cambios importantes **no protegidos** por el nivel de compatibilidad:
> -  Nombres de columna modificados en objetos del sistema. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] la columna *single_pages_kb* en sys.dm_os_sys_info se ha cambiado a *pages_kb*. Independientemente del nivel de compatibilidad, la consulta `SELECT single_pages_kb FROM sys.dm_os_sys_info` generará el error 207 (Nombre de columna no válido).
> -  Objetos del sistema quitados. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], la columna `sp_dboption` se ha quitado. Independientemente del nivel de compatibilidad, la instrucción `EXEC sp_dboption 'AdventureWorks2016CTP3', 'autoshrink', 'FALSE';` generará el error 2812 (No se encontró el procedimiento almacenado 'sp_dboption').
>
> Para obtener más información sobre los cambios importantes, vea [Cambios importantes en las características del motor de base de datos de SQL Server 2017](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2017.md), [Cambios importantes en las características del motor de base de datos de SQL Server 2016](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md), [Cambios importantes en las características del motor de base de datos de SQL Server 2014](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md), [Cambios importantes en las características del motor de base de datos de SQL Server 2012](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md) y [Cambios importantes en las características del motor de base de datos de SQL Server 2008](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md).
  
## <a name="best-practices-for-upgrading-database-compatibility-level"></a>Prácticas recomendadas para actualizar el nivel de compatibilidad de base de datos 
Para ver el flujo de trabajo recomendado para actualizar el nivel de compatibilidad, vea [Cambiar el modo de compatibilidad de la base de datos y usar el almacén de consultas](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md).  

## <a name="compatibility-levels-and-stored-procedures"></a>Niveles de compatibilidad y procedimientos almacenados  
 Cuando se ejecuta un procedimiento almacenado, se utiliza el nivel de compatibilidad actual de la base de datos en la que se define. Cuando se cambia el nivel de compatibilidad de una base de datos, todos sus procedimientos almacenados se vuelven a compilar de forma automática según sea necesario.  

## <a name="differences-between-compatibility-level-140-and-level-150"></a>Diferencias entre los niveles de compatibilidad 140 y 150  
En esta sección se describen los nuevos comportamientos incluidos en el nivel de compatibilidad 150.

El nivel de compatibilidad 150 de la base de datos está actualmente en versión preliminar pública para [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] y [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]. Este nivel de compatibilidad de la base de datos se asociará con la próxima generación de las mejoras de procesamiento de consultas más allá de lo que se introdujo en el nivel de compatibilidad 140 de la base de datos.     

Para más información sobre las características de procesamiento de consultas habilitadas en el nivel de compatibilidad 150 de la base de datos, consulte [Novedades de SQL Server 2019](../../sql-server/what-s-new-in-sql-server-ver15.md) y [Procesamiento de consultas inteligente en bases de datos SQL](https://docs.microsoft.com/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017).

## <a name="differences-between-compatibility-level-130-and-level-140"></a>Diferencias entre los niveles de compatibilidad 130 y 140  
En esta sección se describen los nuevos comportamientos incluidos en el nivel de compatibilidad 140.

|Nivel de compatibilidad 130 o inferior|Nivel de compatibilidad 140|  
|--------------------------------------------------|-----------------------------------------|  
|En las estimaciones de cardinalidad de las instrucciones que hacen referencia a funciones con valores de tabla de múltiples instrucciones se usa una estimación de fila fija.|En las estimaciones de cardinalidad de las instrucciones que hacen referencia a funciones con valores de tabla de múltiples instrucciones se usará la cardinalidad real de la salida de la función.  Esto es posible gracias a la **ejecución intercalada** de funciones con valores de tabla de múltiples instrucciones.|
|Las consultas de modo por lotes que solicitan tamaños de concesión de memoria insuficiente que resultan en desbordamientos de disco pueden seguir provocando problemas en las ejecuciones consecutivas.|Las consultas de modo por lotes que solicitan tamaños de concesión de memoria insuficiente que resultan en desbordamientos de disco pueden haber mejorado el rendimiento en las ejecuciones consecutivas. Esto es posible a través de los **comentarios de concesión de memoria del modo por lotes**, que actualizarán el tamaño de concesión de memoria de un plan en caché si se han producido desbordamientos en el caso de los operadores de modo por lotes. |
|Las consultas de modo por lotes que solicitan un tamaño de concesión de memoria excesivo que resulta en problemas de simultaneidad pueden seguir provocando problemas en las ejecuciones consecutivas.|Las consultas de modo por lotes que solicitan un tamaño de concesión de memoria excesivo que resulta en problemas de simultaneidad pueden haber mejorado la simultaneidad en las ejecuciones consecutivas. Esto es posible a través de los **comentarios de concesión de memoria del modo por lotes**, que actualizarán el tamaño de concesión de memoria de un plan en caché si se ha solicitado inicialmente una cantidad excesiva.|
|Las consultas de modo por lotes que contienen operadores de combinación son aptas para tres algoritmos de combinación físicos, a saber, bucle anidado, combinación hash y combinación de mezcla. Si las estimaciones de cardinalidad son incorrectas en las entradas de la combinación, existe el riesgo de seleccionar un algoritmo de combinación inadecuado. Si esto sucede, el rendimiento se verá afectado y el algoritmo de combinación incorrecto seguirá en uso hasta que el plan en caché se vuelva a compilar.|Hay otro operador de combinación denominado **combinación adaptable**. Si las estimaciones de cardinalidad son incorrectas en la entrada de combinación externa, existe el riesgo de seleccionar un algoritmo de combinación inadecuado. Si esto sucede y la instrucción es apta para una combinación adaptable, se usará dinámicamente un bucle anidado en las entradas de combinación más pequeñas y una combinación hash en las entradas de combinación mayores, sin necesidad de volver a compilar. |
|Los planes triviales que hacen referencia a índices de almacén de columnas no son aptos para ejecutarse en el modo por lotes. |Un plan trivial que hace referencia a índices de almacén de columnas se descartarán en favor de un plan que sea apto para ejecutarse en el modo por lotes.|
|El operador UDX `sp_execute_external_script` solo se puede ejecutar en el modo de fila.|El operador UDX `sp_execute_external_script` se puede usar en la ejecución del modo por lotes.|  
|Las funciones con valores de tabla de múltiples instrucciones carecen de ejecución intercalada. |La ejecución intercalada es posible en las funciones con valores de tabla de múltiples instrucciones para mejorar la calidad del plan.|

Las correcciones incluidas en la marca de seguimiento 4199 en versiones de SQL Server anteriores a SQL Server 2017 ahora están habilitadas de forma predeterminada en el modo de compatibilidad 140. La marca de seguimiento 4199 sigue siendo aplicable a las nuevas correcciones del optimizador de consultas que se publiquen después de SQL Server 2017. Para más información sobre la marca de seguimiento 4199, vea la [marca de seguimiento 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199).  
  
## <a name="differences-between-compatibility-level-120-and-level-130"></a>Diferencias entre los niveles de compatibilidad 120 y 130  
En esta sección se describen los nuevos comportamientos incluidos en el nivel de compatibilidad 130.   

|Nivel de compatibilidad 120 o inferior|Nivel de compatibilidad 130|  
|--------------------------------------------------|-----------------------------------------|  
|La instrucción INSERT en una instrucción INSERT-SELECT es de subproceso único.|La instrucción INSERT en una instrucción INSERT-SELECT es multiproceso o puede tener un plan paralelo.|  
|Las consultas en una tabla optimizada para memoria ejecutan un único subproceso.|Ahora, las consultas en una tabla optimizada para memoria pueden tener planes paralelos.|  
|Incluyó el programa de estimación de cardinalidad de SQL 2014 **CardinalityEstimationModelVersion="120"**.|Más mejoras en la estimación de cardinalidad con el modelo de estimación de cardinalidad 130, que es visible desde una consulta. **CardinalityEstimationModelVersion="130"**| 
|Cambios del modo por lotes frente al modo de fila con índices de almacén de columnas:<br /><ul><li>Las ordenaciones en una tabla con índice de almacén de columnas se producen en el modo de fila. <li>Los agregados de función basados en ventanas funcionan en el modo de fila, como `LAG` o `LEAD`. <li>Las consultas en tablas de almacén de columnas con varias cláusulas Distinct funcionaban en el modo de fila. <li>Las consultas que se ejecutan con Maxdop1 o un plan de consulta en serie se ejecutaban en el modo de fila.</li></ul>| Cambios del modo por lotes frente al modo de fila con índices de almacén de columnas:<br /><ul><li>Ahora, las ordenaciones en una tabla con índice de almacén de columnas se producen en el modo por lotes. <li>Ahora, los agregados basados en ventanas funcionan en el modo por lotes, como `LAG` o `LEAD`. <li>Las consultas en tablas de almacén de columnas con varias cláusulas Distinct funcionaban en el modo por lotes. <li>Las consultas que se ejecutan con MAXDOP 1 o con un plan de consulta en serie se ejecutan en el modo por lotes.</li></ul>|  
|Las estadísticas se pueden actualizar automáticamente. | La lógica que actualiza las estadísticas automáticamente es más agresiva en tablas grandes.  En la práctica, esto debería reducir los casos en los que los clientes advierten problemas de rendimiento en las consultas donde las filas recién insertadas se consultan con frecuencia, pero las estadísticas no se habían actualizado para incluir esos valores. |  
|La marca de seguimiento 2371 está desactivada de forma predeterminada en [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. | La [marca de seguimiento 2371](https://blogs.msdn.microsoft.com/psssql/2016/10/04/default-auto-statistics-update-threshold-change-for-sql-server-2016/) está activada de forma predeterminada en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. La marca de seguimiento 2371 indica al actualizador automático de estadísticas que muestree un subconjunto de filas más pequeño, pero más práctico, en una tabla que tiene un gran número de filas. <br/> <br/> Una mejora consiste en incluir en el ejemplo más filas que se hayan insertado hace poco. <br/> <br/> Otra mejora es permitir que las consultas se ejecuten mientras el proceso de actualización de estadísticas se ejecuta, en lugar de bloquearlas. |  
|En el nivel 120, las estadísticas se muestrean a través de un proceso de *subproceso único*.|En el nivel 130, las estadísticas se muestrean a través de un proceso *multiproceso*. |  
|El límite está establecido en 253 claves externas entrantes.| Hasta 10 000 claves externas entrantes (o referencias similares) pueden hacer referencia a una determinada tabla. Para ver las restricciones, vea [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md). |  
|Se permiten los algoritmos hash en desuso MD2, MD4, MD5, SHA y SHA1.|Solo se permiten los algoritmos hash SHA2_256 y SHA2_512.|
||[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] incluye mejoras en algunas operaciones (bastante infrecuentes) y conversiones de tipos de datos. Para más información, vea [SQL Server 2016 improvements in handling some data types and uncommon operations](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon) (Mejoras de SQL Server 2016 en el tratamiento de algunos tipos de datos y operaciones infrecuentes).|
|La función STRING_SPLIT no está disponible.|La función STRING_SPLIT está disponible en el nivel de compatibilidad 130 o superior. Si el nivel de compatibilidad de la base de datos es inferior a 130, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no podrá encontrar ni ejecutar la función STRING_SPLIT.|
  
Las correcciones incluidas en la marca de seguimiento 4199 en versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ahora están habilitadas de forma predeterminada en el modo de compatibilidad 130. La marca de seguimiento 4199 sigue siendo aplicable a las nuevas correcciones del optimizador de consultas que se publiquen después de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Para usar el optimizador de consultas anterior en [!INCLUDE[ssSDS](../../includes/sssds-md.md)], hay que seleccionar el nivel de compatibilidad 110. Para más información sobre la marca de seguimiento 4199, vea la [marca de seguimiento 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199).  
  
## <a name="differences-between-lower-compatibility-levels-and-level-120"></a>Diferencias entre los niveles de compatibilidad inferiores y el nivel 120  
 En esta sección se describen nuevos comportamientos incluidos con el nivel de compatibilidad 120.  
  
|Nivel de compatibilidad 110 o inferior|Nivel de compatibilidad 120|  
|--------------------------------------------------|-----------------------------------------|  
|Se utiliza el optimizador de consultas más antiguo.|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] incluye mejoras sustanciales en el componente que crea y optimiza los planes de consulta. Esta nueva característica del optimizador de consultas depende del uso del nivel 120 de compatibilidad de base de datos. Para aprovecharse estas mejoras, las nuevas aplicaciones de base de datos deben desarrollarse con el nivel 120 de compatibilidad de base de datos. Las aplicaciones migradas de versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben probarse cuidadosamente para confirmar que el buen rendimiento se ha mantenido o se ha mejorado. Si el rendimiento se degrada, puede establecer la compatibilidad de base de datos en el nivel 110 o inferior para usar la anterior metodología del optimizador de consultas.<br /><br /> El nivel de compatibilidad de la base de datos 120 usa un nuevo estimador de cardinalidad que está optimizado para cargas de trabajo modernas de almacenamiento de datos y OLTP. Antes de establecer el nivel de compatibilidad de la base de datos en 110 debido a problemas de rendimiento, vea las recomendaciones incluidas en la sección Planes de consulta del tema de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [Novedades de Motor de base de datos](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md).|  
|En niveles de compatibilidad inferiores a 120, la configuración de idioma se omite al convertir un valor **date** en un valor de cadena. Cabe mencionar que este comportamiento es específico exclusivamente del tipo **date**. Vea el ejemplo B de la sección Ejemplos más abajo.|La configuración de idioma no se omite al convertir un valor **date** en un valor de cadena.|  
|Las referencias recursivas en el lado derecho de una cláusula `EXCEPT` crean un bucle infinito. Este comportamiento se detalla en el ejemplo C de la sección Ejemplos más abajo.|Las referencias recursivas en una cláusula `EXCEPT` generan un error de acuerdo con el estándar ANSI SQL.|  
|La expresión de tabla común (CTE) recursiva permite el uso de nombres de columna duplicados.|CTE recursiva no admite nombres de columna duplicados.|  
|Los desencadenadores deshabilitados se habilitan si se modifican los desencadenadores.|Modificar un desencadenador no cambia el estado (habilitado o deshabilitado) del mismo.|  
|La cláusula de la tabla OUTPUT INTO omite `IDENTITY_INSERT SETTING = OFF` y permite que se inserten valores explícitos.|No puede insertar valores explícitos relativos a una columna de identidad en una tabla cuando `IDENTITY_INSERT` está establecido en OFF.|  
|Cuando la contención de la base de datos está establecida en parcial, al validar el campo `$action` en la cláusula `OUTPUT` de una instrucción `MERGE`, se puede devolver un error de intercalación.|La intercalación de los valores devueltos por la cláusula `$action` de una instrucción `MERGE` es la intercalación de base de datos en lugar de la intercalación de servidor y no se devuelve un error de conflicto de intercalación.|  
|Una instrucción `SELECT INTO` siempre crea una operación de inserción de subproceso único.|Una instrucción `SELECT INTO` puede crear una operación de inserción en paralelo. Al insertar un gran número de filas, la operación paralela puede mejorar el rendimiento.|  
  
## <a name="differences-between-lower-compatibility-levels-and-levels-110-and-120"></a>Diferencias entre los niveles de compatibilidad inferiores y los niveles 110 y 120  
 En esta sección se describen nuevos comportamientos incluidos con nivel de compatibilidad 110.   Esta sección también se aplica al nivel 120.  
  
|Nivel de compatibilidad 100 o inferior|Configuración de nivel de compatibilidad de al menos 110|  
|--------------------------------------------------|--------------------------------------------------|  
|Los objetos de base de datos de Common Language Runtime (CLR) se ejecutan con la versión 4 de CLR. Sin embargo, algunos cambios de comportamiento incluidos en la versión 4 de CLR se evitan. Para más información, vea [What's New in CLR Integration](../../relational-databases/clr-integration/clr-integration-what-s-new.md) (Novedades en la integración con CLR).|Los objetos de base de datos de CLR se ejecutan con la versión 4 de CLR.|  
|Las funciones de XQuery **string-length** y **substring** cuentan cada suplente como dos caracteres.|Las funciones de XQuery **string-length** y **substring** cuentan cada suplente como un carácter.|  
|`PIVOT` se permite en una consulta de expresión de tabla común (CTE) recursiva. Sin embargo, la consulta devuelve resultados incorrectos cuando hay varias filas por agrupación.|`PIVOT` no se permite en una consulta de expresión de tabla común (CTE) recursiva. Se devuelve un error.|  
|El algoritmo RC4 se admite únicamente por razones de compatibilidad con versiones anteriores. El material nuevo solo se puede cifrar con RC4 o RC4_128 cuando la base de datos tenga el nivel de compatibilidad 90 o 100. (No se recomienda). En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], el material cifrado con RC4 o RC4_128 se puede descifrar en cualquier nivel de compatibilidad.|El nuevo material no se puede cifrar mediante RC4 o RC4_128. Use un algoritmo más reciente como uno de los algoritmos AES en su lugar. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], el material cifrado con RC4 o RC4_128 se puede descifrar en cualquier nivel de compatibilidad.|  
|El estilo predeterminado de las operaciones `CAST` y `CONVERT` en los tipos de datos **time** y **datetime2** es 121, a menos que se use un tipo en una expresión de columna calculada. Para las columnas calculadas, el estilo predeterminado es 0. Este comportamiento afecta a las columnas calculadas cuando se crean, cuando se utilizan en las consultas que implican parametrización automática o cuando se usan en definiciones de restricciones.<br /><br /> En el ejemplo D de la sección Ejemplos más abajo se muestra la diferencia entre los estilos 0 y 121. No se muestra el comportamiento descrito anteriormente. Para más información sobre los estilos de fecha y hora, vea [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).|En el nivel de compatibilidad 110, el estilo predeterminado de las operaciones `CAST` y `CONVERT` en los tipos de datos **time** y **datetime2** es siempre 121. Si su consulta se basa en el comportamiento anterior, use un nivel de compatibilidad menor de 110, o especifique explícitamente el estilo 0 en la consulta correspondiente.<br /><br /> Actualizar la base de datos al nivel de compatibilidad 110 no cambiará los datos de usuario que se hayan almacenado en disco. Debe corregir manualmente estos datos según convenga. Por ejemplo, si usa `SELECT INTO` para crear una tabla de un origen que contenía una expresión de columna calculada como la descrita anteriormente, los datos se almacenarían (si se usa el estilo 0) en lugar de la propia definición de columna calculada. Debería actualizar manualmente estos datos para que coincidieran con el estilo 121.|  
|Cualquier columna de las tablas remotas de tipo **smalldatetime** a la que se haga referencia en una vista con particiones se asignará como **datetime**. Las columnas correspondientes de tablas locales (en la misma posición ordinal en la lista de selección) deben ser **datetime**.|Cualquier columna de las tablas remotas de tipo **smalldatetime** a la que se haga referencia en una vista con particiones se asignará como **smalldatetime**. Las columnas correspondientes de tablas locales (en la misma posición ordinal en la lista de selección) deben ser **smalldatetime**.<br /><br /> Después de actualizar a 110, la vista distribuida con particiones producirá un error debido a una discrepancia en los tipos de datos. Puede resolver este problema cambiando el tipo de datos en la tabla remota a **datetime** o estableciendo el nivel de compatibilidad de la base de datos local en 100 o menos.|  
|La función `SOUNDEX` implementa las siguientes reglas:<br /><br /> 1) Las letras H o W mayúsculas se omiten al separar dos consonantes que tienen el mismo número del código `SOUNDEX`.<br /><br /> 2) Si los dos primeros caracteres de *character_expression* tienen el mismo número del código de `SOUNDEX`, ambos caracteres se incluyen. Si un conjunto de consonantes en paralelo tiene el mismo número del código de `SOUNDEX`, se excluyen todas excepto la primera.|La función `SOUNDEX` implementa las siguientes reglas:<br /><br /> 1) Si H o W mayúsculas separan dos consonantes que tienen el mismo número en el código `SOUNDEX`, se omite la consonante de la derecha.<br /><br /> 2) Si un conjunto de consonantes en paralelo tiene el mismo número del código de `SOUNDEX`, se excluyen todas excepto la primera.<br /><br /> <br /><br /> Las reglas adicionales pueden causar que los valores calculados por la función `SOUNDEX` sean diferentes de los calculados en niveles de compatibilidad menores. Después de actualizar al nivel de compatibilidad 110, es posible que tenga que regenerar los índices, los montones o las restricciones CHECK que usan la función `SOUNDEX`. Para más información, vea [SOUNDEX &#40;Transact-SQL&#41;](../../t-sql/functions/soundex-transact-sql.md).|  
  
## <a name="differences-between-compatibility-level-90-and-level-100"></a>Diferencias entre los niveles de compatibilidad 90 y 100  
 En esta sección se describen nuevos comportamientos incluidos con nivel de compatibilidad 100.  
  
|Nivel de compatibilidad 90|Nivel de compatibilidad 100|Posibilidad de impacto|  
|----------------------------------------|-----------------------------------------|---------------------------|  
|El valor QUOTED_IDENTIFER siempre está establecido en ON para las funciones con valores de tabla con múltiples instrucciones cuando se crean sin tener en cuenta el valor de nivel de sesión.|El valor de sesión de QUOTED IDENTIFIER se cumple cuando se crean funciones con valores de tabla con múltiples instrucciones.|Media|  
|Al crear o modificar una función de partición, los literales **datetime** y **smalldatetime** de la función se evalúan suponiendo que US_English es la configuración de idioma.|La configuración de idioma actual se usa para evaluar los literales **datetime** y **smalldatetime** en la función de partición.|Media|  
|La cláusula `FOR BROWSE` se admite (y se omite) en las instrucciones `INSERT` y `SELECT INTO`.|La cláusula `FOR BROWSE` no se admite en las instrucciones `INSERT` y `SELECT INTO`.|Media|  
|Los predicados de texto completo se permiten en la cláusula `OUTPUT`.|Los predicados de texto completo no se permiten en la cláusula `OUTPUT`.|Baja|  
|No se admite `CREATE FULLTEXT STOPLIST`, `ALTER FULLTEXT STOPLIST` ni `DROP FULLTEXT STOPLIST`. La lista de palabras irrelevantes del sistema se asocia automáticamente a nuevos índices de texto completo.|Se admite `CREATE FULLTEXT STOPLIST`, `ALTER FULLTEXT STOPLIST` y `DROP FULLTEXT STOPLIST`.|Baja|  
|`MERGE` no se aplica como una palabra clave reservada.|MERGE es una palabra clave totalmente reservada. La instrucción `MERGE` se admite por debajo de los niveles de compatibilidad 100 y 90.|Baja|  
|Al usar el argumento \<dml_table_source> de la instrucción INSERT, se genera un error de sintaxis.|Puede capturar los resultados de una cláusula OUTPUT en una instrucción anidada INSERT, UPDATE, DELETE o MERGE, e insertar los resultados obtenidos en una vista o tabla de destino. Para ello, es necesario usar el argumento \<dml_table_source> de la instrucción INSERT.|Baja|
|A menos que se especifique `NOINDEX`, `DBCC CHECKDB` o `DBCC CHECKTABLE` realizan comprobaciones de coherencia física y lógica en una sola tabla o vista indexada, y en todos sus índices XML y no agrupados. Los índices espaciales no se admiten.|A menos que se especifique `NOINDEX`, `DBCC CHECKDB` o `DBCC CHECKTABLE` realizan comprobaciones de coherencia física y lógica en una sola tabla y en todos sus índices no agrupados. Sin embargo, en los índices XML, índices espaciales y vistas indexadas solamente se realizan comprobaciones de coherencia física de forma predeterminada.<br /><br /> Si se especifica `WITH EXTENDED_LOGICAL_CHECKS`, se realizan comprobaciones lógicas en las vistas indexadas, índices XML e índices espaciales, si los hay. De forma predeterminada, las comprobaciones de coherencia física se realizan antes que las comprobaciones de coherencia lógica. Si también se especifica `NOINDEX`, solamente se realizarán las comprobaciones lógicas.|Baja|  
|Cuando una cláusula OUTPUT se utiliza con una instrucción del lenguaje de manipulación de datos (DML) y se produce un error en tiempo de ejecución durante la ejecución de la instrucción, toda la transacción se termina y se revierte.|Cuando una cláusula `OUTPUT` se usa con una instrucción del lenguaje de manipulación de datos (DML) y ocurre un error en tiempo de ejecución durante la ejecución de la instrucción, el comportamiento depende del valor de `SET XACT_ABORT`. Si `SET XACT_ABORT` es OFF, un error de anulación de la instrucción generado por la instrucción DML que usa la cláusula `OUTPUT` terminará la instrucción, pero la ejecución del lote continúa y la transacción no se revierte. Si `SET XACT_ABORT` es ON, todos los errores en tiempo de ejecución generados por la instrucción DML que usa la cláusula OUTPUT terminarán el lote y la transacción se revertirá.|Baja|  
|CUBE y ROLLUP no se exigen como palabras clave reservadas.|`CUBE` y `ROLLUP` son palabras clave reservadas dentro de la cláusula GROUP BY.|Baja|  
|A los elementos de tipo **anyType** de XML se les aplica una validación estricta.|A los elementos de tipo **anyType** de XML se les aplica una validación flexible. Para más información, vea [Componentes comodín y validación del contenido](../../relational-databases/xml/wildcard-components-and-content-validation.md).|Baja|  
|Los atributos especiales **xsi:nil** y **xsi:type** no se pueden consultar ni modificar con instrucciones del lenguaje de manipulación de datos (DML).<br /><br /> Esto significa que `/e/@xsi:nil` genera un error mientras que `/e/@*` omite los atributos **xsi:nil** y **xsi:type**. En cambio, `/e` devuelve los atributos **xsi:nil** y **xsi:type** por coherencia con `SELECT xmlCol`, aun cuando `xsi:nil = "false"`.|Los atributos especiales **xsi:nil** y **xsi:type** se almacenan como atributos regulares y se puede consultar y modificar.<br /><br /> Por ejemplo, al ejecutar la consulta `SELECT x.query('a/b/@*')`, se devuelven todos los atributos incluidos **xsi:nil** y **xsi:type**. Para excluir estos tipos en la consulta, reemplace `@*` por `@*[namespace-uri(.) != "`*insert xsi namespace uri*`"` y no `(local-name(.) = "type"` ni `local-name(.) ="nil".`.|Baja|  
|Una función definida por el usuario que convierta un valor de cadena constante XML en un tipo datetime de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se marca como determinista.|Una función definida por el usuario que convierta un valor de cadena constante XML a un tipo datetime de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se marca como no determinista.|Baja|  
|Los tipos de lista y unión de XML no se admiten por completo.|Los tipos de lista y unión que se admiten totalmente incluyen la funcionalidad siguiente:<br /><br /> Unión de lista<br /><br /> Unión de unión<br /><br /> Lista de tipos atómicos<br /><br /> Lista de unión|Baja|  
|Las opciones de SET requeridas para un método de XQuery no se validan cuando el método está contenido en una vista o función con valores de tabla insertados.|Las opciones de SET requeridas para un método de XQuery se validan cuando el método está contenido en una vista o función con valores de tabla insertados. Se produce un error si las opciones de SET del método se establecen incorrectamente.|Baja|  
|Los valores de los atributos XML que contienen caracteres de fin de línea (retorno de carro y avance de línea) no se normalizan según el estándar XML. Es decir, ambos caracteres se devuelven en lugar de un único carácter de avance de línea.|Los valores de los atributos XML que contienen caracteres de fin de línea (retorno de carro y avance de línea) se normalizan de acuerdo con el estándar XML. Es decir, todos los saltos de línea de las entidades externas analizadas (incluidas las de documento) se normalizan en la entrada traduciendo la secuencia de dos caracteres #xD #xA y cualquier #xD al que no siga #xA por un solo carácter #xA.<br /><br /> Las aplicaciones que utilizan atributos para transportar los valores de cadena que contienen caracteres de fin de línea no recibirán de vuelta estos caracteres a medida que se envíen. Para evitar el proceso de normalización, utilice entidades de caracteres numéricos XML para codificar todos los caracteres de fin de línea.|Baja|  
|Las propiedades de columna `ROWGUIDCOL` e `IDENTITY` se pueden denominar incorrectamente como una restricción. Por ejemplo, la instrucción `CREATE TABLE T (C1 int CONSTRAINT MyConstraint IDENTITY)` se ejecuta, pero el nombre de restricción no se conserva y no es accesible para el usuario.|Las propiedades de columna `ROWGUIDCOL` e `IDENTITY` no se pueden denominar como una restricción. Se devuelve el error 156.|Baja|  
|Al actualizar las columnas mediante una asignación bidireccional como `UPDATE T1 SET @v = column_name = <expression>`, se pueden generar resultados inesperados porque durante la ejecución de la instrucción se puede usar el valor real de la variable en otras cláusulas como `WHERE` y `ON` en lugar del valor inicial de la instrucción. Esto puede hacer que los significados de los predicados cambien de forma imprevisible según cada fila.<br /><br /> Este comportamiento solo es aplicable cuando el nivel de compatibilidad está establecido en 90.|Al actualizar las columnas utilizando una asignación bidireccional, se generan los resultados previstos porque solo se obtiene acceso al valor inicial de la columna de la instrucción durante la ejecución de la misma.|Baja|  
|Vea el ejemplo E en la sección Ejemplos más abajo.|Vea el ejemplo F en la sección Ejemplos más abajo.|Baja|  
|La función ODBC {fn CONVERT()} utiliza el formato de fecha predeterminado del lenguaje. En algunos lenguajes, el formato predeterminado es ADM, lo que puede producir errores de conversión cuando CONVERT() se combina con otras funciones, como `{fn CURDATE()}`, que espera un formato AMD.|La función ODBC `{fn CONVERT()}` usa el estilo 121 (un formato AMD independiente del lenguaje) al convertir a los tipos de datos ODBC SQL_TIMESTAMP, SQL_DATE, SQL_TIME, SQLDATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP.|Baja|  
|Los tipos de fecha y hora intrínsecos como DATEPART no requieren que los valores de entrada de cadena sean literales de fecha y hora válidos. Por ejemplo, `SELECT DATEPART (year, '2007/05-30')` se compila correctamente.|Los tipos de fecha y hora intrínsecos como `DATEPART` requieren que los valores de entrada de cadena sean literales de fecha y hora válidos. Se devuelve el error 241 cuando se utiliza un literal de fecha y hora no válido.|Baja|  
  
## <a name="reserved-keywords"></a>Palabras clave reservadas  
 El nivel de compatibilidad también determina las palabras clave reservadas por el [!INCLUDE[ssDE](../../includes/ssde-md.md)]. En la tabla siguiente se muestran las palabras clave reservadas que inserta cada nivel de compatibilidad.  
  
|Nivel de compatibilidad|Palabras clave reservadas|  
|----------------------------------|-----------------------|  
|130|por determinar.|  
|120|Ninguno.|  
|110|WITHIN GROUP, TRY_CONVERT, SEMANTICKEYPHRASETABLE, SEMANTICSIMILARITYDETAILSTABLE, SEMANTICSIMILARITYTABLE|  
|100|CUBE, MERGE, ROLLUP|  
|90|EXTERNAL, PIVOT, UNPIVOT, REVERT, TABLESAMPLE|  
  
 En un nivel de compatibilidad dado, las palabras clave reservadas incluyen todas las palabras clave insertadas en ese nivel o debajo del mismo. Por ejemplo, para aplicaciones en el nivel 110, todas las palabras clave mostradas en la tabla anterior son reservadas. En los niveles de compatibilidad inferiores, las palabras clave del nivel 100 siguen siendo nombres de objeto válidos, pero las características de idioma del nivel 110 correspondientes a esas palabras clave no están disponibles.  
  
 Una vez insertada, una palabra clave permanece reservada. Por ejemplo, la palabra clave reservada PIVOT, que se introdujo en el nivel de compatibilidad 90, también está reservada en los niveles 100, 110 y 120.  
  
 Si una aplicación utiliza un identificador que está reservado como palabra clave para su nivel de compatibilidad, la aplicación generará un error. Para resolver este problema, incluya el identificador entre corchetes (**[]**) o comillas (**""**); por ejemplo, para actualizar una aplicación que usa el identificador **EXTERNAL** al nivel de compatibilidad 90, puede cambiar el identificador a **[EXTERNAL]** o **"EXTERNAL"**.  
  
 Para obtener más información, vea [Palabras clave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-compatibility-level"></a>A. Cambiar el nivel de compatibilidad  
 En el siguiente ejemplo se cambia el nivel de compatibilidad de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] a `110,`[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 110;  
GO  
```  
  
 En el siguiente ejemplo se devuelve el nivel de compatibilidad de la base de datos actual.  
  
```sql  
SELECT name, compatibility_level   
FROM sys.databases   
WHERE name = db_name();  
```  
  
### <a name="b-ignoring--the-set-language-statement-except-under-compatibility-level-120"></a>b. Omitir la instrucción SET LANGUAGE excepto en el nivel de compatibilidad 120  
 La siguiente consulta omite la instrucción SET LANGUAGE excepto en el nivel de compatibilidad 120.  
  
```sql  
SET DATEFORMAT dmy;   
DECLARE @t2 date = '12/5/2011' ;  
SET LANGUAGE dutch;   
SELECT CONVERT(varchar(11), @t2, 106);   
  
-- Results when the compatibility level is less than 120.   
12 May 2011   
  
-- Results when the compatibility level is set to 120).  
12 mei 2011  
```  
  
### <a name="c"></a>C.  
 En el nivel de compatibilidad 110 o inferior, las referencias recursivas en el lado derecho de una cláusula EXCEPT crean un bucle infinito.  
  
```sql  
WITH   
cte AS (SELECT * FROM (VALUES (1),(2),(3)) v (a)),  
r   
AS (SELECT a FROM Table1  
UNION ALL  
(SELECT a FROM Table1 EXCEPT SELECT a FROM r) )   
SELECT a   
FROM r;  
  
```  
  
### <a name="d"></a>D.  
 En el siguiente ejemplo se muestra la diferencia entre los estilos 0 y 121. Para más información sobre los estilos de fecha y hora, vea [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
```sql  
CREATE TABLE t1 (c1 time(7), c2 datetime2);   
  
INSERT t1 (c1,c2) VALUES (GETDATE(), GETDATE());  
  
SELECT CONVERT(nvarchar(16),c1,0) AS TimeStyle0  
       ,CONVERT(nvarchar(16),c1,121)AS TimeStyle121  
       ,CONVERT(nvarchar(32),c2,0) AS Datetime2Style0  
       ,CONVERT(nvarchar(32),c2,121)AS Datetime2Style121  
FROM t1;  
  
-- Returns values such as the following.  
TimeStyle0       TimeStyle121       
Datetime2Style0      Datetime2Style121  
---------------- ----------------   
-------------------- --------------------------  
3:15PM           15:15:35.8100000   
Jun  7 2011  3:15PM  2011-06-07 15:15:35.8130000  
```  
  
### <a name="e"></a>E.  
 La asignación de variables se permite en una instrucción que contenga un operador UNION de nivel superior, pero devuelve resultados inesperados. Por ejemplo, en las instrucciones siguientes, a `@v` se le asigna el valor de la columna `BusinessEntityID` a partir de la unión de dos tablas. Por definición, si la instrucción SELECT devuelve más de un valor, se asigna a la variable el último valor devuelto. En este caso, a la variable se le asigna correctamente el último valor, sin embargo, también se devuelve el conjunto de resultados de la instrucción SELECT UNION.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET compatibility_level = 110;  
GO  
USE AdventureWorks2012;  
GO  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM HumanResources.Employee  
UNION ALL  
SELECT @v = BusinessEntityID FROM HumanResources.EmployeeAddress;  
SELECT @v;  
```  
  
### <a name="f"></a>F.  
 No se permite la asignación de variables en una instrucción que contiene un operador UNION de nivel superior. Se devuelve el error 10734. Para resolver el error, reescriba la consulta según se muestra en el ejemplo siguiente.  
  
```sql  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM   
    (SELECT BusinessEntityID FROM HumanResources.Employee  
     UNION ALL  
     SELECT BusinessEntityID FROM HumanResources.EmployeeAddress) AS Test;  
SELECT @v;  
```  
  
## <a name="see-also"></a>Consulte también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Palabras clave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
 [Ver o cambiar el nivel de compatibilidad de una base de datos](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) 
  
