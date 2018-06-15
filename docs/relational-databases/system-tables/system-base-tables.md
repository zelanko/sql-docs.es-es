---
title: Tablas Base del sistema | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system base tables [SQL Server]
- hobt [SQL Server]
- base tables
ms.assetid: 31f2df90-651f-4699-8067-19f59b60904f
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c15a0e42091cffb8010cae36ad43322d361f91fe
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33263038"
---
# <a name="system-base-tables"></a>Tablas base del sistema
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Las tablas base del sistema son las tablas subyacentes que almacenan los metadatos para una base de datos específica. El **maestro** base de datos es especial en este sentido porque contiene algunas tablas adicionales que no se encuentran en cualquiera de estas bases de datos. Estas tablas contienen metadatos persistentes con un ámbito para todo el servidor.  
  
> [!IMPORTANT]  
>  Las tablas base del sistema se utilizan solo en [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y no son para el uso general de los clientes. Están sujetos a cambios y su compatibilidad no está garantizada.  
  
## <a name="system-base-table-metadata"></a>Metadatos de tablas base del sistema  
 Un receptor que tiene el permiso VIEW DEFINITION, ALTER o CONTROL en una base de datos puede ver metadatos de la tabla de base de sistema en el **sys.objects** vista de catálogo. El receptor también puede resolver los nombres y los identificadores de tablas base del sistema del objeto mediante las funciones integradas como [OBJECT_NAME](../../t-sql/functions/object-name-transact-sql.md) y [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md).  
  
 Para enlazar con una tabla base del sistema, un usuario tiene que conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando la conexión de administrador dedicada (DAC). Si intentar ejecutar una consulta SELECT de una tabla base del sistema sin conectarse a través de la conexión DAC, se producirá un error.  
  
> [!IMPORTANT]  
>  El acceso a las tablas base del sistema mediante DAC solo está diseñado para el personal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] y no es un escenario de cliente compatible.  
  
## <a name="system-base-tables"></a>Tablas base del sistema  
 En la tabla siguiente se enumeran y describen todas las tablas base del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Tabla base|Description|  
