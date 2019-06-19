---
title: Introducción a las tablas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ef1cc7de-63be-4fa3-a622-6d93b440e3ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff434efd0a9f4fcb3316143e598e636bff85f487
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157831"
---
# <a name="introduction-to-memory-optimized-tables"></a>Introducción a las tablas con optimización para memoria
  Las tablas con optimización para memoria son tablas creadas por medio de [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).  
  
 Las tablas con optimización para memoria residen en la memoria. Las filas de la tabla se leen y se escriben en la memoria. Toda la tabla reside en memoria. Una segunda copia de los datos de la tabla se conserva en el disco pero solo por la durabilidad.  
  
 OLTP en memoria está integrado con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para proporcionar una experiencia satisfactoria en todas las áreas como el desarrollo, la implementación, la facilidad de uso y la compatibilidad. Una base de datos puede contener objetos en memoria y objetos basados en disco.  
  
 Las tablas optimizadas para memoria son siempre con control de versiones. Esto significa que cada fila de la tabla puede tener varias versiones. Todas las versiones de fila se mantienen en la misma estructura de datos de la tabla. El control de versiones de fila se utiliza para permitir las lecturas y las escrituras simultáneas en la misma fila. Para obtener más información sobre las lecturas y las escrituras simultáneas en la misma fila, vea [Transactions in Memory-Optimized Tables](memory-optimized-tables.md).  
  
 La siguiente ilustración muestra la multiversión. La ilustración muestra una tabla con tres filas y cada fila tiene versiones diferentes.  
  
 ![Multiversión.](../../database-engine/media/hekaton-tables-1.gif "Multiversión.")  
  
 La tabla tiene tres filas: r1, r2 y r3. r1 tiene tres versiones, r2 tiene dos versiones y r3 tiene cuatro. Observe que las diferentes versiones de la misma fila no ocupan necesariamente ubicaciones de memoria consecutivas. Las diferentes versiones de fila pueden estar dispersas por la estructura de datos de la tabla.  
  
 La estructura de datos de una tabla optimizada para memoria se puede considerar como una colección de versiones de fila. Las filas de tablas basadas en disco se organizan en páginas y extensiones, las filas individuales se direccionan con el desplazamiento de página y número de página, y las versiones de fila de las tablas optimizadas para memoria se direccionan con punteros de memoria de 8 bytes.  
  
## <a name="durability"></a>Durabilidad  
 De forma predeterminada, las tablas optimizadas para memoria son totalmente durables y, al igual que las transacciones en tablas basadas en disco (tradicionales), las transacciones totalmente durables en este tipo de tablas tienen todas las propiedades de atomicidad, coherencia, aislamiento y durabilidad (ACID). Las tablas con optimización para memoria y los procedimientos almacenados compilados de forma nativa admiten un subconjunto de [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 OLTP en memoria admite las tablas duraderas con durabilidad de transacciones retrasada. Las transacciones duraderas retrasadas se guardan en el disco poco después de confirmarse la transacción. El rendimiento es mayor pero, a cambio, las transacciones confirmadas que no se guardaron en el disco se perderán en caso de bloqueo del servidor o conmutación por error.  
  
 Además de las tablas optimizadas para memoria durables predeterminadas, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] también admite tablas optimizadas para memoria no durables, que no se registran y cuyos datos no se guardan en el disco. Esto significa que las transacciones en estas tablas no requieren ninguna E/S de disco, pero los datos no se recuperarán si hay un bloqueo o una conmutación por error del servidor.  
  
## <a name="accessing-data-in-memory-optimized-tables"></a>Acceso a datos en tablas con optimización para memoria  
 Se puede tener acceso a los datos de las tablas optimizadas para memoria de dos maneras:  
  
-   Con [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado (fuera de un procedimiento almacenado compilado de forma nativa). Estas instrucciones de [!INCLUDE[tsql](../../../includes/tsql-md.md)] pueden ser procedimientos almacenados interpretados internamente o pueden ser instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] ad hoc.  
  
