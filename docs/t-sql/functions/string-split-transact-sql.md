---
title: STRING_SPLIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STRING_SPLIT
- STRING_SPLIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_SPLIT function
ms.assetid: 3273dbf3-0b4f-41e1-b97e-b4f67ad370b9
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 45e0dbf6fac0361a95aeedc3b47ba13ae82058d5
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/04/2018
ms.locfileid: "37787746"
---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Divide la expresión de caracteres usando el separador especificado.  
  
> [!NOTE]  
> La función **STRING_SPLIT** solo está disponible en el nivel de compatibilidad 130 y superior. Si el nivel de compatibilidad de la base de datos es inferior a 130, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no podrá encontrar ni ejecutar la función **STRING_SPLIT**. Para cambiar el nivel de compatibilidad de una base de datos, vea [Ver o cambiar el nivel de compatibilidad de una base de datos](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md).
> Tenga en cuenta que es posible que el nivel de compatibilidad 120 sea el valor predeterminado incluso en una [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] nueva.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
STRING_SPLIT ( string , separator )  
```  
  
## <a name="arguments"></a>Argumentos  
 *string*  
 Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo de carácter (por ejemplo **nvarchar**, **varchar**, **nchar** o **char**).  
  
 *separator*  
 Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de carácter único de cualquier tipo de caracteres (por ejemplo, **nvarchar(1)**, **varchar(1)**, **nchar(1)** o **char(1)**) que se usa como separador para cadenas concatenadas.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve una tabla de una sola columna con fragmentos. El nombre de la columna es **value**. Devuelve **nvarchar** si cualquiera de los argumentos de entrada es **nvarchar** o **nchar**. De lo contrario, devuelve **varchar**. La longitud del tipo de valor devuelto es igual a la longitud del argumento de cadena.  
  
## <a name="remarks"></a>Notas  
**STRING_SPLIT** toma una cadena que se debe dividir y el separador que se usará para dividirla. Devuelve una tabla de una sola columna con subcadenas. Por ejemplo, la siguiente instrucción `SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');`, en la que se usa el carácter de espacio como separador, devuelve la siguiente tabla de resultados:  
  
|value|  
|-----------|  
|Lorem|  
|ipsum|  
|dolor|  
|sit|  
|amet.|  
  
Si la cadena de entrada es **NULL**, la función con valores de tabla **STRING_SPLIT** devuelve una tabla vacía.  
  
**STRING_SPLIT** requiere el modo de compatibilidad 130 como mínimo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-split-comma-separated-value-string"></a>A. Dividir una cadena de valores separados por coma  
Se analiza una lista de valores separados por coma y se devuelven todos los tokens que no están vacíos:  
  
```sql  
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';  
```  
  
STRING_SPLIT devolverá una cadena vacía si no hay nada entre el separador. La condición "RTRIM(value) <>" quitará los tokens vacíos.  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>B. Dividir una cadena de valores separados por coma en una columna  
La tabla Product tiene una columna con una lista de etiquetas separadas por comas que se muestran en el siguiente ejemplo:  
  
|ProductId|Nombre|Etiquetas|  
|---------------|----------|----------|  
|1|Guantes|clothing,road,touring,bike|  
|2|Auriculares LL|bike|  
|3|HL Mountain Frame|bike,mountain|  
  
Con la siguiente consulta se transforma cada lista de etiquetas y las combina con la fila original:  
  
```sql  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|ProductId|Nombre|value|  
|---------------|----------|-----------|  
|1|Guantes|clothing|  
|1|Guantes|road|  
|1|Guantes|touring|  
|1|Guantes|bike|  
|2|Auriculares LL|bike|  
|3|HL Mountain Frame|bike|  
|3|HL Mountain Frame|mountain|  
  
### <a name="c-aggregation-by-values"></a>C. Agregación por valores  
Los usuarios deben crear un informe en el que se muestre el número de productos por etiqueta, ordenadas por número de productos, y filtrar solo las etiquetas con más de dos productos.  
  
```sql  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```  
  
### <a name="d-search-by-tag-value"></a>D. Buscar por el valor de tabla  
Los desarrolladores deben crear consultas que hallen artículos a partir de palabras clave. Pueden usar las siguientes consultas:  
  
Para encontrar productos con una sola etiqueta (clothing):  
  
```sql  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```  
  
Para encontrar productos con dos etiquetas especificadas (clothing y road):  
  
```sql  
  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road');  
```  
  
### <a name="e-find-rows-by-list-of-values"></a>E. Encontrar filas por la lista de valores  
Los desarrolladores deben crear una consulta que busque los artículos a partir de una lista de identificadores. Pueden usar la siguiente consulta:  
  
```sql  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')   
    ON value = ProductId;  
```  
  
Se trata de una forma de reemplazar el uso habitual de patrones poco recomendables, como la creación de una cadena SQL dinámica en el nivel de aplicación o [!INCLUDE[tsql](../../includes/tsql-md.md)], o usar el operador LIKE:  
  
```sql  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```  
  
## <a name="see-also"></a>Ver también  
[LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)     
[LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)     
[RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)    
[RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)     
[SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)     
[TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)     
[Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)      
  
  
