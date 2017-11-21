---
title: INDEXKEY_PROPERTY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INDEXKEY_PROPERTY_TSQL
- INDEXKEY_PROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- index keys [SQL Server]
- INDEXKEY_PROPERTY function
- viewing index keys
- displaying index keys
- keys [SQL Server], index
ms.assetid: 87c0c385-6b2d-4716-ac8c-a3ce6e8d89e9
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4d15a653fbc4954a37e5124a7a24436738ef5c1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="indexkeyproperty-transact-sql"></a>INDEXKEY_PROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca de la clave de índice. Devuelve NULL para los índices XML.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]En su lugar, use [sys.index_columns &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
INDEXKEY_PROPERTY ( object_ID ,index_ID ,key_ID ,property )  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_ID*  
 Es el número de identificación de objeto de la tabla o vista indizada. *object_ID* es **int**.  
  
 *index_id*  
 Es el número de identificación del índice. *index_id* es **int**.  
  
 *valor key_ID*  
 Es la posición de la columna de clave de índice. *valor key_ID* es **int**.  
  
 *propiedad*  
 Es el nombre de la propiedad cuya información se va a devolver. *propiedad* es una cadena de caracteres y puede ser uno de los valores siguientes.  
  
|Valor|Description|  
|-----------|-----------------|  
|**ColumnId**|Id. de columna en la *key_ID* posición del índice.|  
|**IsDescending**|Orden en el que se almacena la columna de índice.<br /><br /> 1 = Descendente ?0 = Ascendente|  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="exceptions"></a>Excepciones  
 Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto.  
  
 Un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como INDEXKEY_PROPERTY, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente, se devuelven ambas propiedades para el identificador de índice `1`, la columna de clave `1` de la tabla `Production.Location`.  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT   
    INDEXKEY_PROPERTY(OBJECT_ID('Production.Location', 'U'),  
        1,1,'ColumnId') AS [Column ID],  
    INDEXKEY_PROPERTY(OBJECT_ID('Production.Location', 'U'),  
        1,1,'IsDescending') AS [Asc or Desc order];  
```  
  
 El conjunto de resultados es:  
  
```  
Column ID   Asc or Desc order   
----------- -----------------   
1           0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también  
 [INDEX_COL &#40; Transact-SQL &#41;](../../t-sql/functions/index-col-transact-sql.md)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  

