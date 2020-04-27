---
title: Directrices para operaciones de índices en línea | Microsoft Docs
ms.custom: ''
ms.date: 11/11/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- clustered indexes, online operations
- online index operations
- indexes [SQL Server], online operations
- disk space [SQL Server], indexes
- nonclustered indexes [SQL Server], online operations
- transaction logs [SQL Server], indexes
ms.assetid: d82942e0-4a86-4b34-a65f-9f143ebe85ce
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e2f7a25a4a6a4bb6b8f153a8b04b47aeb542265c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63162485"
---
# <a name="guidelines-for-online-index-operations"></a>Directrices para operaciones de índices en línea
  Al realizar operaciones de índice en línea se aplican las siguientes directrices:  
  
-   Los índices clúster deben crearse, volver a compilarse o quitarse sin conexión cuando la tabla subyacente contiene los siguientes tipos de datos de objetos `image`grandes (LOB) `text`:, **ntext**y.  
  
-   Los índices de tablas temporales locales no se pueden crear, reconstruir o quitar en línea. Esta restricción no se aplica a los índices de tablas temporales globales.  
  
> [!NOTE]  
>  Las operaciones de índices en línea no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 En la siguiente tabla se muestran operaciones de índice que se pueden llevar a cabo estando en línea y los índices que se excluyen de esas operaciones en línea. También se incluyen restricciones adicionales.  
  
|Operación de índice en línea|Índices excluidos|Otras restricciones|  
|----------------------------|----------------------|------------------------|  
|ALTER INDEX REBUILD|Índice clúster deshabilitado o vista indizada deshabilitada<br /><br /> Índice XML <br /><br />Índice de almacén de columnas<br /><br /> Índice de una tabla temporal local|Si se especifica la palabra clave ALL la operación puede ser errónea si la tabla contiene un índice excluido.<br /><br /> Se aplican restricciones adicionales para reconstruir índices deshabilitados. Para obtener más información, vea [Deshabilitar índices y restricciones](disable-indexes-and-constraints.md).|  
|CREATE INDEX|Índice XML<br /><br /> Índice clúster único inicial en una vista<br /><br /> Índice de una tabla temporal local||  
|CREATE INDEX WITH DROP_EXISTING|Índice clúster deshabilitado o vista indizada deshabilitada<br /><br /> Índice de una tabla temporal local<br /><br /> Índice XML||  
|DROP INDEX|Índice deshabilitado<br /><br /> Índice XML<br /><br /> Índice no clúster<br /><br /> Índice de una tabla temporal local|No se pueden especificar varios índices en una única instrucción.|  
|ALTER TABLE ADD CONSTRAINT (PRIMARY KEY o UNIQUE)|Índice de una tabla temporal local<br /><br /> Índice agrupado|Solo se permite una subcláusula cada vez. Por ejemplo, no puede agregar y quitar restricciones PRIMARY KEY o UNIQUE en la misma instrucción ALTER TABLE.|  
||||  
  
 La tabla subyacente no se puede modificar, truncar o quitar mientras se está llevando a cabo una operación de índice en línea.  
  
 La configuración de opción en línea (ON u OFF) especificada al crear o quitar un índice clúster se aplica a índices no clúster que se deben reconstruir. Por ejemplo, si el índice clúster se genera en línea utilizando CREATE INDEX WITH DROP_EXISTING, ONLINE=ON, todos los índices no clúster asociados se vuelven a crear en línea también.  
  
 Cuando crea o reconstruye un índice UNIQUE en línea, el generador de índices y una transacción de usuario simultánea pueden intentar insertar la misma clave, infringiendo su unicidad. Si una fila especificada por un usuario se inserta en el nuevo índice (destino) antes de que la fila original de la tabla de origen se mueva al nuevo índice, se producirá un error en la operación de índice en línea.  
  
 Aunque no es común, la operación de índice en línea puede causar un interbloqueo cuando interactúa con las actualizaciones de la base de datos debido a las actividades de una aplicación o de un usuario. En esos casos poco comunes, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] seleccionará el usuario o la actividad de la aplicación como sujeto de interbloqueo.  
  
 Solo puede realizar operaciones DDL de índice en línea simultáneas en la misma tabla o vista cuando crea varios índices no clúster o reorganiza índices no clúster. Se producirá un error en todas las operaciones de índice en línea que se realizan al mismo momento. Por ejemplo, no puede crear un índice en línea mientras reconstruye un índice en línea existente en la misma tabla.  
  
 No se puede realizar una operación en línea cuando un índice contiene una columna del tipo de objetos grandes y en la misma transacción hay operaciones de actualización delante de esta operación en línea. Para solucionar temporalmente este problema, ponga la operación en línea fuera de la transacción o colóquela antes que cualquier actualización en la transacción.  
  
