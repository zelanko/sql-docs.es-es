---
title: STRING_SPLIT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
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
- STRING_SPLIT
- STRING_SPLIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_SPLIT function
ms.assetid: 3273dbf3-0b4f-41e1-b97e-b4f67ad370b9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 00debf90f1b79a0e38cb883f31479ae5731f40d3
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Divide la expresión de caracteres utilizando el separador especificado.  
  
> [!NOTE]  
>  El **STRING_SPLIT** función está disponible sólo en el nivel de compatibilidad 130. Si el nivel de compatibilidad de base de datos es inferior a 130, SQL Server no podrá encontrar ni ejecutar **STRING_SPLIT** (función). Puede cambiar un nivel de compatibilidad de la base de datos mediante el comando siguiente:  
> ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130  
>   
>  Tenga en cuenta que el nivel de compatibilidad 120 podría ser predeterminada incluso en las nuevas bases de datos de SQL Azure.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
STRING_SPLIT ( string , separator )  
```  
  
## <a name="arguments"></a>Argumentos  
 *string*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo de carácter (es decir, **nvarchar**, **varchar**, **nchar** o **char**).  
  
 *separator*  
 Es un carácter único [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo de caracteres (por ejemplo, **nvarchar(1)**, **varchar (1)**, **nchar (1)** o  **Char (1)**) que se utiliza como separador para cadenas concatenadas.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve una tabla de una sola columna con fragmentos. El nombre de la columna es **valor**. Devuelve **nvarchar** si cualquiera de los argumentos de entrada son **nvarchar** o **nchar**. De lo contrario devuelve **varchar**. La longitud del tipo de valor devuelto es igual que la longitud del argumento de cadena.  
  
## <a name="remarks"></a>Comentarios  
 **STRING_SPLIT** toma una cadena que se debe dividir y el separador que se utilizará para dividir la cadena. Devuelve una tabla de una sola columna con subcadenas. Por ejemplo, la siguiente instrucción `SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');` con el carácter de espacio como separador, se devuelven después de la tabla de resultados:  
  
|value|  
|-----------|  
|Lorem|  
|ipsum|  
|dolor|  
|sit|  
|AME.|  
  
 Si la cadena de entrada es **NULL**, **STRING_SPLIT** función con valores de tabla devuelve una tabla vacía.  
  
 **STRING_SPLIT** requiere al menos el modo de compatibilidad 130.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-split-comma-separated-value-string"></a>A. Separada por comas de división de cadena del valor  
 Analizar una lista separada por comas de valores y devuelven todos los tokens no está vacío:  
  
```  
  
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';  
  
```  
  
 STRING_SPLIT devolverá una cadena vacía si no hay nada entre separador. Condición RTRIM(value) <> '' quitará tokens vacíos.  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>B. Separada por comas de división de cadena del valor de una columna  
 Tabla Product tiene una columna con lista separadas por comas de etiquetas que se muestra en el ejemplo siguiente:  
  
|productId|Nombre|Etiquetas|  
|---------------|----------|----------|  
|1|Guantes un dedo completo|ropa, road, touring bike|  
|2|Los auriculares con LL|bicicleta|  
|3|HL Mountain Frame|Bike, mountain|  
  
 La consulta siguiente transforma cada lista de etiquetas y los combina con la fila original:  
  
```  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|productId|Nombre|value|  
|---------------|----------|-----------|  
|1|Guantes un dedo completo|ropa|  
|1|Guantes un dedo completo|carretera|  
|1|Guantes un dedo completo|Touring|  
|1|Guantes un dedo completo|bicicleta|  
|2|Los auriculares con LL|bicicleta|  
|3|HL Mountain Frame|bicicleta|  
|3|HL Mountain Frame|montaña|  
  
### <a name="c-aggregation-by-values"></a>C. Agregación por valores  
 Los usuarios deben crear un informe que muestra el número de productos por cada etiqueta, ordenadas por número de productos y para filtrar solo las etiquetas con más de 2 productos.  
  
```  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```  
  
### <a name="d-search-by-tag-value"></a>D. Buscar por su valor de etiqueta  
 Los programadores deben crear consultas que busquen artículos por palabras clave. Puede usar los siguientes consultas:  
  
 Para buscar los productos con una sola etiqueta (ropa):  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```  
  
 Buscar productos con dos etiquetas especificados (ropa y carretera):  
  
```  
  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road');  
```  
  
### <a name="e-find-rows-by-list-of-values"></a>E. Buscar filas por lista de valores  
 Los desarrolladores deben crear una consulta que busca artículos mediante una lista de identificadores. Puede usar la consulta siguiente:  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')   
    ON value = ProductId;  
```  
  
 Se trata de reemplazo para antipatrón comunes como la creación de una cadena SQL dinámica de nivel de aplicación o [!INCLUDE[tsql](../../includes/tsql-md.md)], o mediante LIKE (operador):  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```  
  
## <a name="see-also"></a>Vea también  
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  
