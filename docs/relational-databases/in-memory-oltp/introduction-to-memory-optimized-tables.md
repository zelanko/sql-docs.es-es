---
title: Introducción a las tablas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 12/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ef1cc7de-63be-4fa3-a622-6d93b440e3ac
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9fe7d83331ee1dc0824e77602c60be04e070fb6f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68050203"
---
# <a name="introduction-to-memory-optimized-tables"></a>Introducción a las tablas con optimización para memoria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Las tablas optimizadas para memoria se crean con [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 De forma predeterminada, las tablas optimizadas para memoria son totalmente durables y, al igual que las transacciones en tablas basadas en disco (tradicionales), las transacciones en este tipo de tablas tienen todas las propiedades ACID (atomicidad, coherencia, aislamiento y durabilidad). Las tablas optimizadas para memoria y los procedimientos almacenados compilados de forma nativa admiten solo un subconjunto de características de [!INCLUDE[tsql](../../includes/tsql-md.md)].
 
A partir de SQL Server 2016, y en Azure SQL Database, no existen limitaciones para [intercalaciones o páginas de códigos](../../relational-databases/collations/collation-and-unicode-support.md) que son específicas de OLTP en memoria.
  
 El almacenamiento principal para las tablas optimizadas para memoria es la memoria principal. Las filas de la tabla se leen y se escriben en la memoria. Una segunda copia de los datos de la tabla se conserva en el disco pero solo por la durabilidad. Vea [Crear y administrar el almacenamiento de objetos con optimización para memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md) para obtener más información sobre las tablas durables. Los datos de las tablas optimizadas para memoria solo se leen del disco durante la recuperación de la base de datos (por ejemplo, después de reiniciar el servidor).  
  
 Para conseguir incluso mayores mejoras de rendimiento, OLTP en memoria admite tablas durables con la durabilidad diferida de las transacciones. Las transacciones durables diferidas se guardan en el disco en cuanto la transacción se ha confirmado y se devuelve el control al cliente. A cambio de un mayor rendimiento, las transacciones confirmadas que no se hayan guardado en el disco se pierden si el servidor se bloquea o conmuta por error.  
  
 Además de las tablas optimizadas para memoria durables predeterminadas, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también admite tablas optimizadas para memoria no durables, que no se registran y cuyos datos no se guardan en el disco. Esto significa que las transacciones en estas tablas no requieren ninguna E/S de disco, pero los datos no se recuperarán si hay un bloqueo o una conmutación por error del servidor.  
  
 OLTP en memoria está integrado con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para proporcionar una experiencia satisfactoria en todas las áreas como el desarrollo, la implementación, la facilidad de uso y la compatibilidad. Una base de datos puede contener objetos en memoria y objetos basados en disco.  
  
 Las tablas optimizadas para memoria son siempre con control de versiones. Esto significa que cada fila de la tabla puede tener varias versiones. Todas las versiones de fila se mantienen en la misma estructura de datos de la tabla. El control de versiones de fila se utiliza para permitir las lecturas y las escrituras simultáneas en la misma fila. Para obtener más información sobre las lecturas y las escrituras simultáneas en la misma fila, vea [Transactions with Memory-Optimized Tables](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)(Transacciones con tablas con optimización para memoria).  
  
 La siguiente ilustración muestra la multiversión. La ilustración muestra una tabla con tres filas y cada fila tiene versiones diferentes.  
  
![Multiversión.](../../relational-databases/in-memory-oltp/media/hekaton-tables-1.gif "Multiversión.")  
  
 La tabla tiene tres filas: r1, r2 y r3. r1 tiene tres versiones, r2 tiene dos versiones y r3 tiene cuatro. Observe que las diferentes versiones de la misma fila no ocupan necesariamente ubicaciones de memoria consecutivas. Las diferentes versiones de fila pueden estar dispersas por la estructura de datos de la tabla.  
  
 La estructura de datos de una tabla optimizada para memoria se puede considerar como una colección de versiones de fila. Las filas de tablas basadas en disco se organizan en páginas y extensiones, las filas individuales se direccionan con el desplazamiento de página y número de página, y las versiones de fila de las tablas optimizadas para memoria se direccionan con punteros de memoria de 8 bytes.  
  
 Se puede tener acceso a los datos de las tablas optimizadas para memoria de dos maneras:  
  
-   A través de procedimientos almacenados compilados de forma nativa.  
  
-   Con [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado, fuera de un procedimiento almacenado compilado de forma nativa. Estas instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] pueden ser procedimientos almacenados interpretados internamente o pueden ser instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc.  
  
## <a name="accessing-data-in-memory-optimized-tables"></a>Acceso a datos en tablas con optimización para memoria  

