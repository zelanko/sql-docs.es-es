---
title: Las columnas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COLUMNS
- COLUMNS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS view
- INFORMATION_SCHEMA.COLUMNS view
ms.assetid: bbf7ac4a-7444-4351-a590-a9f71e0bc495
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 8294d3cabda817f68999fc80de45171b09451d4e
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39536195"
---
# <a name="columns-transact-sql"></a>COLUMNS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila por cada columna a la que puede tener acceso el usuario actual en la base de datos actual.  
  
 Para recuperar información de estas vistas, especifique el nombre completo de **INFORMATION_SCHEMA ***.** view_name *.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Calificador de tabla.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Nombre de esquema que contiene la tabla.<br /><br /> **\*\* Importante \* \* ** no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. La única manera confiable de localizar el esquema de un objeto consiste en consultar la vista de catálogo sys.objects.|  
|**TABLE_NAME**|**nvarchar (** 128 **)**|Nombre de la tabla.|  
|**COLUMN_NAME**|**nvarchar (** 128 **)**|Nombre de columna.|  
|**ORDINAL_POSITION**|**int**|Número de identificación de la columna.|  
|**COLUMN_DEFAULT**|**nvarchar (** 4000 **)**|Valor predeterminado de la columna.|  
|**IS_NULLABLE**|**varchar (** 3 **)**|Nulabilidad de la columna. Si esta columna permite valores NULL, esta columna devuelve YES. En caso contrario devuelve NO.|  
|**DATA_TYPE**|**nvarchar (** 128 **)**|Tipo de datos proporcionado por el sistema.|  
|**CAMPO CHARACTER_MAXIMUM_LENGTH**|**int**|Longitud máxima, en caracteres, de los datos binarios, de caracteres, o de texto e imagen.<br /><br /> -1 para **xml** y datos de tipo de valor grande. En caso contrario se devuelve NULL. Para obtener más información, vea [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
|**CHARACTER_OCTET_LENGTH**|**int**|Longitud máxima, en bytes, para datos binarios, datos de caracteres o datos de texto e imagen.<br /><br /> -1 para **xml** y datos de tipo de valor grande. En caso contrario se devuelve NULL.|  
|**CAMPO NUMERIC_PRECISION**|**tinyint**|Precisión de los datos numéricos aproximados, datos numéricos exactos, datos enteros o datos monetarios. En caso contrario se devuelve NULL.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Base de la precisión de datos numéricos aproximados, datos numéricos exactos, datos enteros o datos monetarios. En caso contrario se devuelve NULL.|  
|**NUMERIC_SCALE**|**int**|Escala de datos numéricos aproximados, datos numéricos exactos, datos enteros o datos monetarios. En caso contrario se devuelve NULL.|  
|**DATETIME_PRECISION**|**smallint**|Código de subtipo para **datetime** e ISO **intervalo** tipos de datos. Para los demás tipos de datos, se devuelve NULL.|  
|**CHARACTER_SET_CATALOG**|**nvarchar (** 128 **)**|Devuelve **maestro**. Esto indica a la base de datos en el que se encuentra, el juego de caracteres si la columna de datos de caracteres o **texto** tipo de datos. En caso contrario se devuelve NULL.|  
|**CHARACTER_SET_SCHEMA**|**nvarchar (** 128 **)**|Siempre devuelve NULL.|  
|**CHARACTER_SET_NAME**|**nvarchar (** 128 **)**|Devuelve el nombre único para el juego de caracteres si esta columna contiene datos de caracteres o **texto** tipo de datos. En caso contrario se devuelve NULL.|  
|**COLLATION_CATALOG**|**nvarchar (** 128 **)**|Siempre devuelve NULL.|  
|**COLLATION_SCHEMA**|**nvarchar (** 128 **)**|Siempre devuelve NULL.|  
|**COLLATION_NAME**|**nvarchar (** 128 **)**|Devuelve el nombre único para la intercalación si la columna de datos de caracteres o **texto** tipo de datos. En caso contrario se devuelve NULL.|  
|**DOMAIN_CATALOG**|**nvarchar (** 128 **)**|Si la columna es de un tipo de datos de alias, esta columna es el nombre de la base de datos en que se creó el tipo de datos definido por el usuario. En caso contrario se devuelve NULL.|  
|**DOMAIN_SCHEMA**|**nvarchar (** 128 **)**|Si la columna es de un tipo de datos definido por el usuario, devuelve el nombre del esquema del tipo de datos definido por el usuario. En caso contrario se devuelve NULL.<br /><br /> **\*\* Importante \* \* ** no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un tipo de datos. La única manera confiable de localizar el esquema de un tipo consiste en utilizar la función TYPEPROPERTY.|  
|**NOMBRE_DOMINIO**|**nvarchar (** 128 **)**|Si la columna es de un tipo de datos definido por el usuario, esta columna es el nombre del tipo de datos definido por el usuario. En caso contrario se devuelve NULL.|  
  
## <a name="remarks"></a>Notas  
 El **ORDINAL_POSITION** columna de la **INFORMATION_SCHEMA. COLUMNAS** vista no es compatible con el patrón de bits de las columnas devueltas por la función COLUMNS_UPDATED. Para obtener un patrón de bits que es compatible con COLUMNS_UPDATED, debe hacer referencia a la **ColumnID** propiedad de la función de sistema COLUMNPROPERTY al consultar el **INFORMATION_SCHEMA. COLUMNAS** vista. Por ejemplo:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TABLE_NAME, COLUMN_NAME, COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME), COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de esquema de información &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [Sys.syscharsets &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [COLUMNS_UPDATED &#40;Transact-SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)  
  
  
