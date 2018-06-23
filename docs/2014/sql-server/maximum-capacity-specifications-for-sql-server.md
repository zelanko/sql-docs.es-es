---
title: Especificaciones de capacidad máxima para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 76
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6b85f0d59501aea5ef8a77daadd6f74796a82b41
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113306"
---
# <a name="maximum-capacity-specifications-for-sql-server"></a>Especificaciones de capacidad máxima para SQL Server
  En las siguientes tablas se especifican el tamaño y la cantidad máximos de diversos objetos definidos en los componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para navegar hasta la tabla de una tecnología de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , haga clic en su vínculo:  
  
 [Objetos de motor de base de datos de SQL Server](#Engine)  
  
 [Objetos de Utilidad de SQL Server](#Utility)  
  
 [Objetos de aplicación de nivel de datos de SQL Server](#DAC)  
  
 [Objetos de replicación de SQL Server](#Replication)  
  
##  <a name="Engine"></a> [!INCLUDE[ssDE](../includes/ssde-md.md)] Objetos  
 En la siguiente tabla se especifican el tamaño y la cantidad máxima de diversos objetos definidos en las bases de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o a los que se hace referencia en las instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] objeto|Tamaños o cifras máximas [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 bits)|Tamaños o cifras máximas [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bits)|  
|---------------------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|Tamaño del lote<br /><br /> Nota: Network Packet Size es el tamaño de los paquetes de flujo TDS de TDS utilizados para la comunicación entre aplicaciones y relacionales [!INCLUDE[ssDE](../includes/ssde-md.md)]. El tamaño del paquete predeterminado es 4 KB y se controla mediante la opción de configuración Tamaño de paquete de red.|65.536 * Tamaño de paquete de red|65.536 * Tamaño de paquete de red|  
|Bytes por columna de cadenas cortas|8,000|8,000|  
|Bytes por GROUP BY y ORDER BY|8,060|8,060|  
|Bytes por clave de índice<br /><br /> Nota: El número máximo de bytes en una clave de índice no puede superar los 900 en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Puede definir una clave utilizando columnas de longitud variable cuyos tamaños máximos sumen hasta más de 900, siempre que ninguna fila se haya insertado con más de 900 bytes de datos en dichas columnas. En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], puede incluir columnas sin clave en un índice no clúster para evitar el tamaño máximo de clave de índice de 900 bytes.|900|900|  
|Bytes por clave externa|900|900|  
|Bytes por clave principal|900|900|  
|Bytes por fila<br /><br /> Nota:<br />        [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite el almacenamiento de desbordamiento de fila, lo que habilita la inserción de columnas de longitud variable de manera no consecutiva. Solo se almacena una raíz de 24 bytes en el registro principal para las columnas de longitud variable que se insertan de manera no consecutiva; por ello, el límite real por fila es más alto que en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener más información, vea el tema "Datos de desbordamiento de fila superiores a 8 kB" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|8,060|8,060|  
|Bytes por fila en tablas optimizadas para memoria<br /><br /> Nota:<br />        [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] OLTP en memoria no admite el almacenamiento de desbordamiento de fila. Las columnas de longitud variable no son de inserción no consecutiva. Esto limita al tamaño máximo de fila el ancho máximo de las columnas de longitud variable que se puede especificar en una tabla optimizada para memoria. Para obtener más información, vea [Tamaño de tabla y fila de las tablas con optimización para memoria](../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md).|No compatible|8,060|  
|Bytes en texto de origen de un procedimiento almacenado|El menor del tamaño del lote o 250 MB|El menor del tamaño del lote o 250 MB|  
|Bytes por columna `varchar(max)`, `varbinary(max)`, `xml`, `text` o `image`|2^31-1|2^31-1|  
|Caracteres por columna `ntext` o `nvarchar(max)`|2^30-1|2^30-1|  
|Índices clúster por tabla|1|1|  
|Columnas en GROUP BY y ORDER BY|Limitado solo por el número de bytes|Limitado solo por el número de bytes|  
|Columnas o expresiones en una instrucción GROUP BY WITH CUBE o WITH ROLLUP|10|10|  
|Columnas por clave de índice<br /><br /> Nota: Si la tabla contiene uno o más índices XML, la clave de agrupación de la tabla de usuario está limitada a 15 columnas porque la columna XML se agrega a la clave de agrupación en clústeres del índice XML principal. En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], puede incluir columnas sin clave en un índice no agrupado para evitar la limitación de un máximo de 16 columnas de clave. Para más información, consulte [Create Indexes with Included Columns](../relational-databases/indexes/create-indexes-with-included-columns.md).|16|16|  
|Columnas por clave externa|16|16|  
|Columnas por clave principal|16|16|  
|Columnas por tabla no ancha|1,024|1,024|  
|Columnas por tabla ancha|30,000|30,000|  
|Columnas por instrucción SELECT|4,096|4,096|  
|Columnas por instrucción INSERT|4096|4096|  
|Conexiones por cliente|Valor máximo de conexiones configuradas|Valor máximo de conexiones configuradas|  
|Tamaño de la base de datos|524 272 terabytes|524 272 terabytes|  
|Bases de datos por instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|32,767|32,767|  
|Grupos de archivos por base de datos|32,767|32,767|  
|Grupos de archivo por base de datos para datos optimizados para memoria.|No compatible|1|  
|Archivos por base de datos|32,767|32,767|  
|Tamaño de archivo (datos)|16 terabytes|16 terabytes|  
|Tamaño de archivo (registro)|2 terabytes|2 terabytes|  
|Archivos de datos para datos optimizados para memoria por base de datos|No compatible|4.096|  
|Archivo delta por archivo de datos para datos optimizados para memoria|No compatible|1|  
|Referencias de tabla de claves externas por tabla<br /><br /> Nota: Aunque una tabla puede contener un número ilimitado de restricciones FOREIGN KEY, el máximo recomendado es 253. Según la configuración de hardware que hospeda a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], la especificación de restricciones FOREIGN KEY adicionales puede ser un proceso difícil para el optimizador de consultas.|253|253|  
|Longitud del identificador (en caracteres)|128|128|  
|Instancias por equipo|50 instancias en un servidor independiente para todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite 25 instancias en una conmutación por error de clúster cuando se usa un disco de clúster compartido como opción de almacenamiento para la instalación del clúster [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] recursos compartidos de archivos admite 50 instancias en una conmutación por error de clúster si elige SMB como opción de almacenamiento para la instalación del clúster Para obtener más información, consulte [requisitos de Hardware y Software para instalar SQL Server 2014](install/hardware-and-software-requirements-for-installing-sql-server.md).|50 instancias en un servidor independiente.<br /><br /> 25 instancias en un clúster de conmutación por error cuando se usa un disco de clúster compartido como opción de almacenamiento para la instalación del clúster; [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite 50 instancias en un clúster de conmutación por error si elige recursos compartidos de archivos SMB como opción de almacenamiento para la instalación del clúster.|  
|Índices por tabla optimizada para memoria|No compatible|8|  
|Longitud de una cadena que contiene instrucciones SQL (tamaño de lote)<br /><br /> Nota: Network Packet Size es el tamaño de los paquetes de flujo TDS de TDS utilizados para la comunicación entre aplicaciones y relacionales [!INCLUDE[ssDE](../includes/ssde-md.md)]. El tamaño del paquete predeterminado es 4 KB y se controla mediante la opción de configuración Tamaño de paquete de red.|65.536 * Tamaño de paquete de red|65.536 * Tamaño de paquete de red|  
|Bloqueos por conexión|Máximo de bloqueos por servidor|Máximo de bloqueos por servidor|  
|Bloqueos por instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]<br /><br /> Nota: Este valor sirve para asignaciones de bloqueo estático. Los bloqueos dinámicos están limitados solo por la memoria.|Hasta 2.147.483.647|Limitado solo por la memoria|  
|Niveles de procedimientos almacenados anidados<br /><br /> Nota: Si un procedimiento almacenado tiene acceso a más de 64 bases de datos, o más de 2 bases de datos en intercalación, recibirá un error.|32|32|  
|Subconsultas anidadas|32|32|  
|Niveles de desencadenadores anidados|32|32|  
|Índices no clúster por tabla|999|999|  
|El número de expresiones distintas en la cláusula BY GROUP cuando cualquiera de los elementos siguientes está presente: CUBE, ROLLUP, GROUPING SETS, WITH CUBE, WITH ROLLUP|32|32|  
|El número de conjuntos de agrupamiento generados por los operadores de la cláusula BY GROUP|4,096|4,096|  
|Parámetros por procedimiento almacenado|2,100|2,100|  
|Parámetros por función definida por el usuario|2,100|2,100|  
|REFERENCES por tabla|253|253|  
|Filas por tabla|Limitado por el espacio de almacenamiento disponible|Limitado por el espacio de almacenamiento disponible|  
|Tablas por base de datos<br /><br /> Nota: Los objetos de base de datos incluyen objetos como tablas, vistas, procedimientos almacenados, funciones definidas por el usuario, desencadenadores, reglas, valores predeterminados y restricciones. La suma de todos estos objetos en una base de datos no puede superar 2.147.483.647.|Limitado por el número de objetos de la base de datos|Limitado por el número de objetos de la base de datos|  
|Particiones por tabla o índice con particiones|1,000<br /><br /> **\*\* Importante \* \***  crear una tabla o índice con más de 1.000 particiones es posible en un sistema de 32 bits, pero no se admite.|15,000|  
|Estadísticas en columnas no indizadas|30,000|30,000|  
|Tablas por instrucción SELECT|Limitado solo por los recursos disponibles|Limitado solo por los recursos disponibles|  
|Desencadenadores por tabla<br /><br /> Nota: Los objetos de base de datos incluyen objetos como tablas, vistas, procedimientos almacenados, funciones definidas por el usuario, desencadenadores, reglas, valores predeterminados y restricciones. La suma de todos estos objetos en una base de datos no puede superar 2.147.483.647.|Limitado por el número de objetos de la base de datos|Limitado por el número de objetos de la base de datos|  
|Columnas por instrucción UPDATE (tablas anchas)|4096|4096|  
|Conexiones de usuario|32,767|32,767|  
|índices XML|249|249|  
  
##  <a name="Utility"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objetos de utilidad  
 En la siguiente tabla se especifican el tamaño y cantidad máximos de diversos objetos que se probaron en la utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objeto de utilidad|Tamaños o cifras máximas [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 bits)|Tamaños o cifras máximas [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bits)|  
|----------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|Equipos (equipos físicos o máquinas virtuales) por cada utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|100|100|  
|Instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] por equipo|5|5|  
|Número total de instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] por cada utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|200*|200*|  
|Bases de datos de usuario por instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], incluidas las aplicaciones de capa de datos|50|50|  
|Número total de bases de datos de usuario por cada utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|1,000|1,000|  
|Grupos de archivos por base de datos|1|1|  
|Archivos de datos por grupo de archivos|1|1|  
|Archivos de registro por base de datos|1|1|  
|Volúmenes por equipo|3|3|  
  
 * El número máximo de instancias administradas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilidad puede variar según la configuración de hardware del servidor. Para obtener información de introducción, vea [Características y tareas de la utilidad de SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md). El punto de control de la Utilidad de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no está disponible en todas las ediciones de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
