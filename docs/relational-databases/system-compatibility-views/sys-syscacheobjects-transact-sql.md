---
title: Sys.syscacheobjects (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.syscacheobjects_TSQL
- sys.syscacheobjects
- syscacheobjects
- syscacheobjects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscacheobjects system table
- sys.syscacheobjects compatibility view
ms.assetid: 9b14f37c-b7f5-4f71-b070-cce89a83f69e
caps.latest.revision: 37
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: de76f70e43c7b8d4cc043be069c2b412bb03f69b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="syssyscacheobjects-transact-sql"></a>sys.syscacheobjects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene información sobre cómo se utiliza la caché.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**BucketID**|**int**|Identificador de depósito. El valor indica un intervalo de 0 a (tamaño de directorio -1). El tamaño de directorio es el de la tabla hash.|  
|**cacheobjtype**|**nvarchar(17)**|Tipo de objeto en caché:<br /><br /> Plan compilado<br /><br /> Plan ejecutable<br /><br /> Árbol de análisis<br /><br /> Cursor<br /><br /> Procedimiento almacenado extendido|  
|**ObjType**|**nvarchar (8)**|Tipo de objeto:<br /><br /> Procedimiento almacenado<br /><br /> Instrucción preparada<br /><br /> Consulta "ad hoc" ([!INCLUDE[tsql](../../includes/tsql-md.md)] enviado como eventos de lenguaje desde el **sqlcmd** o **osql** utilidades, en lugar de llamadas a procedimiento remoto)<br /><br /> ReplProc (procedimiento de replicación) <br /><br /> Desencadenador<br /><br /> Ver<br /><br /> Predeterminado<br /><br /> Tabla de usuario<br /><br /> Tabla del sistema<br /><br /> Comprobación<br /><br /> Regla|  
|**ObjID**|**int**|Una de las claves principales utilizadas para buscar un objeto en la caché. Éste es el objeto identificador almacena en **sysobjects** para objetos de base de datos (procedimientos, vistas, desencadenadores y así sucesivamente). Para los objetos de caché, como SQL preparada o ad hoc, **objid** es un valor generado internamente.|  
|**dbid**|**smallint**|Id. de la base de datos donde se ha compilado el objeto de caché.|  
|**dbidexec**|**smallint**|Id. de la base de datos desde la que se ejecuta la consulta.<br /><br /> Para la mayoría de los objetos, **dbidexec** tiene el mismo valor que **dbid**.<br /><br /> Para las vistas del sistema, **dbidexec** es el identificador de base de datos desde el que se ejecuta la consulta.<br /><br /> Para las consultas ad hoc, **dbidexec** es 0. Esto significa **dbidexec** tiene el mismo valor que **dbid**.|  
|**UID**|**smallint**|Indica el creador del plan para los planes de consulta ad hoc y los planes preparados.<br /><br /> -2 = El lote enviado no depende de la resolución implícita de nombre y puede compartirse entre usuarios distintos. Éste es el método preferido. Cualquier otro valor representa el Id. del usuario que envía la consulta en la base de datos.<br /><br /> Produce un desbordamiento o devuelve NULL si el número de usuarios y roles es superior a 32.767.|  
|**refCounts**|**int**|Número de otros objetos de caché que hacen referencia a este objeto de caché. La cuenta comienza en 1.|  
|**usecounts**|**int**|Número de veces que se ha usado este objeto de caché desde el comienzo.|  
|**pagesused**|**int**|Número de páginas consumidas por el objeto de caché.|  
|**setopts**|**int**|Valores de la opción SET que afectan a un plan compilado. Forman parte de la clave de caché. Los cambios en los valores de esta columna indican que los usuarios han modificado opciones SET. Estas opciones incluyen las siguientes:<br /><br /> **ANSI_PADDING**<br /><br /> **FORCEPLAN**<br /><br /> **CONCAT_NULL_YIELDS_NULL**<br /><br /> **ANSI_WARNINGS**<br /><br /> **ANSI_NULLS**<br /><br /> **QUOTED_IDENTIFIER**<br /><br /> **ANSI_NULL_DFLT_ON**<br /><br /> **ANSI_NULL_DFLT_OFF**|  
|**LangID**|**smallint**|Identificador de idioma. Es el Id. del idioma de la conexión que creó el objeto de caché.|  
|**dateformat**|**smallint**|Formato de fecha de la conexión que creó el objeto de caché.|  
|**status**|**int**|Indica si el objeto de caché es o no un plan de cursor. En la actualidad solo se utiliza el bit menos significativo.|  
|**lasttime**|**bigint**|Se conserva únicamente por compatibilidad con versiones anteriores. Siempre devuelve 0.|  
|**maxexectime específicos**|**bigint**|Se conserva únicamente por compatibilidad con versiones anteriores. Siempre devuelve 0.|  
|**avgexectime**|**bigint**|Se conserva únicamente por compatibilidad con versiones anteriores. Siempre devuelve 0.|  
|**lastreads**|**bigint**|Se conserva únicamente por compatibilidad con versiones anteriores. Siempre devuelve 0.|  
|**lastwrites**|**bigint**|Se conserva únicamente por compatibilidad con versiones anteriores. Siempre devuelve 0.|  
|**SqlBytes**|**int**|Longitud en bytes de la definición del procedimiento o el lote enviado.|  
|**sql**|**nvarchar(3900)**|Definición del módulo o los primeros 3900 caracteres del lote enviado.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  

