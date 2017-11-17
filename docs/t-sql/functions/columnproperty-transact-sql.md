---
title: COLUMNPROPERTY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLUMNPROPERTY
- COLUMNPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- parameters [SQL Server], properties
- COLUMNPROPERTY function
ms.assetid: 2408c264-6eca-4120-bb71-df043c7c2792
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: c6c2af8d231f03c40ee87d3468977c3b66cbeeb4
ms.contentlocale: es-es
ms.lasthandoff: 10/05/2017

---
# <a name="columnproperty-transact-sql"></a>COLUMNPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve información acerca de una columna o de un parámetro.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
COLUMNPROPERTY ( id , column , property )   
```  
  
## <a name="arguments"></a>Argumentos  
*id*  
Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) que contiene el identificador (ID) de la tabla o el procedimiento.
  
*columna*  
Es una expresión que contiene el nombre de la columna o del parámetro.
  
*propiedad*  
Es una expresión que contiene la información que se devuelve para *identificador*, y puede tener uno de los siguientes valores.
  
|Valor|Description|Valor devuelto|  
|---|---|---|
|**AllowsNull**|Permite valores null.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**ColumnId**|Valor de Id. de columna correspondiente a **sys.columns.column_id**.|Identificador de columna<br /><br /> **Nota:** al consultar varias columnas, pueden aparecer espacios en la secuencia de valores de Id. de columna.|  
|**FullTextTypeColumn**|La columna TYPE de la tabla que contiene la información de tipo de documento de la *columna*.|Id. de TYPE COLUMN de texto completo de la columna pasada como segundo parámetro de esta propiedad.|  
|**Es calculado**|La columna es una columna calculada.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**IsCursorType**|El parámetro de procedimiento es del tipo CURSOR.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**IsDeterministic**|La columna es determinista. Esta propiedad solo se aplica a columnas calculadas y columnas de vistas.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida. No es una columna calculada o una columna de vista.|  
|**IsFulltextIndexed**|La columna se ha registrado para la indización de texto completo.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**IsIdentity**|La columna utiliza la propiedad IDENTITY.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**IsIdNotForRepl**|La columna comprueba el valor IDENTITY_INSERT.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**IsIndexable**|La columna se puede indizar.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**IsOutParam**|El parámetro de procedimiento es un parámetro de salida.|1 = TRUE<br /><br /> 0 = FALSE o NULL = La entrada no es válida.|  
|**IsPrecise**|La columna es precisa. Esta propiedad solo se aplica a columnas deterministas.|1 = TRUE<br /><br /> 0 = FALSE o NULL = La entrada no es válida. No es una columna determinista|  
|**IsRowGuidCol**|La columna tiene el **uniqueidentifier** tipo de datos y se define con la propiedad ROWGUIDCOL.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**IsSystemVerified**|El [!INCLUDE[ssDE](../../includes/ssde-md.md)] puede comprobar las propiedades de determinismo y precisión de la columna. Esta propiedad solo se aplica a las columnas calculadas y columnas de vistas.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**IsXmlIndexable**|La columna XML se puede utilizar en un índice XML.|1 = TRUE<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**Precisión**|Longitud del tipo de datos de la columna o del parámetro.|Longitud del tipo de datos especificado para la columna<br /><br /> -1 = **xml** o tipos de valores grandes<br /><br /> NULL = La entrada no es válida.|  
|**Escala**|Escala del tipo de datos de la columna o del parámetro.|La escala<br /><br /> NULL = La entrada no es válida.|  
|**StatisticalSemantics**|La columna está habilitada para la indización semántica.|1 = TRUE<br /><br /> 0 = False|  
|**SystemDataAccess**|La columna se deriva de una función que tiene acceso a los datos de los catálogos del sistema o de las tablas virtuales del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta propiedad solo se aplica a las columnas calculadas y columnas de vistas.|1 = TRUE (indica acceso de solo lectura)<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**UserDataAccess**|La columna se deriva de una función que tiene acceso a los datos de las tablas de usuario, incluidas las vistas y tablas temporales, almacenadas en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta propiedad solo se aplica a las columnas calculadas y columnas de vistas.|1 = TRUE (indica acceso de solo lectura)<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**UsesAnsiTrim**|ANSI_PADDING se estableció en ON la primera vez que se creó la tabla. Esta propiedad solo se aplica a columnas o parámetros de tipo **char** o **varchar**.|1= TRUE <br /><br /> 0= FALSE <br /><br /> NULL = La entrada no es válida.|  
|**IsSparse**|La columna es una columna dispersa. Para obtener más información, vea [Usar columnas dispersas](../../relational-databases/tables/use-sparse-columns.md).|1= TRUE <br /><br /> 0= FALSE <br /><br /> NULL = La entrada no es válida.|  
|**IsColumnSet**|La columna es un conjunto de columnas. Para obtener más información, vea [Usar conjuntos de columnas](../../relational-databases/tables/use-column-sets.md).|1= TRUE <br /><br /> 0= FALSE <br /><br /> NULL = La entrada no es válida.|  
|**GeneratedAlwaysType**|Es el valor de columna generado por el sistema. Corresponde a **sys.columns.generated_always_type**|**Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = no generado siempre<br /><br /> 1 = generadas siempre como inicio de la fila<br /><br /> 2 – generado siempre como final de fila|  
|**IsHidden**|Es el valor de columna generado por el sistema. Corresponde a **sys.columns.is_hidden**|**Se aplica a**: desde [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = no ocultos<br /><br /> 1 = Hidden|  
  
## <a name="return-types"></a>Tipos de valor devuelto
 **int**  
  
## <a name="exceptions"></a>Excepciones  
Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto.
  
Un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como COLUMNPROPERTY, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).
  
## <a name="remarks"></a>Comentarios  
Cuando compruebe la propiedad determinista de una columna, compruebe primero si se trata de una columna calculada. **IsDeterministic** devuelve NULL para las columnas no calculadas. Las columnas calculadas se pueden especificar como columnas de índice.
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se devuelve la longitud de la columna `LastName`.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT COLUMNPROPERTY( OBJECT_ID('Person.Person'),'LastName','PRECISION')AS 'Column Length';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Column Length
-------------
50
```  
  
## <a name="see-also"></a>Vea también
[Funciones de metadatos &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[TYPEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)
  
  

