---
title: sp_fulltext_keymappings (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fulltext_keymappings_TSQL
- sp_fulltext_keymappings
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], key column
- sp_fulltext_keymappings
- full-text indexes [SQL Server], troubleshooting
ms.assetid: 2818fa42-072d-4664-a2f7-7ec363b51d81
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 872f3c474a790bdf7cbfabb4f8adf36ca0339724
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spfulltextkeymappings-transact-sql"></a>sp_fulltext_keymappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Devuelve las asignaciones entre los identificadores de documento (DocIds) y los valores de clave de texto completo. La columna DocId contiene valores para un **bigint** entero que se asigna a un determinado valor de clave de texto completo en una tabla indizada de texto completo. Los valores de DocId que cumplen una condición de búsqueda se pasan desde el motor de búsqueda de texto completo al motor de base de datos, donde se asignan a valores de clave de texto completo de la tabla base en la que se realizan las consultas. La columna de clave de texto completo es un índice único requerido en una columna de la tabla.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_fulltext_keymappings { table_id | table_id, docid | table_id, NULL, key }  
```  
  
#### <a name="parameters"></a>Parámetros  
 *table_id*  
 Identificador de objeto de la tabla con índice de texto completo. Si especifica un válido *table_id*, se devuelve un error. Para obtener información acerca de cómo obtener el identificador de objeto de una tabla, vea [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md).  
  
 *docid*  
 Identificador de documento interno (DocId) que corresponde al valor de clave. Un valor de *docid* no válido no devuelve ningún resultado.  
  
 *clave*  
 Valor de clave de texto completo de la tabla especificada. Un valor de *key* no válido no devuelve ningún resultado. Para obtener información acerca de los valores de clave de texto completo, vea [administrar índices de texto completo](http://msdn.microsoft.com/library/28ff17dc-172b-4ac4-853f-990b5dc02fd1).  
  
> [!IMPORTANT]  
>  Para obtener información sobre cómo usar uno, dos o tres parámetros, vea "Notas" más adelante en este tema.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Ninguno.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|DocId|**bigint**|Una columna de identificador de documento interno (DocId) que se corresponde con el valor de clave.|  
|Key|*|Valor de clave de texto completo de la tabla especificada.<br /><br /> Si no hay ninguna clave de texto completo en la tabla de asignación, se devuelve un conjunto de filas vacío.|  
  
 <sup>*</sup> El tipo de datos para la clave es igual que el tipo de datos de la columna de clave de texto completo en la tabla base.  
  
## <a name="permissions"></a>Permissions  
 Esta función es pública y no requiere permisos especiales.  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente, se describe el efecto de usar uno, dos o tres parámetros.  
  
|Esta lista de parámetros…|Tiene este resultado…|  
|--------------------------|----------------------|  
|*table_id*|Cuando se invoca con el *table_id* , sp_fulltext_keymappings devuelve todos los valores de clave de texto completo (Key) de la tabla base especificada, junto con el DocId que corresponde a cada clave. Esto incluye las claves pendientes de eliminación.<br /><br /> Esta función resulta útil para solucionar problemas de diversa índole. Es especialmente útil para ver el contenido del índice de texto completo cuando el tipo de datos de la clave de texto completo seleccionada no es Integer. Esto implica combinar los resultados de sp_fulltext_keymappings con los resultados de **sys.dm_fts_index_keywords_by_document**. Para obtener más información, consulte [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md).<br /><br /> Sin embargo, le recomendamos que, siempre que sea posible, ejecute sp_fulltext_keymappings con parámetros que especifiquen una clave de texto completo o un DocId específico. Esto es mucho más eficaz que devolver un mapa de claves completo, sobre todo si se trata de una tabla muy grande para la cual el costo por rendimiento de devolver el mapa de claves completo puede ser elevado.|  
|*table_id*, *docid*|Si solo el *table_id* y *docid* se especifican, *docid* debe ser nonNULL y especificar un DocId válido en la tabla especificada. Esta función resulta útil para aislar la clave de texto completo personalizada de la tabla base que corresponde al DocId de un determinado índice de texto completo.|  
|*table_id*, NULL, *clave*|Si hay tres parámetros, el segundo parámetro debe ser NULL, y *clave* debe ser nonNULL y especificar un valor de clave de texto completo válido de la tabla especificada. Esta función resulta útil para aislar el DocId que corresponde a una determinada clave de texto completo de la tabla base.|  
  
 Se devolverá un error en cualquiera de las condiciones siguientes:  
  
-   Especifique una válida *table_id*.  
  
-   La tabla no dispone de un índice de texto completo.  
  
-   Se ha encontrado NULL para un parámetro que debe ser nonNULL.  
  
## <a name="examples"></a>Ejemplos  
  
> [!NOTE]  
>  Los ejemplos de esta sección se usa la `Production.ProductReview` tabla de la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos de ejemplo. Puede crear este índice ejecutando el ejemplo proporcionado para el `ProductReview` tabla [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
### <a name="a-obtaining-all-the-key-and-docid-values"></a>A. Obtener todos los valores Key y DocId  
 En el ejemplo siguiente se usa un [DECLARE](../../t-sql/language-elements/declare-local-variable-transact-sql.md) instrucción para crear una variable local, `@table_id` y asignar el identificador de la `ProductReview` tabla como su valor. El ejemplo se ejecuta **sp_fulltext_keymappings** especificar `@table_id` para el *table_id* parámetro.  
  
> [!NOTE]  
>  Usar **sp_fulltext_keymappings** solamente con el *table_id* parámetro es apropiado para tablas pequeñas.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @table_id int = OBJECT_ID(N'Production.ProductReview');  
EXEC sp_fulltext_keymappings @table_id;  
GO  
  
```  
  
 En este ejemplo se devuelven todos los identificadores DocId y claves de texto completo de la tabla, del siguiente modo:  
  
||||  
|-|-|-|  
||`docid`|`key`|  
|`1`|`1`|`1`|  
|`2`|`2`|`2`|  
|`3`|`3`|`3`|  
|`4`|`4`|`4`|  
  
### <a name="b-obtaining-the-docid-value-for-a-specific-key-value"></a>B. Obtener el valor DocId para un valor Key específico  
 En el ejemplo siguiente se usa una instrucción DECLARE para crear una variable local, `@table_id`, y asignar el identificador de la tabla `ProductReview` como su valor. El ejemplo se ejecuta **sp_fulltext_keymappings** especificar `@table_id` para el *table_id* parámetro, NULL para la *docid* parámetro y 4 para el *clave* parámetro.  
  
> [!NOTE]  
>  Usar **sp_fulltext_keymappings** solamente con el *table_id* parámetro apropiado para tablas pequeñas.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @table_id int = OBJECT_ID(N'Production.ProductReview');  
EXEC sp_fulltext_keymappings @table_id, NULL, 4;  
GO  
  
```  
  
 En este ejemplo se devuelven los resultados siguientes.  
  
||||  
|-|-|-|  
||`docid`|`key`|  
|`4`|`4`|`4`|  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenan de búsqueda de texto completo y la búsqueda semántica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
