---
title: PARÁMETROS (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- PARAMETERS_TSQL
- PARAMETERS
dev_langs:
- TSQL
helpviewer_keywords:
- PARAMETERS view
- INFORMATION_SCHEMA.PARAMETERS view
ms.assetid: 06ded0ca-7d21-4400-864a-b801e855b257
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 611a7545bfe13a2c9d835abee021c3117be846cd
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51657754"
---
# <a name="parameters-transact-sql"></a>PARAMETERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila por cada parámetro de una función o procedimiento almacenado definido por el usuario al que puede tener acceso el usuario actual de la base de datos actual. Para las funciones, esta vista también devuelve una fila con información del valor devuelto.  
  
 Para recuperar información de estas vistas, especifique el nombre completo de **INFORMATION_SCHEMA. *** view_name*.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**SPECIFIC_CATALOG**|**nvarchar (** 128 **)**|Nombre del catálogo de la rutina de la cual éste es un parámetro.|  
|**SPECIFIC_SCHEMA**|**nvarchar (** 128 **)**|Nombre del esquema de la rutina de la cual éste es un parámetro.<br /><br /> **\*\* Importante \* \***  no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. La única manera confiable de localizar el esquema de un objeto consiste en consultar la vista de catálogo sys.objects.|  
|**SPECIFIC_NAME**|**nvarchar (** 128 **)**|Nombre de la rutina de la cual éste es un parámetro.|  
|**ORDINAL_POSITION**|**int**|Posición ordinal del parámetro que empieza en 1. para el valor devuelto de una función, es un 0.|  
|**PARAMETER_MODE**|**nvarchar (** 10 **)**|Devuelve IN si es un parámetro de entrada, OUT si es un parámetro de salida e INOUT si es un parámetro de entrada/salida.|  
|**IS_RESULT**|**nvarchar (** 10 **)**|Devuelve YES si indica que el resultado de la rutina es una función. De lo contrario, devuelve NO.|  
|**AS_LOCATOR**|**nvarchar (** 10 **)**|Devuelve YES si se ha declarado como localizador. De lo contrario, devuelve NO.|  
|**NOMBRE DE PARÁMETRO**|**nvarchar (** 128 **)**|Nombre del parámetro. NULL si corresponde al valor devuelto de una función.|  
|**DATA_TYPE**|**nvarchar (** 128 **)**|Tipo de datos proporcionado por el sistema.|  
|**CAMPO CHARACTER_MAXIMUM_LENGTH**|**int**|Longitud máxima en caracteres de los tipos de datos binarios o de caracteres.<br /><br /> -1 para **xml** y datos de tipo de valor grande. De lo contrario, devuelve NULL.|  
|**CHARACTER_OCTET_LENGTH**|**int**|Longitud máxima, en bytes, de los tipos de datos binarios o de caracteres.<br /><br /> -1 para **xml** y datos de tipo de valor grande. De lo contrario, devuelve NULL.|  
|**COLLATION_CATALOG**|**nvarchar (** 128 **)**|Siempre devuelve NULL.|  
|**COLLATION_SCHEMA**|**nvarchar (** 128 **)**|Siempre devuelve NULL.|  
|**COLLATION_NAME**|**nvarchar (** 128 **)**|Nombre de la intercalación del parámetro. Si no es de uno de los tipos de carácter, devuelve NULL.|  
|**CHARACTER_SET_CATALOG**|**nvarchar (** 128 **)**|Nombre del catálogo del juego de caracteres del parámetro. Si no es de uno de los tipos de carácter, devuelve NULL.|  
|**CHARACTER_SET_SCHEMA**|**nvarchar (** 128 **)**|Siempre devuelve NULL.|  
|**CHARACTER_SET_NAME**|**nvarchar (** 128 **)**|Nombre del juego de caracteres del parámetro. Si no es de uno de los tipos de carácter, devuelve NULL.|  
|**CAMPO NUMERIC_PRECISION**|**tinyint**|Precisión de los datos numéricos aproximados, datos numéricos exactos, datos enteros o datos monetarios. De lo contrario, devuelve NULL.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Base de la precisión de datos numéricos aproximados, datos numéricos exactos, datos enteros o datos monetarios. De lo contrario, devuelve NULL.|  
|**NUMERIC_SCALE**|**tinyint**|Escala de datos numéricos aproximados, datos numéricos exactos, datos enteros o datos monetarios. De lo contrario, devuelve NULL.|  
|**DATETIME_PRECISION**|**smallint**|Precisión en fracciones de segundo si el tipo de parámetro es **datetime** o **smalldatetime**. De lo contrario, devuelve NULL.|  
|**INTERVAL_TYPE**|**nvarchar (** 30 **)**|NULL. Reservado para uso futuro.|  
|**INTERVAL_PRECISION**|**smallint**|NULL. Reservado para uso futuro.|  
|**USER_DEFINED_TYPE_CATALOG**|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|**USER_DEFINED_TYPE_SCHEMA**|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|**USER_DEFINED_TYPE_NAME**|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|**SCOPE_CATALOG**|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|**SCOPE_SCHEMA**|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|**SCOPE_NAME**|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de esquema de información &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