|----------------|-----------------|  
|**Sys.sysschobjs**|Existe en todas las bases de datos. Cada fila representa un objeto en la base de datos.|  
|**Sys.sysbinobjs**|Existe en todas las bases de datos. Contiene una fila para cada entidad de Service Broker en la base de datos. Las entidades de Service Broker contienen los siguientes elementos:<br /><br /> Tipo de mensaje<br /><br /> Contrato de servicio<br /><br /> ssNoVersion<br /><br /> Los nombres y tipos utilizan intercalación binaria fija.|  
|**Sys.sysclsobjs**|Existe en todas las bases de datos. Contiene una fila para cada entidad clasificada que comparte las mismas propiedades comunes, entre las que se incluyen las siguientes:<br /><br /> Ensamblado<br /><br /> Dispositivo de copia de seguridad<br /><br /> Catálogo de texto completo<br /><br /> Función de partición<br /><br /> Esquema de partición<br /><br /> Grupo de archivos<br /><br /> Clave de ofuscación|  
|**Sys.sysnsobjs**|Existe en todas las bases de datos. Contiene una fila para cada entidad centrada en el espacio de nombres. Esta tabla se usa para almacenar entidades de la colección de XML.|  
|**Sys.syscolpars**|Existe en todas las bases de datos. Contiene una fila para cada columna en una tabla, vista o función con valores de tabla. También contiene las filas para cada parámetro de un procedimiento o función.|  
|**Sys.systypedsubobjs**|Existe en todas las bases de datos. Contiene una fila para cada subentidad escrita. Solo se incluyen en esta categoría los parámetros de la función de partición.|  
|**Sys.sysidxstats**|Existe en todas las bases de datos. Contiene una fila para cada índice o estadísticas para tablas y vistas indizadas<br /><br /> Nota: Todos los índices (excepto el montón) está asociado con una estadística que tiene el mismo nombre que el índice.|  
|**Sys.sysiscols**|Existe en todas las bases de datos. Contiene una fila para cada índice persistente y para columna de estadísticas.|  
|**Sys.sysscalartypes**|Existe en todas las bases de datos. Contiene una fila por cada tipo de sistema o cada tipo definido por el usuario.|  
|**Sys.sysdbreg**|Existe en el **maestro** solo la base de datos. Contiene una fila por cada base de datos registrada.|  
|**Sys.sysxsrvs**|Existe en el **maestro** solo la base de datos. Contiene una fila para cada servidor local, vinculado o remoto.|  
|**Sys.sysrmtlgns**|Esta tabla del sistema base existe en el **maestro** solo la base de datos. Contiene una fila para cada asignación de inicio de sesión remota. Se utiliza para asignar inicios de sesión entrantes originados en el servidor correspondiente para un inicio de sesión local real.|  
|**Sys.syslnklgns**|Existe en el **maestro** solo la base de datos. Contiene una fila para cada asignación de inicio de sesión vinculada. Las llamadas a procedimiento remoto y las consultas distribuidas que proceden de un servidor local fuera de un servidor vinculado correspondiente utilizan las asignaciones de inicio de sesión vinculadas.|  
|**Sys.sysxlgns**|Existe en el **maestro** solo la base de datos. Contiene una fila para cada entidad de seguridad de servidor.|  
|**Sys.sysdbfiles**|Existe en todas las bases de datos. Si la columna **dbid** es cero, la fila representa un archivo que pertenece a esta base de datos. En el **maestro** la base de datos, la columna **dbid** puede ser distinto de cero. Cuando eso ocurra, la fila representará un archivo maestro.|  
|**Sys.sysusermsg**|Existe en el **maestro** solo la base de datos. Cada fila representa un mensaje de error definido por el usuario.|  
|**Sys.sysprivs**|Existe en todas las bases de datos. Contiene una fila para cada permiso de base de datos o de servidor.<br /><br /> Nota: Los permisos de nivel de servidor se almacenan en la **maestro** base de datos.|  
|**Sys.sysowners**|Existe en todas las bases de datos. Cada fila representa una entidad de base de datos.|  
|**Sys.sysobjkeycrypts**|Existe en todas las bases de datos. Contiene una fila para cada clave simétrica, cifrado o propiedad criptográfica asociada a un objeto.|  
|**Sys.syscerts**|Existe en todas las bases de datos. Contiene una fila para cada certificado en una base de datos.|  
|**Sys.sysasymkeys**|Existe en todas las bases de datos. Cada fila representa una clave asimétrica.|  
|**Sys.ftinds**|Existe en todas las bases de datos. Contiene una fila para cada índice de texto completo de la base de datos.|  
|**Sys.sysxprops**|Existe en todas las bases de datos. Contiene una fila para cada propiedad extendida.|  
|**Sys.sysallocunits**|Existe en todas las bases de datos. Contiene una fila para cada unidad de asignación de almacenamiento.|  
|**Sys.sysrowsets**|Existe en todas las bases de datos. Contiene una fila para cada conjunto de filas de particiones para un índice o montón.|  
|**Sys.sysrowsetrefs**|Existe en todas las bases de datos. Contiene una fila para cada índice de la referencia del conjunto de filas.|  
|**Sys.syslogshippers**|Existe en el **maestro** solo la base de datos. Contiene una fila para cada testigo de creación de reflejo de la base de datos.|  
|**Sys.sysremsvcbinds**|Existe en todas las bases de datos. Contiene una fila para cada enlace de servicio remoto.|  
|**Sys.sysconvgroup**|Existe en todas las bases de datos. Contiene una fila para cada instancia de servicio de Service Broker.|  
|**Sys.sysxmitqueue**|Existe en todas las bases de datos. Contiene una fila por cada cola de transmisión de Service Broker.|  
|**Sys.sysdesend**|Existe en todas las bases de datos. Contiene una fila para cada extremo de envío de una conversación de Service Broker.|  
|**Sys.sysdercv**|Existe en todas las bases de datos. Contiene una fila para cada extremo de recepción de una conversación de Service Broker.|  
|**Sys.sysendpts**|Existe en el **maestro** solo la base de datos. Contiene una fila para cada extremo creado en el servidor.|  
|**Sys.syswebmethods**|Existe en el **maestro** solo la base de datos. Contiene una fila para cada método SOAP definido en un extremo HTTP habilitado por SOAP que se crea en el servidor.|  
|**Sys.sysqnames**|Existe en todas las bases de datos. Contiene una fila para cada espacio de nombres o nombre completo de un token del identificador de 4 bytes.|  
|**Sys.sysxmlcomponent**|Existe en todas las bases de datos. Cada fila representa un componente de esquema XML.|  
|**Sys.sysxmlfacet**|Existe en todas las bases de datos. Contiene una fila para cada aspecto de XML (restricción) de definición de tipo de XML.|  
|**Sys.sysxmlplacement**|Existe en todas las bases de datos. Contiene una fila para cada ubicación XML de componentes XML.|  
|**Sys.syssingleobjrefs**|Existe en todas las bases de datos. Contiene una fila para cada referencia general N a 1.|  
|**Sys.sysmultiobjrefs**|Existe en todas las bases de datos. Contiene una fila para cada referencia general N a N.|  
|**Sys.sysobjvalues**|Existe en todas las bases de datos. Contiene una fila para cada propiedad de valor general de una entidad.|  
|**Sys.sysguidrefs**|Existe en todas las bases de datos. Contiene una fila para cada referencia del identificador clasificado por GUID.|  
  
  
