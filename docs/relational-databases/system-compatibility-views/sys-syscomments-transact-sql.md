---
title: Sys.syscomments (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.syscomments_TSQL
- syscomments
- syscomments_TSQL
- sys.syscomments
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syscomments compatibility view
- syscomments system table
ms.assetid: 767dd410-6bc9-4c4a-ab0f-6d2cf6163426
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9a49d0a12cbf6e8f0c07cf6913786a0b437f1d0a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="syssyscomments-transact-sql"></a>sys.syscomments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una entrada por cada vista, regla, valor predeterminado, desencadenador, restricción CHECK, restricción DEFAULT y procedimiento almacenado de la base de datos. El **texto** columna contiene las instrucciones de definición de SQL originales.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Se recomienda que utilice en su lugar sys.sql_modules. Para obtener más información, consulte [sys.sql_modules &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md).  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identificador del objeto al que se aplica el texto.|  
|**number**|**smallint**|Número dentro del grupo de procedimientos, en el caso de procedimientos agrupados.<br /><br /> 0 = Las no son procedimientos.|  
|**colid**|**smallint**|Número de secuencia de fila para las definiciones de objeto de más de 4.000 caracteres.|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**ctext**|**varbinary(8000)**|Los bytes sin formato de la instrucción de definición de SQL.|  
|**texttype**|**smallint**|0 = Comentario proporcionado por el usuario<br /><br /> 1 = Comentario proporcionado por el sistema<br /><br /> 4 = Comentario cifrado|  
|**idioma**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**encrypted**|**bit**|Indica si se ofusca la definición de procedimiento.<br /><br /> 0 = no ofuscado<br /><br /> 1 = ofuscó<br /><br /> **\*\*Importante \* \***  para ofuscar las definiciones de procedimientos almacenados, utilice CREATE PROCEDURE con la palabra clave de cifrado.|  
|**compressed**|**bit**|Siempre devuelve 0. Ello indica que el procedimiento está comprimido.|  
|**texto**|**nvarchar(4000)**|Texto real de la instrucción de definición de SQL.<br /><br /> La semántica de la expresión descodificada es equivalente al texto original; no obstante, no existen garantías sintácticas. Por ejemplo, los espacios en blanco se quitan de la expresión descodificada.<br /><br /> Esto [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]-vista compatible obtiene información actual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de estructuras y puede devolver más caracteres que el **nvarchar (4000)** definición. **sp_help** devuelve **nvarchar (4000)** como el tipo de datos de la columna de texto. Cuando se trabaja con **syscomments** considere el uso de **nvarchar (max)**. Para los nuevos trabajos de desarrollo, no use **syscomments**.|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
