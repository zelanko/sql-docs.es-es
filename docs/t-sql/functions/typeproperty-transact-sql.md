---
title: TYPEPROPERTY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TYPEPROPERTY
- TYPEPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], data types
- data types [SQL Server], status information
- TYPEPROPERTY function
ms.assetid: bc311c80-bac5-46ab-a5c8-68b1c6bbf24a
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 8608de51a13d2bc0109b9874b30749b10b65eaea
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="typeproperty-transact-sql"></a>TYPEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información acerca de un tipo de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
TYPEPROPERTY (type , property)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Tipo*  
 Es el nombre del tipo de datos.  
  
 *propiedad*  
 Es el tipo de información que se devuelve del tipo de datos. *propiedad* puede ser uno de los siguientes valores.  
  
|Propiedad|Description|Valor devuelto|  
|--------------|-----------------|--------------------|  
|**AllowsNull**|El tipo de datos permite valores nulos.|1 = True<br /><br /> 0 = False<br /><br /> NULL = No se encuentra el tipo de datos.|  
|**OwnerId**|Propietario del tipo.<br /><br /> Nota: El propietario del esquema no es necesariamente el propietario del tipo.|NonNULL = El Id. de usuario de la base de datos del propietario del tipo.<br /><br /> NULL = Tipo no compatible o Id. de tipo no válido.|  
|**Precisión**|Precisión del tipo de datos.|El número de dígitos o caracteres.<br /><br /> -1 = **xml** o tipo de datos de valores grandes<br /><br /> NULL = No se encuentra el tipo de datos.|  
|**Escala**|Escala del tipo de datos.|El número de decimales del tipo de datos.<br /><br /> NULL = no es de tipo de datos **numérico** o no se encuentra.|  
|**UsesAnsiTrim**|La configuración del relleno ANSI era ON cuando se creó el tipo de datos.|1 = True<br /><br /> 0 = False<br /><br /> NULL = No se encuentra el tipo de datos o no es un tipo de datos de cadena o binario.|  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="exceptions"></a>Excepciones  
 Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como TYPEPROPERTY, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-identifying-the-owner-of-a-data-type"></a>A. Identificar el propietario de un tipo de datos  
 En el ejemplo siguiente se devuelve el propietario de un tipo de datos.  
  
```  
SELECT TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId') AS owner_id, name, system_type_id, user_type_id, schema_id  
FROM sys.types;  
```  
  
### <a name="b-returning-the-precision-of-the-tinyint-data-type"></a>B. Devolver la precisión del tipo de datos tinyint  
 En el siguiente ejemplo se devuelve la precisión o el número de dígitos del tipo de datos `tinyint`.  
  
```  
SELECT TYPEPROPERTY( 'tinyint', 'PRECISION');  
```  
  
## <a name="see-also"></a>Vea también  
 [TYPE_ID &#40; Transact-SQL &#41;](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPE_NAME &#40; Transact-SQL &#41;](../../t-sql/functions/type-name-transact-sql.md)   
 [COLUMNPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [Funciones de metadatos &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [Sys.Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  