##  <a name="DAC"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objetos de aplicación de capa de datos  
 En la tabla siguiente se especifican los tamaños y la cantidad máxima de diversos objetos que se probaron en las aplicaciones de capa de datos (DAC) de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objeto DAC|Tamaños o cifras máximas [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 bits)|Tamaños o cifras máximas [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bits)|  
|------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|Bases de datos por DAC|1|1|  
|Objetos por DAC*|Se limita por el número de objetos de una base de datos o la memoria disponible.|Se limita por el número de objetos de una base de datos o la memoria disponible.|  
  
 *Los tipos de objetos incluidos en el límite son usuarios, tablas, vistas, procedimientos almacenados, funciones definidas por el usuario, tipos de datos definidos por el usuario, roles de base de datos, esquemas y tipos de tabla definidos por el usuario.  
  
##  <a name="Replication"></a> Objetos de replicación  
 En la siguiente tabla se especifican el tamaño y la cantidad máxima de diversos objetos definidos en la replicación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objeto de replicación|Tamaño y cantidad máxima de SQL Server (32 bits)|Tamaño y número máximo SQL Server (64 bits)|  
|--------------------------------------------------|---------------------------------------------------|---------------------------------------------------|  
|Artículos (publicación de combinación)|256|256|  
|Artículos (publicación de instantáneas o transaccional)|32,767|32,767|  
|Columnas de una tabla* (publicación de mezcla)|246|246|  
|Columnas de una tabla**(publicación de instantáneas o transaccional de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] )|1,000|1,000|  
|Columnas de una tabla** (publicación de instantáneas o transaccional de Oracle)|995|995|  
|Bytes para una columna utilizada en un filtro de fila (publicación de combinación)|1,024|1,024|  
|Bytes para una columna utilizada en un filtro de fila (publicación de instantáneas o transaccional)|8,000|8,000|  
  
 *Si se utiliza el seguimiento por fila en la detección de conflictos (valor predeterminado), la tabla base puede incluir un máximo de 1024 columnas, pero las columnas deben filtrarse desde el artículo de forma que se publique un máximo de 246 columnas. Si se utiliza el seguimiento por columna, la tabla base puede incluir 246 columnas como máximo.  
  
 **La tabla base puede incluir el número máximo de columnas permitido en la base de datos de publicación (1024 para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]), pero las columnas deben filtrarse desde el artículo si superan el máximo especificado para el tipo de publicación.  
  
## <a name="see-also"></a>Vea también  
 [Requisitos de hardware y Software para instalar SQL Server 2014](install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Comprobar los parámetros del Comprobador de configuración del sistema](../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [Características y tareas de la utilidad de SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  