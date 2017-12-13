---
title: MODIFICAR el nivel de compatibilidad de base de datos (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 12/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COMPATIBILITY_LEVEL_TSQL
- COMPATIBILITY_LEVEL
dev_langs: TSQL
helpviewer_keywords:
- 80 compatibility level
- ALTER DATABASE statement, compatibility levels
- 90 compatibility level
- compatibility levels [SQL Server]
- 100 compatibility level
ms.assetid: ca5fd220-d5ea-4182-8950-55d4101a86f6
caps.latest.revision: "89"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b418634c714fda6dfd0e339e42c7b584436c5433
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="alter-database-transact-sql-compatibility-level"></a>Nivel de compatibilidad de ALTER DATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  
Configura varios comportamientos de la base de datos de manera que sean compatibles con la versión especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para ver otras opciones de ALTER DATABASE, consulte [ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ALTER DATABASE database_name   
SET COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 | 90 }  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Es el nombre de la base de datos que se va a modificar.  
  
 COMPATIBILITY_LEVEL {140 | 130 | 120 | 110 | 100 | 90 | 80}  
 Es la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la que se va a hacer compatible la base de datos. Se pueden configurar los valores de nivel de compatibilidad siguientes:  
  
|Product|Versión del motor de base de datos|Designación de nivel de compatibilidad|Valores de nivel de compatibilidad admitidos|  
|-------------|-----------------------------|-------------------------------------|------------------------------------------|  
|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]|14|140|140, 130, 120, 110, 100|
|[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|12|130|140, 130, 120, 110, 100|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|13|130|130, 120, 110, 100|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|12|120|120, 110, 100|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|11|110|110, 100, 90|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|10.5|100|100, 90, 80|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|10|100|100, 90, 80|  
|Resultado de|9|90|90, 80|  
|SQL Server 2000|8|80|80|  
  
> [!NOTE]  
>  **La base de datos de SQL Azure** V12 se lanzó en diciembre de 2014. Uno de los aspectos de esa versión fue que acaba de crear las bases de datos tenían su nivel de compatibilidad establecido en 120. En 2015 base de datos SQL comenzó a compatibilidad con el nivel 130, aunque el valor predeterminado permanecido como 120.  
> 
> A partir de **mid junio de 2016**, en la base de datos de SQL Azure, el nivel de compatibilidad predeterminado son 130 en lugar de 120 para **recién creado** bases de datos. Bases de datos existentes creados antes de mediados de junio de 2016 no se ven afectados y mantengan su nivel de compatibilidad actual (100, 110 o 120). 
> 
> Si desea nivel 130 para la base de datos por lo general, pero tienes razón por la que prefiera el nivel 110 **estimación de cardinalidad** algoritmo, vea [ALTER DATABASE SCOPED CONFIGURATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)y, en particular la palabra clave LEGACY_CARDINALITY_ESTIMATION = ON.  
>  
>  Para obtener más información acerca de cómo evaluar las diferencias de rendimiento de las consultas más importantes, entre dos niveles de compatibilidad de base de datos de SQL Azure, consulte [mejora el rendimiento de la consulta con 130 de nivel de compatibilidad de base de datos de SQL Azure](http://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/).


 Ejecute la siguiente consulta para determinar la versión de la [!INCLUDE[ssDE](../../includes/ssde-md.md)] que están conectados a.  
  
```tsql  
SELECT SERVERPROPERTY('ProductVersion');  
```  
  
> [!NOTE]  
>  No todas las características que varían según el nivel de compatibilidad se admiten en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  

 Para determinar el nivel de compatibilidad actual, consulte la **compatibility_level** columna de [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
```tsql  
SELECT name, compatibility_level FROM sys.databases;  
```  
  
## <a name="remarks"></a>Comentarios  
 Para todas las instalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el nivel de compatibilidad predeterminado se establece en la versión de la [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Las bases de datos se establecen en este nivel, a menos que la **modelo** base de datos tiene un nivel de compatibilidad inferior. Cuando se actualiza una base de datos desde cualquier versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la base de datos mantiene su nivel de compatibilidad si es al menos mínimo permitido para esa instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Actualizar una base de datos con un nivel de compatibilidad inferior al nivel permitido, Establece la base de datos para la compatibilidad menor nivel permitida. Esto se aplica a las bases de datos del usuario y del sistema. Use **ALTER DATABASE** para cambiar el nivel de compatibilidad de la base de datos. Para ver el nivel de compatibilidad actual de una base de datos, consulte el **compatibility_level** columna en el **sys.databases** vista de catálogo.  

  
## <a name="using-compatibility-level-for-backward-compatibility"></a>Usar el nivel de compatibilidad para la compatibilidad con versiones anteriores  
 El nivel de compatibilidad afecta solo al comportamiento de la base de datos especificada y no a todo el servidor. El nivel de compatibilidad solo proporciona compatibilidad parcial con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A partir de modo de compatibilidad 130, se agregaron las nuevas características que afectan a plan de consulta solo para el nuevo modo de compatibilidad. Esto se ha realizado con el fin de minimizar el riesgo durante las actualizaciones que surgen de degradación del rendimiento debido a cambios del plan de consulta. Desde una perspectiva de aplicación, el objetivo es aún estén en el nivel de compatibilidad más reciente para heredar algunas de las nuevas características, así como mejoras de rendimiento que se realiza en el espacio del optimizador de consultas, pero hacerlo en un modo controlado. Use el nivel de compatibilidad como ayuda provisional para la migración, para solucionar diferencias de comportamiento entre las versiones que se controlan con el valor de nivel de compatibilidad correspondiente. Para obtener más información, consulte las prácticas recomendadas de actualización más adelante en el artículo.  
  
 Si existen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicaciones se ven afectadas por las diferencias de comportamiento en la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], convertir la aplicación para trabajar sin problemas con el nuevo modo de compatibilidad. A continuación, utilice **ALTER DATABASE** para cambiar el nivel de compatibilidad a 130. La nueva configuración de compatibilidad de una base de datos surte efecto cuando un **base de datos de uso** emitido o un nuevo inicio de sesión se procesa con esa base de datos como la base de datos de forma predeterminada.  
  
## <a name="best-practices"></a>Procedimientos recomendados  
Para el flujo de trabajo recomendado para actualizar el nivel de compatibilidad, vea [cambiar el modo de compatibilidad de base de datos y usar el almacén de consultas](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md).  
  
## <a name="compatibility-levels-and-stored-procedures"></a>Niveles de compatibilidad y procedimientos almacenados  
 Cuando se ejecuta un procedimiento almacenado, se utiliza el nivel de compatibilidad actual de la base de datos en la que se define. Cuando se cambia el nivel de compatibilidad de una base de datos, todos sus procedimientos almacenados se vuelven a compilar de forma automática según sea necesario.  

## <a name="differences-between-compatibility-level-130-and-level-140"></a>Diferencias entre el nivel de compatibilidad 130 y 140 de nivel  
En esta sección se describe nuevos comportamientos incluidos con nivel de compatibilidad 140.

|Configuración de nivel de compatibilidad de 130 o inferior|Configuración de nivel de compatibilidad de 140|  
|--------------------------------------------------|-----------------------------------------|  
|Estimaciones de cardinalidad para las instrucciones que hacen referencia a valores de tabla de múltiples instrucciones funciones utilizan una aproximación de fila fijo.|Estimaciones de cardinalidad para instrucciones válidas que hacen referencia a valores de tabla de múltiples instrucciones funciones usará la cardinalidad real de la salida de función.  Esta opción se habilita a través de **intercalado ejecución** para las funciones con valores de tabla de múltiples instrucciones.|
|Las consultas de modo por lotes que solicitan memoria insuficiente conceden tamaños de resultados en los volcados de disco pueden seguir teniendo problemas en las ejecuciones consecutivas.|Consultas de modo por lotes que solicitan los tamaños de concesión de memoria insuficiente que generan volcados en el disco puede tener un mejor rendimiento en las ejecuciones consecutivas.  Esta opción se habilita a través de **comentarios de concesión de memoria de modo por lotes** que actualizará el tamaño de concesión de memoria de un plan almacenado en caché si se han producido los volcados para operadores de modo por lotes. |
|Las consultas de modo por lotes que solicitan una memoria excesivo conceden tamaño que produce problemas de simultaneidad puede seguir teniendo problemas en las ejecuciones consecutivas.|Las consultas de modo por lotes que solicitan una memoria excesivo conceden tamaño que es el resultado de problemas de simultaneidad puede se ha mejorado la simultaneidad en ejecuciones consecutivas.  Esta opción se habilita a través de **comentarios de concesión de memoria de modo por lotes** que actualizará el tamaño de concesión de memoria de un plan almacenado en caché si originalmente se solicitó una cantidad excesiva.|
|Las consultas de modo por lotes que contengan operadores de combinación son aptas para tres algoritmos de combinación físicos, incluidos los bucles anidados, combinación hash y combinación de mezcla.  Si las estimaciones de cardinalidad son incorrectas para entradas de la combinación, se puede seleccionar un algoritmo de combinación inadecuado.  Si esto ocurre, se verá afectado el rendimiento y el algoritmo de combinación inapropiado permanecerán en uso hasta que se vuelve a compilar el plan almacenado en caché.|Hay un operador de combinación adicional denominado **combinación adaptable**. Si las estimaciones de cardinalidad son incorrectas para la entrada de combinación externa de compilación, se puede seleccionar un algoritmo de combinación inadecuado.  Si esto ocurre y la instrucción es apta para una combinación adaptable, un bucle anidado se utilizará para entradas de la combinación más pequeños y una combinación hash se usará para las entradas de combinación mayor dinámicamente sin necesidad de volver a compilar. |
|Triviales planes que hacen referencia a los índices de almacén de columnas no son aptos para su ejecución en modo por lotes. |Un plan trivial que hacen referencia a los índices de almacén de columnas se descartarán en favor de un plan que es apto para la ejecución en modo por lotes.|
|El operador UDX sp_execute_external_script sólo puede ejecutarse en modo de fila.|El operador UDX sp_execute_external_script es apto para la ejecución en modo por lotes.|  
|TVF de múltiples instrucciones no tiene la ejecución intercalada |Ejecución intercalada de TVF de múltiples instrucciones mejorar la calidad del plan. |

Correcciones que se encontraban bajo la marca de seguimiento 4199 en versiones anteriores de SQL Server anterior a SQL Server 2017 están habilitadas de forma predeterminada. Con el modo de compatibilidad 140. Marca de seguimiento 4199 todavía se puede aplicar de nuevo correcciones del optimizador de consultas que se publicaron con posterioridad 2017 de SQL Server. Para obtener información acerca de la marca de seguimiento 4199, consulte [marca de seguimiento 4199](https://support.microsoft.com/en-us/kb/974006).  
  
## <a name="differences-between-compatibility-level-120-and-level-130"></a>Diferencias entre el nivel de compatibilidad 120 y 130 de nivel  
Esta sección describen nuevos comportamientos incluidos con nivel de compatibilidad 130.   

  
|Configuración de nivel de compatibilidad de 120 o inferior|Configuración de nivel de compatibilidad de 130|  
|--------------------------------------------------|-----------------------------------------|  
|La instrucción Insert en una instrucción Insert select es de subproceso único.|La instrucción Insert en una instrucción Insert select es multiproceso, o puede tener un plan paralelo.|  
|Ejecutar consultas en una tabla optimizada en memoria un único subproceso.|Las consultas en una tabla con optimización para memoria ahora pueden tener planes paralelos.|  
|Introdujo el Estimador de cardinalidad de SQL 2014 **CardinalityEstimationModelVersion = "120"**|Plan de cardinalidad más mejoras de estimación (CE) con el 130 de modelo de estimación de cardinalidad que es visible desde una consulta. **CardinalityEstimationModelVersion = "130"**|  
|Modo por lotes frente a cambios de modo de fila con los índices de almacén de columnas<br /><br /> Ordena en una tabla con índice de almacén de columnas está en modo de fila<br /><br /> Agregados de la función de ventana funcionan en el modo de fila como LAG o clientes potenciales<br /><br /> Consultas en tablas de almacén de columnas con varias cláusulas distinct operadas en modo de fila<br /><br /> Consultas que se ejecuten con MAXDOP 1 o un plan serie que se ejecuta en modo de fila | Modo por lotes frente a cambios de modo de fila con los índices de almacén de columnas<br /><br /> Ordena en una tabla con un índice de almacén de columnas se encuentran ahora en modo por lotes<br /><br /> Agregados de ventana funcionan ahora en modo por lotes como LAG o clientes potenciales<br /><br /> Las consultas en las tablas de almacén de columnas con varias cláusulas distinct funcionan en modo por lotes<br /><br /> Las consultas que se ejecuten con Maxdop1 o un plan en serie se ejecuten en modo por lotes|  
| Las estadísticas se pueden actualizar automáticamente. | La lógica que actualiza automáticamente las estadísticas es más agresiva en tablas grandes.  En la práctica, esto debería reducir donde los clientes han visto los problemas de rendimiento en las consultas donde las filas recién insertadas se consultan con frecuencia pero que las estadísticas no se hubiera actualizado para incluir los valores de los casos. |  
| Seguimiento 2371 es OFF de forma predeterminada en [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. | [Seguimiento 2371](https://blogs.msdn.microsoft.com/psssql/2016/10/04/default-auto-statistics-update-threshold-change-for-sql-server-2016/) está activado de forma predeterminada en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Marca de seguimiento 2371 indica el actualizador de estadísticas automática a un subconjunto más pequeño aún mejor de filas en una tabla que tiene un gran número de filas de ejemplo. <br/> <br/> Una mejora consiste en incluir en el ejemplo más filas que se insertaron recientemente. <br/> <br/> Otra mejora es permitir que las consultas se ejecutan mientras el proceso de actualización de estadísticas se ejecuta, en lugar de bloqueo de la consulta. |  
| Para el nivel 120, las estadísticas se muestrean mediante un *único*-un subproceso de proceso. | Nivel de 130, las estadísticas se muestrean mediante un *múltiples*-un subproceso de proceso. |  
| 253 claves externas entrantes es el límite. | Puede hacer referencia a una tabla determinada hasta 10 000 claves externas entrantes o referencias similar. Para ver las restricciones, vea [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md). |  
|Se permiten los algoritmos de hash MD2, MD4, MD5, SHA y SHA1 en desuso.|Se permiten los algoritmos de hash solo SHA2_256 y SHA2_512.|  
  
  
Marca de correcciones que se encontraban bajo seguimiento 4199 en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] están habilitados de forma predeterminada. Con el modo de compatibilidad 130. Marca de seguimiento 4199 seguirán aplicable para nuevas correcciones del optimizador de consultas que se publicaron con posterioridad [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Para utilizar el optimizador de consultas anterior en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] debe seleccionar el nivel de compatibilidad 110. Para obtener información acerca de la marca de seguimiento 4199, consulte [marca de seguimiento 4199](https://support.microsoft.com/en-us/kb/974006).  
  
## <a name="differences-between-lower-compatibility-levels-and-level-120"></a>Diferencias entre los niveles de compatibilidad inferiores y el nivel 120  
 En esta sección se describen nuevos comportamientos incluidos con el nivel de compatibilidad 120.  
  
|Nivel de compatibilidad 110 o inferior|Nivel de compatibilidad 120|  
|--------------------------------------------------|-----------------------------------------|  
|Se utiliza el optimizador de consultas más antiguo.|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] incluye mejoras sustanciales en el componente que crea y en los planes de consulta optimizados. Esta nueva característica del optimizador de consultas depende del uso del nivel 120 de compatibilidad de base de datos. Para aprovecharse estas mejoras, las nuevas aplicaciones de base de datos deben desarrollarse con el nivel 120 de compatibilidad de base de datos. Las aplicaciones migradas de versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben probarse cuidadosamente para confirmar que el buen rendimiento se ha mantenido o se ha mejorado. Si el rendimiento se degrada, puede establecer la compatibilidad de base de datos en el nivel 110 o inferior para usar la anterior metodología del optimizador de consultas.<br /><br /> El nivel de compatibilidad de la base de datos 120 usa un nuevo estimador de cardinalidad que está optimizado para cargas de trabajo modernas de almacenamiento de datos y OLTP. Antes de establecer el nivel de compatibilidad de base de datos en 110 debido a problemas de rendimiento, vea las recomendaciones incluidas en la sección planes de consulta de la [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [What's New en el motor de base de datos](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md) tema.|  
|En los niveles de compatibilidad inferiores a 120, se omite la configuración de idioma al convertir un **fecha** valor con un valor de cadena. Tenga en cuenta que este comportamiento es específico solamente el **fecha** tipo. Vea el ejemplo B en la sección ejemplos siguiente.|La configuración de idioma no se omite al convertir un **fecha** valor con un valor de cadena.|  
|Las referencias recursivas en el lado derecho de una cláusula EXCEPT crean un bucle infinito. Ejemplo C en la sección ejemplos siguiente demuestra este comportamiento.|Las referencias recursivas en una cláusula EXCEPT generan un error de acuerdo con el estándar ANSI SQL.|  
|CTE recursiva admite nombres de columna duplicados.|CTE recursiva no admite nombres de columna duplicados.|  
|Los desencadenadores deshabilitados se habilitan si se modifican los desencadenadores.|Modificar un desencadenador no cambia el estado (habilitado o deshabilitado) del mismo.|  
|La cláusula de la tabla OUTPUT INTO omite IDENTITY_INSERT SETTING = OFF y permite que se inserten los valores explícitos.|No puede insertar valores explícitos para una columna de identidad en una tabla cuando IDENTITY_INSERT es OFF.|  
|Cuando la contención de la base de datos está establecida en parcial, al validar el campo $action en la cláusula OUTPUT de una instrucción MERGE puede devolverse un error de intercalación.|La intercalación de los valores devueltos por la cláusula $action de una instrucción MERGE es la intercalación de base de datos en lugar de la intercalación de servidor y no se devuelve un error de conflicto de intercalación.|  
|A **SELECT INTO** instrucción siempre crea una operación de inserción de un único subproceso.|A **SELECT INTO** instrucción puede crear una operación de inserción en paralelo. Al insertar un gran número de filas, la operación paralela puede mejorar el rendimiento.|  
  
## <a name="differences-between-lower-compatibility-levels-and-levels-110-and-120"></a>Diferencias entre los niveles de compatibilidad inferiores y los niveles 110 y 120  
 En esta sección se describen nuevos comportamientos incluidos con nivel de compatibilidad 110.   Esta sección también se aplica al nivel 120.  
  
|Nivel de compatibilidad 100 o inferior|Configuración de nivel de compatibilidad de al menos 110|  
|--------------------------------------------------|--------------------------------------------------|  
|Los objetos de base de datos de Common Language Runtime (CLR) se ejecutan con la versión 4 de CLR. Sin embargo, algunos cambios de comportamiento incluidos en la versión 4 de CLR se evitan. Para obtener más información, consulte [What's New en integración CLR](../../relational-databases/clr-integration/clr-integration-what-s-new.md).|Los objetos de base de datos de CLR se ejecutan con la versión 4 de CLR.|  
|Las funciones de XQuery **longitud de la cadena** y **subcadena** cuentan cada suplente como dos caracteres.|Las funciones de XQuery **longitud de la cadena** y **subcadena** cuentan cada suplente como un solo carácter.|  
|PIVOT se permite en una consulta de expresión de tabla común (CTE) recursiva. Sin embargo, la consulta devuelve resultados incorrectos cuando hay varias filas por agrupación.|PIVOT no se permite en una consulta de expresión de tabla común (CTE) recursiva. Se devuelve un error.|  
|El algoritmo RC4 se admite únicamente por razones de compatibilidad con versiones anteriores. El material nuevo solo se puede cifrar con RC4 o RC4_128 cuando la base de datos tenga el nivel de compatibilidad 90 o 100. (No se recomienda). En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], el material cifrado con RC4 o RC4_128 se puede descifrar en cualquier nivel de compatibilidad.|El nuevo material no se puede cifrar mediante RC4 o RC4_128. Use un algoritmo más reciente como uno de los algoritmos AES en su lugar. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], el material cifrado con RC4 o RC4_128 se puede descifrar en cualquier nivel de compatibilidad.|  
|El estilo predeterminado para las operaciones CAST y CONVERT en **tiempo** y **datetime2** tipos de datos es 121, a menos que se utilizan cualquiera de estos tipos en una expresión de columna calculada. Para las columnas calculadas, el estilo predeterminado es 0. Este comportamiento afecta a las columnas calculadas cuando se crean, cuando se utilizan en las consultas que implican parametrización automática o cuando se usan en definiciones de restricciones.<br /><br /> Ejemplo D en la siguiente sección de ejemplos muestra la diferencia entre los estilos 0 y 121. No se muestra el comportamiento descrito anteriormente. Para obtener más información sobre los estilos de fecha y hora, vea [CAST y CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).|Habilita la compatibilidad con el nivel 110, el estilo predeterminado para las operaciones CAST y CONVERT en **tiempo** y **datetime2** tipos de datos es siempre 121. Si su consulta se basa en el comportamiento anterior, use un nivel de compatibilidad menor de 110, o especifique explícitamente el estilo 0 en la consulta correspondiente.<br /><br /> Actualizar la base de datos al nivel de compatibilidad 110 no cambiará los datos de usuario que se hayan almacenado en disco. Debe corregir manualmente estos datos según convenga. Por ejemplo, si utilizara SELECT INTO para crear una tabla de un origen que contuviera una expresión de columna calculada como la descrita anteriormente, se almacenarían los datos (si se usa el estilo 0) en lugar de la propia definición de columna calculada. Debería actualizar manualmente estos datos para que coincidieran con el estilo 121.|  
|Las columnas de tablas remotas de tipo **smalldatetime** que se hace referencia en una vista con particiones se asignan como **datetime**. Las columnas correspondientes de las tablas locales (en la misma posición ordinal en la lista de selección) deben ser de tipo **datetime**.|Las columnas de tablas remotas de tipo **smalldatetime** que se hace referencia en una vista con particiones se asignan como **smalldatetime**. Las columnas correspondientes de las tablas locales (en la misma posición ordinal en la lista de selección) deben ser de tipo **smalldatetime**.<br /><br /> Después de actualizar a 110, la vista distribuida con particiones producirá un error debido a una discrepancia en los tipos de datos. Puede resolver este problema, cambie el tipo de datos en la tabla remota para **datetime** o establecer la compatibilidad de nivel de la base de datos local en 100 o inferior.|  
|La función SOUNDEX implementa las reglas siguientes:<br /><br /> (1)-mayúsculas H o W mayúsculas se omiten al separar dos consonantes que tienen el mismo número en el código SOUNDEX.<br /><br /> 2) si los 2 primeros caracteres de *character_expression* tienen el mismo número en el código SOUNDEX, ambos caracteres se incluyen. Si un conjunto de consonantes en paralelo tiene el mismo número del código de SOUNDEX, se excluyen todas excepto la primera.|La función SOUNDEX implementa las reglas siguientes:<br /><br /> (1) si mayúscula H o W mayúsculas separan dos consonantes que tienen el mismo número en el código SOUNDEX, codifica la consonante situada a la derecha se omite<br /><br /> (2) si un conjunto de consonantes side-by-side tiene el mismo número en el código SOUNDEX, todas ellas se excluyen excepto el primero.<br /><br /> <br /><br /> Las reglas adicionales pueden causar que los valores calculados por la función SOUNDEX sean diferentes de los calculados en niveles de compatibilidad menores. Después de actualizar al nivel de compatibilidad 110, es posible que tenga que regenerar los índices, los montones o las restricciones CHECK que usan la función SOUNDEX. Para obtener más información, vea [SOUNDEX &#40; Transact-SQL &#41;](../../t-sql/functions/soundex-transact-sql.md)|  
  
## <a name="differences-between-compatibility-level-90-and-level-100"></a>Diferencias entre los niveles de compatibilidad 90 y 100  
 En esta sección se describen nuevos comportamientos incluidos con nivel de compatibilidad 100.  
  
|Nivel de compatibilidad 90|Nivel de compatibilidad 100|Posibilidad de impacto|  
|----------------------------------------|-----------------------------------------|---------------------------|  
|El valor QUOTED_IDENTIFER siempre está establecido en ON para las funciones con valores de tabla con múltiples instrucciones cuando se crean sin tener en cuenta el valor de nivel de sesión.|El valor de sesión de QUOTED IDENTIFIER se cumple cuando se crean funciones con valores de tabla con múltiples instrucciones.|Media|  
|Al crear o modificar una función de partición, **datetime** y **smalldatetime** literales en la función se evalúan suponiendo que US_English es la configuración de idioma.|La configuración de idioma actual se utiliza para evaluar **datetime** y **smalldatetime** literales en la función de partición.|Media|  
|La cláusula FOR BROWSE se permite (y se omite) en las instrucciones SELECT INTO e INSERT.|La cláusula FOR BROWSE no se permite en las instrucciones SELECT INTO e INSERT.|Media|  
|Los predicados de texto completo se permiten en la cláusula OUTPUT.|Los predicados de texto completo no se permiten en la cláusula OUTPUT.|Baja|  
|No se admiten CREATE FULLTEXT STOPLIST, ALTER FULLTEXT STOPLIST o DROP FULLTEXT STOPLIST. La lista de palabras irrelevantes del sistema se asocia automáticamente a nuevos índices de texto completo.|Se admiten CREATE FULLTEXT STOPLIST, ALTER FULLTEXT STOPLIST o DROP FULLTEXT STOPLIST.|Baja|  
|MERGE no se aplica como una palabra clave reservada.|MERGE es una palabra clave totalmente reservada. La instrucción MERGE se admite por debajo de los niveles de compatibilidad 100 y 90.|Baja|  
|Mediante el \<dml_table_source > argumento de la instrucción INSERT genera un error de sintaxis.|Puede capturar los resultados de una cláusula OUTPUT en una instrucción anidada INSERT, UPDATE, DELETE o MERGE, e insertar los resultados obtenidos en una vista o tabla de destino. Esto se realiza mediante el \<dml_table_source > argumento de la instrucción INSERT.|Baja|
|A menos que se especifique NOINDEX, DBCC CHECKDB o DBCC CHECKTABLE realizan comprobaciones de coherencia física y lógica en una sola tabla o vista indexada, y en todos sus índices XML y no clúster. Los índices espaciales no se admiten.|A menos que se especifique NOINDEX, DBCC CHECKDB o DBCC CHECKTABLE realizan comprobaciones de coherencia física y lógica en una sola tabla, y en todos sus índices no clúster. Sin embargo, en los índices XML, índices espaciales y vistas indexadas solamente se realizan comprobaciones de coherencia física de forma predeterminada.<br /><br /> Si se especifica WITH EXTENDED_LOGICAL_CHECKS, se realizan comprobaciones lógicas en las vistas indexadas, índices XML e índices espaciales, si los hay. De forma predeterminada, las comprobaciones de coherencia física se realizan antes que las comprobaciones de coherencia lógica. Si también se especifica NOINDEX, solamente se realizarán las comprobaciones lógicas.|Baja|  
|Cuando una cláusula OUTPUT se utiliza con una instrucción del lenguaje de manipulación de datos (DML) y se produce un error en tiempo de ejecución durante la ejecución de la instrucción, toda la transacción se termina y se revierte.|Cuando una cláusula OUTPUT se utiliza con una instrucción del lenguaje de manipulación de datos (DML) y ocurre un error en tiempo de ejecución durante la ejecución de la instrucción, el comportamiento depende del valor de SET XACT_ABORT. Si SET XACT_ABORT es OFF, un error de anulación de la instrucción generado por la instrucción DML que usa la cláusula OUTPUT terminará la instrucción, pero la ejecución del lote continúa y la transacción no se revierte. Si SET XACT_ABORT es ON, todos los errores en tiempo de ejecución generados por la instrucción DML que usa la cláusula OUTPUT terminarán el lote y la transacción se revertirá.|Baja|  
|CUBE y ROLLUP no se exigen como palabras clave reservadas.|CUBE y ROLLUP son palabras clave reservadas dentro de la cláusula GROUP BY.|Baja|  
|Validación estricta se aplica a los elementos de XML **anyType** tipo.|Validación lax se aplica a los elementos de la **anyType** tipo. Para obtener más información, consulte [componentes comodín y validación de contenido](../../relational-databases/xml/wildcard-components-and-content-validation.md).|Baja|  
|Los atributos especiales **xsi: nil** y **xsi: Type** no se pueden consultar ni modificar mediante instrucciones de lenguaje de manipulación de datos.<br /><br /> Esto significa que `/e/@xsi:nil` genera un error mientras `/e/@*` pasa por alto el **xsi: nil** y **xsi: Type** atributos. Sin embargo, `/e` devuelve el **xsi: nil** y **xsi: Type** atributos para mantener la coherencia con `SELECT xmlCol`, incluso si `xsi:nil = "false"`.|Los atributos especiales **xsi: nil** y **xsi: Type** se almacenan como atributos normales y se puede consultar y modificar.<br /><br /> Por ejemplo, al ejecutar la consulta `SELECT x.query('a/b/@*')` devuelve todos los atributos incluidos **xsi: nil** y **xsi: Type**. Para excluir estos tipos en la consulta, reemplace `@*` con `@*[namespace-uri(.) != "` *insertar uri de espacio de nombres xsi* `"` y no `(local-name(.) = "type"` o`local-name(.) ="nil".`|Baja|  
|Una función definida por el usuario que convierta un valor de cadena constante XML en un tipo datetime de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se marca como determinista.|Una función definida por el usuario que convierta un valor de cadena constante XML a un tipo datetime de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se marca como no determinista.|Baja|  
|Los tipos de lista y unión de XML no se admiten por completo.|Los tipos de lista y unión que se admiten totalmente incluyen la funcionalidad siguiente:<br /><br /> Unión de lista<br /><br /> Unión de unión<br /><br /> Lista de tipos atómicos<br /><br /> Lista de unión|Baja|  
|Las opciones de SET requeridas para un método de XQuery no se validan cuando el método está contenido en una vista o función con valores de tabla insertados.|Las opciones de SET requeridas para un método de XQuery se validan cuando el método está contenido en una vista o función con valores de tabla insertados. Se produce un error si las opciones de SET del método se establecen incorrectamente.|Baja|  
|Los valores de los atributos XML que contienen caracteres de fin de línea (retorno de carro y avance de línea) no se normalizan según el estándar XML. Es decir, ambos caracteres se devuelven en lugar de un único carácter de avance de línea.|Los valores de los atributos XML que contienen caracteres de fin de línea (retorno de carro y avance de línea) se normalizan de acuerdo con el estándar XML. Es decir, todos los saltos de línea de las entidades externas analizadas (incluidas las de documento) se normalizan en la entrada traduciendo la secuencia de dos caracteres #xD #xA y cualquier #xD al que no siga #xA por un solo carácter #xA.<br /><br /> Las aplicaciones que utilizan atributos para transportar los valores de cadena que contienen caracteres de fin de línea no recibirán de vuelta estos caracteres a medida que se envíen. Para evitar el proceso de normalización, utilice entidades de caracteres numéricos XML para codificar todos los caracteres de fin de línea.|Baja|  
|Las propiedades de columna ROWGUIDCOL e IDENTITY se pueden denominar incorrectamente como una restricción. Por ejemplo, la instrucción `CREATE TABLE T (C1 int CONSTRAINT MyConstraint IDENTITY)` se ejecuta, pero el nombre de restricción no se conserva y no es accesible para el usuario.|Las propiedades de columna ROWGUIDCOL e IDENTITY no se pueden denominar como una restricción. Se devuelve el error 156.|Baja|  
|Al actualizar las columnas utilizando una asignación bidireccional como `UPDATE T1 SET @v = column_name = <expression>`, se pueden generar resultados inesperados porque durante la ejecución de la instrucción se puede utilizar el valor real de la variable en otras cláusulas como WHERE y ON en lugar del valor inicial de la instrucción. Esto puede hacer que los significados de los predicados cambien de forma imprevisible según cada fila.<br /><br /> Este comportamiento solo es aplicable cuando el nivel de compatibilidad está establecido en 90.|Al actualizar las columnas utilizando una asignación bidireccional, se generan los resultados previstos porque solo se obtiene acceso al valor inicial de la columna de la instrucción durante la ejecución de la misma.|Baja|  
|Vea el ejemplo E en la siguiente sección de ejemplos.|Vea el ejemplo F en la siguiente sección de ejemplos.|Baja|  
|La función ODBC {fn CONVERT()} utiliza el formato de fecha predeterminado del lenguaje. En algunos lenguajes, el formato predeterminado es ADM, lo que puede producir errores de conversión cuando CONVERT() se combina con otras funciones, como {fn CURDATE()}, que espera un formato AMD.|La función ODBC {fn CONVERT()} utiliza el estilo 121 (un formato AMD independiente del lenguaje) al convertir a los tipos de datos ODBC SQL_TIMESTAMP, SQL_DATE, SQL_TIME, SQLDATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP.|Baja|  
|Los tipos de fecha y hora intrínsecos como DATEPART no requieren que los valores de entrada de cadena sean literales de fecha y hora válidos. Por ejemplo, SELECT DATEPART (year, 2007/05-30') se compila correctamente.|Los tipos de fecha intrínsecos y hora como DATEPART requieren que los valores de entrada de cadena sean literales de fecha y hora válidos. Se devuelve el error 241 cuando se utiliza un literal de fecha y hora no válido.|Baja|  
  
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
  
 Si una aplicación utiliza un identificador que está reservado como palabra clave para su nivel de compatibilidad, la aplicación generará un error. Para resolver este problema, incluya el identificador entre ambos corchetes (**[]**) o comillas (**""**); por ejemplo, para actualizar una aplicación que utiliza el identificador **externo** al nivel de compatibilidad 90, puede cambiar el identificador como **[EXTERNAL]** o **"Externo"**.  
  
 Para obtener más información, vea [Palabras clave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-compatibility-level"></a>A. Cambiar el nivel de compatibilidad  
 En el ejemplo siguiente se cambia el nivel de compatibilidad de la [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] a la base de datos `110,` [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
```tsql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 110;  
GO  
```  
  
 El ejemplo siguiente devuelve el nivel de compatibilidad de la base de datos actual.  
  
```tsql  
SELECT name, compatibility_level   
FROM sys.databases   
WHERE name = db_name();  
```  
  
### <a name="b-ignoring--the-set-language-statement-except-under-compatibility-level-120"></a>B. Se omitirá la instrucción SET LANGUAGE excepto en el nivel de compatibilidad 120  
 La siguiente consulta omite la instrucción SET LANGUAGE excepto en el nivel de compatibilidad 120.  
  
```tsql  
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
 Para la configuración de nivel de compatibilidad de 110 o inferior, las referencias recursivas en el lado derecho de una cláusula EXCEPT crean un bucle infinito.  
  
```tsql  
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
 Este ejemplo muestra la diferencia entre los estilos 0 y 121. Para obtener más información sobre los estilos de fecha y hora, vea [CAST y CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
```tsql  
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
  
```tsql  
ALTER DATABASE AdventureWorks2012  
SET compatibility_level = 90;  
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
  
```tsql  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM   
    (SELECT BusinessEntityID FROM HumanResources.Employee  
     UNION ALL  
     SELECT BusinessEntityID FROM HumanResources.EmployeeAddress) AS Test;  
SELECT @v;  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Palabras clave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
 [Ver o cambiar el nivel de compatibilidad de una base de datos](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) 
  
