---
title: ISJSON (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISJSON
- ISJSON_TSQL
helpviewer_keywords:
- ISJSON function
- JSON, validating
ms.assetid: c836f3d3-3e17-44ae-92bf-f341918896c3
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9b641847387801097bce59e78cf75255cc7217be
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="isjson-transact-sql"></a>ISJSON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Comprueba si una cadena contiene JSON válido.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
ISJSON ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Cadena que se va a comprobar.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve 1 si la cadena contiene JSON válido; en caso contrario, devuelve 0. Devuelve null si *expresión* es null.  
  
 No se devuelven errores.  
  
## <a name="remarks"></a>Comentarios  
 **ISJSON** no comprueba la unicidad de las claves en el mismo nivel.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="example-1"></a>Ejemplo 1  
En el siguiente ejemplo se ejecuta un bloque de instrucciones condicionalmente si el valor del parámetro `@param` contiene JSON válido.  
  
```sql  
DECLARE @param <data type>
SET @param = <value>

IF (ISJSON(@param) > 0)  
BEGIN  
     -- Do something with the valid JSON value of @param.  
END
 
```  
  
### <a name="example-2"></a>Ejemplo 2  
En el ejemplo siguiente, se devuelven las filas en las que la columna `json_col` contiene JSON válido.  
  
```sql  
SELECT id, json_col
FROM tab1
WHERE ISJSON(json_col) > 0 
```  
  
## <a name="see-also"></a>Vea también  
 [Datos JSON &#40; SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  