Se puede tener acceso a las tablas con optimización para memoria de forma más eficaz desde procedimientos almacenados compilados de forma nativa ([Procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)). Se puede tener acceso también a las tablas con optimización para memoria con [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado (tradicional). [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado hace referencia al acceso a tablas optimizadas para memoria sin un procedimiento almacenado compilado de forma nativa. Algunos ejemplos de acceso con [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado son el acceso a una tabla optimizada para memoria desde un desencadenador DML, un lote ad hoc de [!INCLUDE[tsql](../../includes/tsql-md.md)] , una vista y una función con valores de tabla.  
  
 En la tabla siguiente se resume el acceso con [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado y nativo para varios objetos.  
  
|Característica|Acceso con un procedimiento almacenado compilado de forma nativa|Acceso con [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado|Acceso CLR|  
|-------------|-------------------------------------------------------|-------------------------------------------|----------------|  
|Tabla con optimización para memoria|Sí|Sí|No*|  
|Tipo de tabla con optimización para memoria|Sí|Sí|No|  
|Procedimiento almacenado compilado de forma nativa|Ahora se admite el anidamiento de procedimientos almacenados compilados de forma nativa. Puede usar la sintaxis EXECUTE dentro de los procedimientos almacenados, siempre que el procedimiento de referencia también se compile de forma nativa.|Sí|No*|  
  
 *No puede tener acceso a una tabla optimizada para memoria o a un procedimiento almacenado compilado de forma nativa desde la conexión de contexto (la conexión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al ejecutar un módulo CLR). Sin embargo, puede crear y abrir otra conexión en la que pueda tener acceso a las tablas optimizadas para memoria y a los procedimientos almacenados compilados de forma nativa.  
  
## <a name="performance-and-scalability"></a>Escalabilidad y rendimiento  

Los siguientes factores afectarán a las mejoras del rendimiento que se pueden lograr con OLTP en memoria:  
  
*Comunicación:* Una aplicación que realiza muchas llamadas a procedimientos almacenados cortos puede suponer un aumento del rendimiento menor en comparación con una aplicación que realiza menos llamadas e implementa más funcionalidad en cada procedimiento almacenado.  
  
*Ejecución de [!INCLUDE[tsql](../../includes/tsql-md.md)]:* OLTP en memoria alcanza el máximo rendimiento cuando se usan procedimientos almacenados compilados de forma nativa en lugar de procedimientos almacenados interpretados o de ejecución de consultas. Puede haber un beneficio para obtener acceso a las tablas optimizadas para memoria desde este tipo de procedimientos almacenados.  
  
*Examen de intervalo y búsqueda de puntos:* Los índices no clúster con optimización para memoria admiten los exámenes de intervalo y los exámenes ordenados. Para las búsquedas de puntos, los índices hash optimizados para memoria tienen mejor rendimiento que los índices no clúster optimizados para memoria. Los índices no clúster con optimización para memoria tienen mejor rendimiento que los índices basados en disco.

- A partir de SQL Server 2016, el plan de consulta para una tabla optimizada para memoria puede examinar la tabla en paralelo. Esto mejora el rendimiento de las consultas de análisis.
  - Los índices de hash también han pasado a poder examinarse en paralelo en SQL Server 2016.
  - Los índices no agrupados también han pasado a poder examinarse en paralelo en SQL Server 2016.
  - Los índices de almacén de columnas se han podido examinar en paralelo desde el principio, en SQL Server 2014.
  
*Operaciones de índice:* las operaciones de índice no se registran y solo existen en memoria.  
  
*Simultaneidad:* Las aplicaciones cuyo rendimiento se ve afectado por la simultaneidad del nivel de motor, como la contención de bloqueos temporales o el bloqueo, mejoran significativamente cuando se pasan a OLTP en memoria.  
  
En la tabla siguiente se enumeran los problemas de rendimiento y escalabilidad que se suelen encontrar en las bases de datos relacionales y el modo en que OLTP en memoria puede mejorar el rendimiento.  
  
|Problema|Impacto de OLTP en memoria|  
|-----------|----------------------------|  
|Rendimiento<br /><br /> Uso elevado de los recursos (CPU, E/S, red o memoria).|CPU<br /> Los procedimientos almacenados compilados de forma nativa pueden reducir el uso de la CPU de forma significativa porque requieren muchas menos instrucciones para ejecutar una instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] si se compara con los procedimientos almacenados interpretados.<br /><br /> OLTP en memoria puede ayudar a reducir la inversión en hardware en las cargas de trabajo con escalado horizontal, ya que un servidor podría ofrecer el rendimiento de entre cinco y diez servidores.<br /><br /> E/S<br /> Si encuentra un cuello de botella de E/S desde el procesamiento hasta las páginas de datos o de índices, OLTP en memoria puede reducir el cuello de botella. Además, la comprobación de los objetos de OLTP en memoria es continua y no produce incrementos súbitos de las operaciones de E/S. Sin embargo, si el espacio de trabajo de las tablas de rendimiento crítico no cabe en la memoria, OLTP en memoria no mejorará el rendimiento porque requiere que los datos residan en la memoria. Si encuentra un cuello de botella de E/S en el registro, OLTP en memoria puede reducirlo porque realiza menos tareas de registro. Si una o más tablas optimizadas para memoria se configuran como tablas no durables, puede eliminar el registro de los datos.<br /><br /> Memoria<br /> OLTP en memoria no proporciona ninguna ventaja de rendimiento. OLTP en memoria puede suponer una presión adicional sobre la memoria, ya que los objetos deben residir en la memoria.<br /><br /> Red<br /> OLTP en memoria no proporciona ninguna ventaja de rendimiento. Los datos tienen que comunicarse desde la capa de datos en el nivel de aplicación.|  
|Escalabilidad<br /><br /> La mayoría de los problemas de escala de las aplicaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son causados por problemas de simultaneidad como la contención de bloqueos, bloqueos temporales y bloqueos por subproceso.|Contención de bloqueos temporales<br /> Un escenario típico es la contención en la última página de un índice al insertar filas simultáneamente en el orden de clave. Dado que OLTP en memoria no adopta bloqueos temporales para tener acceso a los datos, los problemas de escalabilidad relacionados con las contenciones de bloqueos temporales desaparecen por completo.<br /><br /> Contención de bloqueo por subproceso<br /> Dado que OLTP en memoria no adopta bloqueos temporales para tener acceso a los datos, los problemas de escalabilidad relacionados con las contenciones de bloqueos por subproceso desaparecen por completo.<br /><br /> Contención relacionada con el bloqueo<br /> Si la aplicación de base de datos encuentra problemas de bloqueo entre las operaciones de lectura y escritura, OLTP en memoria evita dichos problemas porque usa un nuevo formato de control de simultaneidad optimista para implementar todos los niveles de aislamiento de las transacciones. OLTP en memoria no usa TempDB para almacenar las versiones de fila.<br /><br /> Si el problema de escala se debe al conflicto entre dos operaciones de escritura, como dos transacciones simultáneas que intenten actualizar la misma fila, OLTP en memoria permite que una transacción sea correcta y que la otra dé error. La transacción errónea debe volver a enviarse ya sea de forma explícita o implícita, volviendo a intentar la transacción. En cualquier caso, debe realizar cambios en la aplicación.<br /><br /> Si la aplicación experimenta conflictos frecuentes entre dos operaciones de escritura, el valor de bloqueo optimista se reduce. La aplicación no es adecuada para OLTP en memoria. La mayoría de las aplicaciones OLTP no tienen conflictos de escritura a menos que el conflicto sea inducido por la extensión de bloqueo.|  
  
##  <a name="rls"></a> Seguridad de nivel de fila en tablas con optimización para memoria  

La[seguridad de nivel de fila](../../relational-databases/security/row-level-security.md) es compatible con las tablas optimizadas para memoria. La aplicación de directivas de seguridad de nivel de fila a las tablas optimizadas para memoria es esencialmente igual que para las tablas basadas en disco, con la excepción de que las funciones con valores de tabla en línea que se usan como predicados seguros deben compilarse de manera nativa (se deben crear con la opción WITH NATIVE_COMPILATION). Para obtener más información, vea la sección [Compatibilidad entre características](../../relational-databases/security/row-level-security.md#Limitations) del tema [Seguridad de nivel de fila](../../relational-databases/security/row-level-security.md) .  
  
 Diversas funciones de seguridad integradas esenciales para la seguridad de nivel de fila se habilitaron para las tablas en memoria. Para obtener más información, vea [Funciones integradas en módulos compilados de forma nativa](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#bfncsp).  
  
 **EXECUTE AS CALLER:** todos los módulos nativos ahora admiten y usan EXECUTE AS CALLER de manera predeterminada, aunque no se especifique la sugerencia. Esto se debe a que se espera que todas las funciones de predicado de seguridad de nivel de fila usen EXECUTE AS CALLER, para que la función (y cualquier función integrada que se use dentro de ella) se evalúe en el contexto del usuario que realiza la llamada.   
EXECUTE AS CALLER tiene una pequeña merma en el rendimiento (de aproximadamente 10 %) provocada por las comprobaciones de permisos en el autor de la llamada. Si el módulo especifica EXECUTE AS OWNER o EXECUTE AS SELF de manera explícita, se evitarán estas comprobaciones de permisos y su costo de rendimiento asociado. Sin embargo, si usa cualquiera de estas opciones junto con las funciones integradas mencionadas anteriormente, se producirá una merma de rendimiento considerablemente mayor debido al cambio de contexto necesario.  
  
## <a name="scenarios"></a>Escenarios

Para obtener una breve descripción de los escenarios habituales en los que [!INCLUDE[hek_1](../../includes/hek-1-md.md)] puede mejorar el rendimiento, vea [OLTP en memoria](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte también

[OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
