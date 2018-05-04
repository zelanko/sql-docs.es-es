---
title: DOMINIOS (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-information-schema-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DOMAINS_TSQL
- DOMAINS
dev_langs:
- TSQL
helpviewer_keywords:
- DOMAINS view
- INFORMATION_SCHEMA.DOMAINS view
ms.assetid: f0b734d5-816f-4b10-a60c-615931b515c2
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 931e5e6b59694d261a957d408a617bac984db28e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="domains-transact-sql"></a>DOMAINS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada tipo de datos de alias al que puede tener acceso el usuario actual en la base de datos actual.  
  
 Para recuperar información de estas vistas, especifique el nombre completo de **INFORMATION_SCHEMA. *** view_name*.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**DOMAIN_CATALOG**|**nvarchar (** 128 **)**|Base de datos donde existe el tipo de datos de alias.|  
|**DOMAIN_SCHEMA**|**nvarchar (** 128 **)**|Nombre del esquema que contiene el tipo de datos de alias.<br /><br /> **\*\* Importante \* \***  no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un tipo de datos. La única manera confiable de localizar el esquema de un tipo consiste en utilizar la función TYPEPROPERTY.|  
|**NOMBRE_DOMINIO**|**sysname**|Tipo de datos de alias.|  
|**DATA_TYPE**|**sysname**|Tipo de datos proporcionado por el sistema.|  
|**CAMPO CHARACTER_MAXIMUM_LENGTH**|**int**|Longitud máxima, en caracteres, de los datos binarios, de caracteres, o de texto e imagen.<br /><br /> -1 para **xml** y los datos de tipo de valor grande. En caso contrario se devuelve NULL. Para obtener más información, vea [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
|**CHARACTER_OCTET_LENGTH**|**int**|Longitud máxima, en bytes, para datos binarios, datos de caracteres o datos de texto e imagen.<br /><br /> -1 para **xml** y los datos de tipo de valor grande. En caso contrario se devuelve NULL.|  
|**COLLATION_CATALOG**|**varchar (** 6 **)**|Siempre devuelve NULL.|  
|**COLLATION_SCHEMA**|**varchar (** 3 **)**|Siempre devuelve NULL.|  
|**COLLATION_NAME**|**nvarchar (** 128 **)**|Devuelve el nombre único para el criterio de ordenación si la columna contiene datos de caracteres o **texto** tipo de datos. En caso contrario se devuelve NULL.|  
|**CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|Devuelve **principal**. Esto indica la base de datos en el que se encuentra, el juego de caracteres si la columna contiene datos de caracteres o **texto** tipo de datos. En caso contrario se devuelve NULL.|  
|**CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|Siempre devuelve NULL.|  
|**CHARACTER_SET_NAME**|**nvarchar (** 128 **)**|Devuelve el nombre único para el juego de caracteres si esta columna contiene datos de caracteres o **texto** tipo de datos. En caso contrario se devuelve NULL.|  
|**CAMPO NUMERIC_PRECISION**|**tinyint**|Precisión de los datos numéricos aproximados, datos numéricos exactos, datos enteros o datos monetarios. En caso contrario se devuelve NULL.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Base de la precisión de datos numéricos aproximados, datos numéricos exactos, datos enteros o datos monetarios. En caso contrario se devuelve NULL.|  
|**NUMERIC_SCALE**|**tinyint**|Escala de datos numéricos aproximados, datos numéricos exactos, datos enteros o datos monetarios. En caso contrario se devuelve NULL.|  
|**DATETIME_PRECISION**|**smallint**|Código de subtipo para **datetime** e ISO **intervalo** tipo de datos. Para otros tipos de datos, esta columna devuelve un valor NULL.|  
|**DOMAIN_DEFAULT**|**nvarchar (** 4000 **)**|Texto real de la instrucción de definición de [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de esquema de información &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [Sys.syscharsets &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
