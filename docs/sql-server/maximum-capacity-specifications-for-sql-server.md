---
title: "Especificaciones de capacidad máxima para SQL Server | Microsoft Docs"
ms.date: 11/6/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- objects [SQL Server]
- number capacity specifications [SQL Server]
- size [SQL Server], capacity specifications
- number of objects
- capacity specifications [SQL Server]
- maximum capacity specifications [SQL Server]
- size [SQL Server]
- replication capacity specifications [SQL Server]
- objects [SQL Server], capacity specifications
- Database Engine [SQL Server], capacity specifications
ms.assetid: 13e95046-0e76-4604-b561-d1a74dd824d7
caps.latest.revision: "88"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: c56b0a570f295896e76c5d0b3441042543445178
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="maximum-capacity-specifications-for-sql-server"></a>Especificaciones de capacidad máxima para SQL Server

 > Para obtener contenido relacionado con versiones anteriores de SQL Server, vea [Especificaciones de capacidad máxima para SQL Server](https://msdn.microsoft.com/en-US/library/ms143432(SQL.120).aspx).

  En las siguientes tablas se especifican el tamaño y el número máximo de diversos objetos definidos en los componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para navegar hasta la tabla de una tecnología de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , haga clic en su vínculo:  
  
 [Objetos de motor de base de datos de SQL Server](#Engine)  
  
 [Objetos de Utilidad de SQL Server](#Utility)  
  
 [Objetos de aplicación de nivel de datos de SQL Server](#DAC)  
  
 [Objetos de replicación de SQL Server](#Replication)  
  
##  <a name="Engine"></a> [!INCLUDE[ssDE](../includes/ssde-md.md)] Objetos  
 Tamaño y número máximo de diversos objetos definidos en las bases de datos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o a los que se hace referencia en las instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] .  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] objeto||Tamaños o cifras máximas [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bits)|Información adicional|  
|---------------------------------------------------------|-|------------------------------------------------------------------|----------------------------|  
|Tamaño del lote||65.536 * Tamaño de paquete de red|El tamaño del paquete de red es el tamaño de los paquetes de flujo TDS usados para la comunicación entre aplicaciones y el [!INCLUDE[ssDE](../includes/ssde-md.md)]relacional. El tamaño del paquete predeterminado es 4 KB y se controla mediante la opción de configuración Tamaño de paquete de red.|  
|Bytes por columna de cadenas cortas||8,000||  
|Bytes por GROUP BY y ORDER BY||8,060||  
|Bytes por clave de índice||900 bytes para un índice agrupado. 1700 para un índice no agrupado.|El número máximo de bytes de una clave de índice agrupado no puede superar los 900 en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para una clave de índice no agrupado, el máximo es 1700 bytes.<br /><br /> Puede definir una clave usando columnas de longitud variable cuyos tamaños máximos sumen más del límite. Pero los tamaños combinados de los datos de dichas columnas no pueden superar el límite.<br /><br /> En un índice no agrupado, puede incluir más columnas sin clave. Estas no contarán para el límite de tamaño de la clave. Las columnas sin clave pueden ayudar a que algunas consultas den mejores resultados.|  
|Bytes por clave de índice en tablas optimizadas para memoria||2500 bytes para un índice no agrupado. No hay límite para un índice de hash, siempre y cuando todas claves de índice quepan en la fila.|En una tabla optimizada para memoria, un índice no agrupado no puede tener columnas de clave cuyos tamaños máximos declarados superen los 2500 bytes. No importa si los datos reales de las columnas de clave son más cortos que los tamaños máximos declarados.<br /><br /> Las clave de índice de hash no tienen límite máximo de tamaño.<br /><br /> En el caso de los índices de tablas optimizadas para memoria no existe el concepto de columnas incluidas, ya que todos los índices cubren de forma inherente todas las columnas.<br /><br /> En el caso de las tablas optimizadas para memoria, aunque el tamaño de fila sea de 8060 bytes, algunas columnas de longitud variable pueden almacenarse físicamente fuera de esos 8060 bytes. Pero los tamaños máximos declarados de todas las columnas de clave para todos los índices de una tabla, más las columnas adicionales de longitud fija de la tabla, deben caber en dichos 8060 bytes.|  
|Bytes por clave externa||900||  
|Bytes por clave principal||900||  
|Bytes por fila||8,060|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite el almacenamiento de desbordamiento de fila, lo que habilita la inserción de columnas de longitud variable de manera no consecutiva. Solo se almacena una raíz de 24 bytes en el registro principal para las columnas de longitud variable que se insertan de manera no consecutiva; por ello, el límite real por fila es más alto que en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener más información, vea el tema "Datos de desbordamiento de fila superiores a 8 kB" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|Bytes por fila en tablas optimizadas para memoria||8,060|A partir de [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] , las tablas optimizadas para memoria admiten el almacenamiento no consecutivo. Las columnas de longitud variable se insertan de manera no consecutiva si el tamaño máximo de todas las columnas de la tabla supera los 8060 bytes; se trata de una decisión en tiempo de compilación. Solo se almacena una referencia de 8 bytes de forma consecutiva para las columnas almacenadas de forma no consecutiva. Para obtener más información, vea [Tamaño de tabla y fila de las tablas con optimización para memoria](../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md).|  
|Bytes en texto de origen de un procedimiento almacenado||El menor del tamaño del lote o 250 MB||  
|Bytes por columna **varchar(max)**, **varbinary(max)**, **xml**, **text**o **image**||2^31-1||  
|Caracteres por columna **ntext** o **nvarchar(max)**||2^30-1||  
|Índices clúster por tabla||1||  
|Columnas en GROUP BY y ORDER BY||Limitado solo por el número de bytes||  
|Columnas o expresiones en una instrucción GROUP BY WITH CUBE o WITH ROLLUP||10||  
|Columnas por clave de índice||32|Si la tabla contiene uno o varios índices XML, la clave de agrupación en clústeres de la tabla de usuario estará limitada a 31 columnas, ya que la columna XML se agrega a la clave de agrupación en clústeres del índice XML principal. En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], puede incluir columnas sin clave en un índice no agrupado para evitar la limitación de un máximo de 32 columnas de clave. Para más información, consulte [Create Indexes with Included Columns](../relational-databases/indexes/create-indexes-with-included-columns.md).|  
|Columnas por clave externa||32||  
|Columnas por clave principal||32||  
|Columnas por tabla no ancha||1,024||  
|Columnas por tabla ancha||30,000||  
|Columnas por instrucción SELECT||4,096||  
|Columnas por instrucción INSERT||4,096||  
|Conexiones por cliente||Valor máximo de conexiones configuradas||  
|Tamaño de la base de datos||524 272 terabytes||  
|Bases de datos por instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||32,767||  
|Grupos de archivos por base de datos||32,767||  
|Grupos de archivo por base de datos para datos optimizados para memoria.||1||  
|Archivos por base de datos||32,767||  
|Tamaño de archivo (datos)||16 terabytes||  
|Tamaño de archivo (registro)||2 terabytes||  
|Archivos de datos para datos optimizados para memoria por base de datos||4.096 en [!INCLUDE[ssSQL14](../includes/ssSQL14-md.md)]. Las versiones posteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no imponen un límite tan estricto.||  
|Archivo delta por archivo de datos para datos optimizados para memoria||1||  
|Referencias de tabla de claves externas por tabla||Saliente = 253. Entrante = 10 000.|Para ver las restricciones, vea [Create Foreign Key Relationships](../relational-databases/tables/create-foreign-key-relationships.md).|  
|Longitud del identificador (en caracteres)||128||  
|Instancias por equipo||50 instancias en un servidor independiente.<br /><br /> 25 instancias en un clúster de conmutación por error cuando se usa un disco de clúster compartido como opción de almacenamiento para la instalación del clúster; [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite 50 instancias en un clúster de conmutación por error si elige recursos compartidos de archivos SMB como opción de almacenamiento para la instalación del clúster.||  
|Índices por tabla optimizada para memoria||999 a partir de [!INCLUDE[ssSQL17](../includes/ssSQL17-md.md)] y en [!INCLUDE[ssSDSFull](../includes/ssSDSFull-md.md)]<br/>8 en [!INCLUDE[ssSQL14](../includes/ssSQL14-md.md)] y [!INCLUDE[ssSQL15](../includes/ssSQL15-md.md)]||  
|Longitud de una cadena que contiene instrucciones SQL (tamaño de lote)||65.536 * Tamaño de paquete de red|El tamaño del paquete de red es el tamaño de los paquetes de flujo TDS usados para la comunicación entre aplicaciones y el [!INCLUDE[ssDE](../includes/ssde-md.md)]relacional. El tamaño del paquete predeterminado es 4 KB y se controla mediante la opción de configuración Tamaño de paquete de red.|  
|Bloqueos por conexión||Máximo de bloqueos por servidor||  
|Bloqueos por instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||Limitado solo por la memoria|Este valor sirve para asignaciones de bloqueo estático. Los bloqueos dinámicos están limitados solo por la memoria.|  
|Niveles de procedimientos almacenados anidados||32|Si un procedimiento almacenado tiene acceso a más de 64 bases de datos o a más de 2 bases de datos en intercalación, recibirá un error.|  
|Subconsultas anidadas||32||  
|Niveles de desencadenadores anidados||32||  
|Índices no clúster por tabla||999||  
|El número de expresiones distintas en la cláusula BY GROUP cuando cualquiera de los elementos siguientes está presente: CUBE, ROLLUP, GROUPING SETS, WITH CUBE, WITH ROLLUP||32||  
|El número de conjuntos de agrupamiento generados por los operadores de la cláusula BY GROUP||4,096||  
|Parámetros por procedimiento almacenado||2,100||  
|Parámetros por función definida por el usuario||2,100||  
|REFERENCES por tabla||253||  
|Filas por tabla||Limitado por el espacio de almacenamiento disponible||  
|Tablas por base de datos||Limitado por el número de objetos de la base de datos|Los objetos de base de datos incluyen objetos como tablas, vistas, procedimientos almacenados, funciones definidas por el usuario, desencadenadores, reglas, valores predeterminados y restricciones. La suma de todos estos objetos en una base de datos no puede superar 2.147.483.647.|  
|Particiones por tabla o índice con particiones||15,000||  
|Estadísticas en columnas no indizadas||30,000|| 
|Tablas por instrucción SELECT||Limitado solo por los recursos disponibles||  
|Desencadenadores por tabla||Limitado por el número de objetos de la base de datos|Los objetos de base de datos incluyen objetos como tablas, vistas, procedimientos almacenados, funciones definidas por el usuario, desencadenadores, reglas, valores predeterminados y restricciones. La suma de todos estos objetos en una base de datos no puede superar 2.147.483.647.|  
|Columnas por instrucción UPDATE (tablas anchas)||4096||  
|Conexiones de usuario||32,767||  
|índices XML||249||  
  
##  <a name="Utility"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objetos de utilidad  
 Tamaño y número máximo de diversos objetos que se probaron en la Utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objeto de utilidad||Tamaños o cifras máximas [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bits)|  
|----------------------------------------------|-|------------------------------------------------------------------|  
|Equipos (equipos físicos o máquinas virtuales) por cada utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||100|  
|Instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] por equipo||5|  
|Número total de instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] por cada utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||200*|  
|Bases de datos de usuario por instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], incluidas las aplicaciones de capa de datos||50|  
|Número total de bases de datos de usuario por cada utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||1,000|  
|Grupos de archivos por base de datos||1|  
|Archivos de datos por grupo de archivos||1|  
|Archivos de registro por base de datos||1|  
|Volúmenes por equipo||3|  
  
 *El número máximo de instancias administradas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admitidas por la Utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] puede variar según la configuración de hardware del servidor. Para obtener información de introducción, vea [Características y tareas de la utilidad de SQL Server](https://msdn.microsoft.com/library/ee210548.aspx). [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no está disponible en todas las ediciones de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](https://msdn.microsoft.com/library/cc645993.aspx).    
  
##  <a name="DAC"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objetos de aplicación de capa de datos  
 Tamaño y número máximo de diversos objetos que se probaron en las aplicaciones de capa de datos (DAC) de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objeto DAC||Tamaños o cifras máximas [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bits)|  
|------------------------------------------|-|------------------------------------------------------------------|  
|Bases de datos por DAC||1|  
|Objetos por DAC*||Se limita por el número de objetos de una base de datos o la memoria disponible.|  
  
 *Los tipos de objetos incluidos en el límite son usuarios, tablas, vistas, procedimientos almacenados, funciones definidas por el usuario, tipos de datos definidos por el usuario, roles de base de datos, esquemas y tipos de tabla definidos por el usuario.  
  
##  <a name="Replication"></a> Objetos de replicación  
 Tamaño y número máximo de los diversos objetos definidos en Replicación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objeto de replicación||Tamaño y número máximo SQL Server (64 bits)|  
|--------------------------------------------------|-|---------------------------------------------------|  
|Artículos (publicación de combinación)||2048|  
|Artículos (publicación de instantáneas o transaccional)||32,767|  
|Columnas de una tabla* (publicación de mezcla)||246|  
|Columnas de una tabla**(publicación de instantáneas o transaccional de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] )||1,000|  
|Columnas de una tabla** (publicación de instantáneas o transaccional de Oracle)||995|  
|Bytes para una columna utilizada en un filtro de fila (publicación de combinación)||1,024|  
|Bytes para una columna utilizada en un filtro de fila (publicación de instantáneas o transaccional)||8,000|  

 *Si se utiliza el seguimiento por fila en la detección de conflictos (valor predeterminado), la tabla base puede incluir un máximo de 1024 columnas, pero las columnas deben filtrarse desde el artículo de forma que se publique un máximo de 246 columnas. Si se utiliza el seguimiento por columna, la tabla base puede incluir 246 columnas como máximo.  
  
 **La tabla base puede incluir el número máximo de columnas permitido en la base de datos de publicación (1024 para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]), pero las columnas deben filtrarse desde el artículo si superan el máximo especificado para el tipo de publicación.  
  
## <a name="see-also"></a>Vea también  
 [Requisitos de hardware y software para instalar SQL Server 2016](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Comprobar los parámetros del Comprobador de configuración del sistema](../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [Características y tareas de la utilidad de SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
