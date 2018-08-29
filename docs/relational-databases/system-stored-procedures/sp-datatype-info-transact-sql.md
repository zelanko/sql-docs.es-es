---
title: sp_datatype_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/25/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_datatype_info_TSQL
- sp_datatype_info
dev_langs:
- TSQL
helpviewer_keywords:
- sp_datatype_info
ms.assetid: 045f3b5d-6bb7-4748-8b4c-8deb4bc44147
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aa2ad0da3b651660674dc1b4d5d2e82531fc547a
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43033307"
---
# <a name="spdatatypeinfo-transact-sql"></a>sp_datatype_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Devuelve información acerca de los tipos de datos que admite el entorno actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_datatype_info [ [ @data_type = ] data_type ]   
     [ , [ @ODBCVer = ] odbc_version ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@data_type=** ] *data_type*  
 Es el número de código del tipo de datos especificado. Para obtener una lista de todos los tipos de datos, omita este parámetro. *data_type* es **int**, su valor predeterminado es 0.  
  
 [  **@ODBCVer=** ] *odbc_version*  
 Es la versión de ODBC que se utiliza. *odbc_version* es **tinyint**, con el valor predeterminado es 2.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|TYPE_NAME|**sysname**|Tipo de datos dependiente del DBMS.|  
|DATA_TYPE|**smallint**|Código para el tipo de ODBC al que se asignan todas las columnas de este tipo.|  
|PRECISION|**int**|Precisión máxima del tipo de datos en el origen de datos. Se devuelve NULL para los tipos de datos a los que no se puede aplicar un parámetro de precisión. El valor devuelto para la columna PRECISION está expresado en base 10.|  
|LITERAL_PREFIX|**varchar (** 32 **)**|Carácter o caracteres utilizados antes de una constante. Por ejemplo, una comilla simple (**'**) para tipos de carácter y 0 x para el archivo binario.|  
|LITERAL_SUFFIX|**varchar (** 32 **)**|Carácter o caracteres utilizados para terminar una constante. Por ejemplo, una comilla simple (**'**) para tipos de caracteres y sin comillas binario.|  
|CREATE_PARAMS|**varchar (** 32 **)**|Descripción de los parámetros de creación para este tipo de datos. Por ejemplo, **decimal** es "precisión, escala", **float** es NULL, y **varchar** es "max_length".|  
|NULLABLE|**smallint**|Especifica la nulabilidad.<br /><br /> 1 = Permite valores NULL.<br /><br /> 0 = No permite valores NULL.|  
|CASE_SENSITIVE|**smallint**|Especifica si deben distinguirse mayúsculas y minúsculas.<br /><br /> 1 = Todas las columnas de este tipo distinguen mayúsculas y minúsculas (para intercalaciones).<br /><br /> 0 = Las columnas de este tipo no distinguen mayúsculas y minúsculas.|  
|SEARCHABLE|**smallint**|Especifica la capacidad de búsqueda del tipo de columna:<br /><br /> 1 = No se puede buscar.<br /><br /> 2 = Se puede buscar con LIKE.<br /><br /> 3 = Se puede buscar con WHERE.<br /><br /> 4 = Se puede buscar con WHERE o LIKE.|  
|UNSIGNED_ATTRIBUTE|**smallint**|Especifica el signo del tipo de datos.<br /><br /> 1 = Tipo de datos sin signo.<br /><br /> 0 = Tipo de datos con signo.|  
|MONEY|**smallint**|Especifica el **dinero** tipo de datos.<br /><br /> 1 = **dinero** tipo de datos.<br /><br /> 0 = no un **dinero** tipo de datos.|  
|AUTO_INCREMENT|**smallint**|Especifica el incremento automático.<br /><br /> 1 = Incremento automático.<br /><br /> 0 = Sin incremento automático.<br /><br /> NULL = Atributo no aplicable.<br /><br /> Una aplicación puede insertar valores en una columna que tenga este atributo, pero no puede actualizar los valores de la columna. Con la excepción de la **bit** tipo de datos, AUTO_INCREMENT solo es válida para los tipos de datos que pertenecen a la exacto o numérico aproximado numérico categorías de tipos de datos.|  
|LOCAL_TYPE_NAME|**sysname**|Versión traducida del nombre del tipo de datos, dependiente del origen de datos. Por ejemplo, DECIMAL es DECIMALE en francés. Se devuelve NULL si el origen de datos no admite un nombre traducido.|  
|MINIMUM_SCALE|**smallint**|Escala mínima del tipo de datos en el origen de datos. Si un tipo de datos tiene una escala fija, las columnas MINIMUM_SCALE y MAXIMUM_SCALE contienen este valor. Se devuelve NULL cuando no se puede aplicar la escala.|  
|MAXIMUM_SCALE|**smallint**|Escala máxima del tipo de datos en el origen de datos. Si la escala máxima no está definida por separado en el origen de datos, sino que se define igual que la precisión máxima, esta columna contendrá el mismo valor que la columna PRECISION.|  
|SQL_DATA_TYPE|**smallint**|Valor del tipo de datos SQL tal como aparece en el campo TYPE del descriptor. Esta columna es igual que la columna DATA_TYPE, salvo por el **datetime** y ANSI **intervalo** tipos de datos. Este campo siempre devuelve un valor.|  
|SQL_DATETIME_SUB|**smallint**|**fecha y hora** o ANSI **intervalo** subcódigo si el valor de SQL_DATA_TYPE es SQL_DATETIME o SQL_INTERVAL. Para tipos de datos distinto **datetime** y ANSI **intervalo**, este campo es NULL.|  
|NUM_PREC_RADIX|**int**|Número de bits o dígitos para calcular el número máximo que puede tener una columna. Si el tipo de datos es numérico aproximado, esta columna contendrá el valor 2 para indicar varios bits. Para tipos numéricos exactos, esta columna contiene el valor 10 que indica varias cifras decimales. De lo contrario, esta columna es NULL. Mediante la combinación de la precisión con la base, la aplicación puede calcular el número máximo que puede tener la columna.|  
|INTERVAL_PRECISION|**smallint**|Valor de intervalo inicial precisión si *data_type* es **intervalo**; de lo contrario, NULL.|  
|USERTYPE|**smallint**|**usertype** valor de la tabla systypes.|  
  
## <a name="remarks"></a>Notas  
 sp_datatype_info es equivalente a SQLGetTypeInfo en ODBC. Los resultados devueltos se ordenan por DATA_TYPE y, a continuación, por la proximidad de la asignación de los tipos de datos a los tipos de datos de ODBC SQL correspondientes.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol public.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se recupera información de la **sysname** y **nvarchar** tipos de datos especificando el *data_type* valor de `-9`.  
  
```  
USE master;  
GO  
EXEC sp_datatype_info -9;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