## <a name="disk-space-considerations"></a>Consideraciones acerca del espacio en disco  
 Normalmente, los requisitos de espacio en disco son los mismos para operaciones de índice en línea y sin conexión. Una excepción es el espacio en disco adicional que necesita el índice de asignación temporal. Este índice temporal se utiliza en operaciones de índice en línea que crean, reconstruyen o quitan un índice clúster. Para quitar un índice clúster en línea se requiere tanto espacio como para crearlo. Para más información, consulte [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md).  
  
## <a name="performance-considerations"></a>Consideraciones de rendimiento  
 Aunque las operaciones de índice en línea permiten actividades de actualización de usuario simultáneas, las operaciones de índice tardan más si la actividad de actualización es muy grande. Normalmente, las operaciones de índice en línea son más lentas que las operaciones de índice sin conexión equivalentes, independientemente del nivel de actividad de actualización simultánea.  
  
 Como las estructuras de origen y de destino se mantienen durante la operación de índice en línea, el uso de recursos para insertar, actualizar y eliminar transacciones aumenta, potencialmente hasta el doble. Esto puede provocar una reducción del rendimiento y un mayor uso de los recursos, especialmente de tiempo de CPU, durante la operación de índice. Las operaciones de índice en línea se registran totalmente.  
  
 Aunque se recomiendan las operaciones en línea, se debe evaluar el entorno y los requisitos específicos. Puede ser mejor ejecutar operaciones de índice sin conexión. Al hacerlo así, los usuarios tienen acceso restringido a los datos durante la operación, pero la operación acaba más rápido y utiliza menos recursos.  
  
 En los equipos con varios procesadores que ejecutan [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], las instrucciones sobre índices pueden usar más procesadores para realizar las operaciones de examen y ordenación asociadas a dicha instrucción, al igual que hacen otras consultas. Puede utilizar la opción de índice MAXDOP para controlar el número de procesadores dedicados a la operación de índice en línea. De este modo, puede equilibrar los recursos utilizados por la operación de índice con los de los usuarios simultáneos. Para obtener más información, vea [Configurar operaciones de índice en paralelo](configure-parallel-index-operations.md). Para obtener más información sobre las ediciones de SQL Server que admiten operaciones indizadas en paralelo, vea [características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Debido a que un bloqueo S o un bloqueo Sch-M se conservan en la fase final de la operación de índice, debe tener cuidado cuando ejecute una operación de índice en línea dentro de una transacción de usuario explícita, como el bloque BEGIN TRANSACTION...COMMIT. De esta manera el bloqueo se conserva hasta el final de la transacción y se impide la simultaneidad de usuarios.  
  
 La regeneración de índices en línea puede aumentar la fragmentación cuando se puede ejecutar con las opciones `MAX DOP > 1` y `ALLOW_PAGE_LOCKS = OFF` . Para obtener más información, vea el blog [How It Works: Online Index Rebuild - Can Cause Increased Fragmentation](https://blogs.msdn.com/b/psssql/archive/2012/09/05/how-it-works-online-index-rebuild-can-cause-increased-fragmentation.aspx)(Cómo la regeneración de índices en línea puede provocar una fragmentación mayor).  
  
## <a name="transaction-log-considerations"></a>Consideraciones del registro de transacciones  
 Las operaciones de índice a gran escala, realizadas sin conexión o en línea, pueden generar grandes cargas de datos que pueden hacer que el registro de transacciones se llene rápidamente. Para estar seguros de que la operación de índice se pueda revertir, el registro de transacciones no se puede truncar hasta que se haya completado la operación de índice; no obstante, se puede realizar una copia de seguridad del registro durante la operación de índice. Por lo tanto, el registro de transacciones debe tener suficiente espacio para almacenar las transacciones de la operación de índice y cualquier transacción de usuario simultánea durante la operación de índice. Para más información, consulte [Transaction Log Disk Space for Index Operations](transaction-log-disk-space-for-index-operations.md).  
  
## <a name="related-content"></a>Contenido relacionado  
 [Cómo funcionan las operaciones de índice en línea](how-online-index-operations-work.md)  
  
 [Realizar operaciones de índice en línea](perform-index-operations-online.md)  
  
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)  
  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
  