-   A través de procedimientos almacenados compilados de forma nativa.  
  
 Se puede tener acceso a las tablas con optimización para memoria de forma más eficaz desde procedimientos almacenados compilados de forma nativa ([Procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md)). Se puede tener acceso también a las tablas con optimización para memoria con [!INCLUDE[tsql](../../../includes/tsql-md.md)]interpretado (tradicional). [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado hace referencia al acceso a tablas optimizadas para memoria sin un procedimiento almacenado compilado de forma nativa. Algunos ejemplos de acceso con [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado son el acceso a una tabla optimizada para memoria desde un desencadenador DML, un lote ad hoc de [!INCLUDE[tsql](../../../includes/tsql-md.md)] , una vista y una función con valores de tabla.  
  
 En la tabla siguiente se resume el acceso con [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado y nativo para varios objetos.  
  
|Característica|Acceso con un procedimiento almacenado compilado de forma nativa|Acceso con [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado|Acceso CLR|  
|-------------|-------------------------------------------------------|-------------------------------------------|----------------|  
|Tablas con optimización para memoria|Sí|Sí|No <sup>1</sup>|  
|[Variables de tabla con optimización para memoria](../../database-engine/memory-optimized-table-variables.md)|Sí|Sí|No|  
|[Procedimientos almacenados compilados de forma nativa](https://msdn.microsoft.com/library/dn133184.aspx)|No puede utilizar la instrucción EXECUTE para ejecutar un procedimiento almacenado desde un procedimiento almacenado compilado de forma nativa.|Sí|No <sup>1</sup>|  
  
 <sup>1</sup> no puede tener acceso a una tabla optimizada para memoria o el procedimiento almacenado compilado de forma nativa desde la conexión de contexto (la conexión desde [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] al ejecutar un módulo CLR). Sin embargo, puede crear y abrir otra conexión en la que pueda tener acceso a las tablas optimizadas para memoria y a los procedimientos almacenados compilados de forma nativa. Para obtener más información, consulte [vs Regular. Conexiones de contexto](../clr-integration/data-access/context-connections-vs-regular-connections.md).  
  
## <a name="performance-and-scalability"></a>Escalabilidad y rendimiento  
 Los siguientes factores afectarán a las mejoras del rendimiento que se pueden lograr con OLTP en memoria:  
  
 Comunicación  
 Una aplicación que realiza muchas llamadas a procedimientos almacenados cortos puede suponer un aumento del rendimiento menor en comparación con una aplicación que realiza menos llamadas e implementa más funcionalidad en cada procedimiento almacenado.  
  
 Ejecución de [!INCLUDE[tsql](../../../includes/tsql-md.md)]  
 OLTP en memoria alcanza el máximo rendimiento cuando se usan procedimientos almacenados compilados de forma nativa en lugar de procedimientos almacenados interpretados o de ejecución de consultas. Los procedimientos almacenados que ejecutan otros procedimientos almacenados no se pueden compilar de forma nativa, pero puede resultar beneficioso el acceso a tablas optimizadas para memoria desde estos procedimientos.  
  
 Examen de intervalo y búsqueda de puntos  
 Los índices no clúster con optimización para memoria admiten los exámenes de intervalo y los exámenes ordenados. Para las búsquedas de puntos, los índices hash optimizados para memoria tienen mejor rendimiento que los índices no clúster optimizados para memoria. Los índices no clúster con optimización para memoria tienen mejor rendimiento que los índices basados en disco.  
  
 Las operaciones de índice no se registran y solo existen en memoria.  
  
 Simultaneidad  
 Las aplicaciones cuyo rendimiento se ve afectado por la simultaneidad del nivel de motor, como la contención de bloqueos temporales o el bloqueo, mejoran significativamente cuando se pasan a OLTP en memoria.  
  
 En la tabla siguiente se enumeran los problemas de rendimiento y escalabilidad que se suelen encontrar en las bases de datos relacionales y el modo en que OLTP en memoria puede mejorar el rendimiento.  
  
|Problema|Impacto de OLTP en memoria|  
|-----------|----------------------------|  
|Rendimiento<br /><br /> Uso elevado de los recursos (CPU, E/S, red o memoria).|CPU<br /> Los procedimientos almacenados compilados de forma nativa pueden reducir el uso de la CPU de forma significativa porque requieren muchas menos instrucciones para ejecutar una instrucción de [!INCLUDE[tsql](../../../includes/tsql-md.md)] si se compara con los procedimientos almacenados interpretados.<br /><br /> OLTP en memoria puede ayudar a reducir la inversión en hardware en las cargas de trabajo con escalado horizontal, ya que un servidor podría ofrecer el rendimiento de entre cinco y diez servidores.<br /><br /> E/S<br /> Si encuentra un cuello de botella de E/S desde el procesamiento hasta las páginas de datos o de índices, OLTP en memoria puede reducir el cuello de botella. Además, la comprobación de los objetos de OLTP en memoria es continua y no produce incrementos súbitos de las operaciones de E/S. Sin embargo, si el espacio de trabajo de las tablas de rendimiento crítico no cabe en la memoria, OLTP en memoria no mejorará el rendimiento porque requiere que los datos residan en la memoria. Si encuentra un cuello de botella de E/S en el registro, OLTP en memoria puede reducirlo porque realiza menos tareas de registro. Si una o más tablas optimizadas para memoria se configuran como tablas no durables, puede eliminar el registro de los datos.<br /><br /> Memoria<br /> OLTP en memoria no proporciona ninguna ventaja de rendimiento. OLTP en memoria puede suponer una presión adicional sobre la memoria, ya que los objetos deben residir en la memoria.<br /><br /> red<br /> OLTP en memoria no proporciona ninguna ventaja de rendimiento. Los datos tienen que comunicarse desde la capa de datos en el nivel de aplicación.|  
|Escalabilidad<br /><br /> La mayoría de los problemas de escala de las aplicaciones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] son causados por problemas de simultaneidad como la contención de bloqueos, bloqueos temporales y bloqueos por subproceso.|Contención de bloqueos temporales<br /> Un escenario típico es la contención en la última página de un índice al insertar filas simultáneamente en el orden de clave. Dado que OLTP en memoria no adopta bloqueos temporales para tener acceso a los datos, los problemas de escalabilidad relacionados con las contenciones de bloqueos temporales desaparecen por completo.<br /><br /> Contención de bloqueo por subproceso<br /> Dado que OLTP en memoria no adopta bloqueos temporales para tener acceso a los datos, los problemas de escalabilidad relacionados con las contenciones de bloqueos por subproceso desaparecen por completo.<br /><br /> Contención relacionada con el bloqueo<br /> Si la aplicación de base de datos encuentra problemas de bloqueo entre las operaciones de lectura y escritura, OLTP en memoria evita dichos problemas porque usa un nuevo formato de control de simultaneidad optimista para implementar todos los niveles de aislamiento de las transacciones. OLTP en memoria no usa TempDB para almacenar las versiones de fila.<br /><br /> Si el problema de escala se debe al conflicto entre dos operaciones de escritura, como dos transacciones simultáneas que intenten actualizar la misma fila, OLTP en memoria permite que una transacción sea correcta y que la otra dé error. La transacción errónea debe volver a enviarse ya sea de forma explícita o implícita, volviendo a intentar la transacción. En cualquier caso, debe realizar cambios en la aplicación.<br /><br /> Si la aplicación experimenta conflictos frecuentes entre dos operaciones de escritura, el valor de bloqueo optimista se reduce. La aplicación no es adecuada para OLTP en memoria. La mayoría de las aplicaciones OLTP no tienen conflictos de escritura a menos que el conflicto sea inducido por la extensión de bloqueo.|  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
