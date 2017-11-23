---
title: JSON_QUERY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JSON_QUERY
- JSON_QUERY_TSQL
helpviewer_keywords:
- JSON, extracting
- JSON, querying
- JSON_QUERY function
ms.assetid: 1ab0d90f-19b6-4988-ab4f-22fdf28b7c79
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 310d85e26226cd54eff5d1c99e94b235348a90f7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="jsonquery-transact-sql"></a>JSON_QUERY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Extrae un objeto o una matriz de una cadena JSON.  
  
 Para extraer un valor escalar de una cadena JSON en lugar de un objeto o una matriz, vea [JSON_VALUE &#40; Transact-SQL &#41; ](../../t-sql/functions/json-value-transact-sql.md). Para obtener información sobre las diferencias entre **JSON_VALUE** y **JSON_QUERY**, consulte [comparar JSON_VALUE y JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
JSON_QUERY ( expression [ , path ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Expresión. Normalmente es el nombre de una variable o una columna que contiene texto JSON.  
  
 Si **JSON_QUERY** busca JSON que no es válido en *expresión* antes de encuentra el valor identificado por *ruta de acceso*, la función devuelve un error. Si **JSON_QUERY** no encuentra el valor identificado por *ruta de acceso*, examina todo el texto y devuelve un error si encuentra JSON que no es válida en cualquier lugar en *expresión*.  
  
 *ruta de acceso*  
 Una ruta de acceso JSON que especifica el objeto o la matriz para extraer.

En [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y en [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], puede proporcionar una variable como el valor de *ruta de acceso*.

La ruta de acceso JSON puede especificar el modo de lax o strict para el análisis. Si no se especifica el modo de análisis, modo lax es el valor predeterminado. Para obtener más información, consulte [expresiones de ruta de acceso JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  

El valor predeterminado de *ruta de acceso* es '$'. Como resultado, si no proporciona un valor para *ruta de acceso*, **JSON_QUERY** devuelve la entrada *expresión*.

Si el formato de *ruta de acceso* no es válida, **JSON_QUERY** devuelve un error.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un fragmento de JSON de tipo nvarchar (max). La intercalación del valor devuelto es la misma que la intercalación de la expresión de entrada.  
  
 Si el valor no es un objeto o una matriz:  
  
-   En el modo lax, **JSON_QUERY** devuelve null.  
  
-   En modo strict, **JSON_QUERY** devuelve un error.  
  
## <a name="remarks"></a>Comentarios  

### <a name="lax-mode-and-strict-mode"></a>Modo lax y modo strict

 Tenga en cuenta el siguiente texto JSON:  
  
```json  
{
    "info": {
        "type": 1,
        "address": {
            "town": "Bristol",
            "county": "Avon",
            "country": "England"
        },
        "tags": ["Sport", "Water polo"]
    },
    "type": "Basic"
} 
```  
  
 En la tabla siguiente se compara el comportamiento de **JSON_QUERY** en modo lax y en modo strict. Para obtener más información acerca de la especificación del modo de ruta de acceso opcional (lax o strict), consulte [expresiones de ruta de acceso JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Ruta de acceso|Valor devuelto en el modo lax|Valor devuelto en modo strict|Más información|  
|----------|------------------------------|---------------------------------|---------------|  
|$|Devuelve todo el texto JSON.|Devuelve todo el texto JSON.|N/A|  
|$. info.type|NULL|Error|No un objeto o matriz.<br /><br /> Use **JSON_VALUE** en su lugar.|  
|$. info.address.town|NULL|Error|No un objeto o matriz.<br /><br /> Use **JSON_VALUE** en su lugar.|  
|$.info." dirección"|N'{"ciudad": "Bristol", "provincia": "Asturias", "país": "Inglaterra"}'|N'{"ciudad": "Bristol", "provincia": "Asturias", "país": "Inglaterra"}'|N/A|  
|$. info.tags|N '["deporte", "Agua polo"]'|N '["deporte", "Agua polo"]'|N/A|  
|$. info.type[0]|NULL|Error|No es una matriz.|  
|$. info.none|NULL|Error|Propiedad no existe.|  

### <a name="using-jsonquery-with-for-json"></a>Uso de JSON_QUERY con FOR JSON

**JSON_QUERY** devuelve un fragmento de JSON válido. Como resultado, **FOR JSON** no caracteres de escape especiales en el **JSON_QUERY** valor devuelto.

Si va a devolver resultados con FOR JSON y, incluidos los datos que ya está en formato JSON (en una columna o como resultado de una expresión), ajustar los datos JSON con **JSON_QUERY** sin el *ruta de acceso* parámetro.

## <a name="examples"></a>Ejemplos  
  
### <a name="example-1"></a>Ejemplo 1  
 En el ejemplo siguiente se muestra cómo devolver un fragmento de JSON desde un `CustomFields` columna en resultados de la consulta.  
  
```sql  
SELECT PersonID,FullName,
 JSON_QUERY(CustomFields,'$.OtherLanguages') AS Languages
FROM Application.People
```  
  
### <a name="example-2"></a>Ejemplo 2  
En el ejemplo siguiente se muestra cómo incluir fragmentos JSON en la salida de la cláusula FOR JSON.  
  
```sql  
SELECT StockItemID, StockItemName,
         JSON_QUERY(Tags) as Tags,
         JSON_QUERY(CONCAT('["',ValidFrom,'","',ValidTo,'"]')) ValidityPeriod
FROM Warehouse.StockItems
FOR JSON PATH
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones de ruta de acceso JSON &#40; SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Datos JSON &#40; SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
