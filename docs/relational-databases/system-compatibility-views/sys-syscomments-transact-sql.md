---
title: Sys. syscomments (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 183fa2fc1a674ec1cc987c265f5a0d4c399e27cc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68010749"
---
# <a name="syssyscomments-transact-sql"></a>sys.syscomments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una entrada por cada vista, regla, valor predeterminado, desencadenador, restricción CHECK, restricción DEFAULT y procedimiento almacenado de la base de datos. La columna de **texto** contiene las instrucciones de definición de SQL originales.  
  
> [!IMPORTANT]  
>  
  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Se recomienda utilizar restricciones sys.sql_modules en su lugar. Para obtener más información, vea [Sys. sql_modules &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md).  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**sesión**|**int**|Identificador del objeto al que se aplica el texto.|  
|**número**|**smallint**|Número dentro del grupo de procedimientos, en el caso de procedimientos agrupados.<br /><br /> 0 = Las no son procedimientos.|  
|**colid**|**smallint**|Número de secuencia de fila para las definiciones de objeto de más de 4.000 caracteres.|  
|**estatus**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**ctext**|**varbinary (8000)**|Los bytes sin formato de la instrucción de definición de SQL.|  
|**texttype**|**smallint**|0 = Comentario proporcionado por el usuario<br /><br /> 1 = Comentario proporcionado por el sistema<br /><br /> 4 = Comentario cifrado|  
|**módulo**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cifra**|**bit**|Indica si se ofusca la definición de procedimiento.<br /><br /> 0 = no ofuscado<br /><br /> 1 = ofuscó<br /><br /> ** \* Importante \* \* ** Para ofuscar definiciones de procedimientos almacenados, utilice CREATE PROCEDURE con la palabra clave ENCRYPTION.|  
|**comprimido**|**bit**|Siempre devuelve 0. Ello indica que el procedimiento está comprimido.|  
|**negrita**|**nvarchar(4000)**|Texto real de la instrucción de definición de SQL.<br /><br /> La semántica de la expresión descodificada es equivalente al texto original; no obstante, no existen garantías sintácticas. Por ejemplo, los espacios en blanco se quitan de la expresión descodificada.<br /><br /> Esta [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]vista compatible con obtiene información de las estructuras [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] actuales y puede devolver más caracteres que la definición de **nvarchar (4000)** . **sp_help** devuelve **nvarchar (4000)** como tipo de datos de la columna de texto. Al trabajar con **syscomments** , considere la posibilidad de usar **nvarchar (Max)**. En el caso de los nuevos trabajos de desarrollo, no use **syscomments**.|  
  
## <a name="see-also"></a>Consulte también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
