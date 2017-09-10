---
title: STRING_AGG (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- STRING_AGG
- STRING_AGG_TSQL
helpviewer_keywords:
- STRING_AGG function
ms.assetid: 8860ef3f-142f-4cca-aa64-87a123e91206
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bf74698e9e61f456726b1e6a62126a8d78a09777
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="stringagg-transact-sql"></a>STRING_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

Concatena los valores de expresiones de cadena y coloca los valores de separador entre ellos. El separador no se agrega al final de la cadena.
 
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
STRING_AGG ( expression, separator ) [ <order_clause> ]

<order_clause> ::=   
    WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )   
```

## <a name="arguments"></a>Argumentos 

*separador*  
Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de `NVARCHAR` o `VARCHAR` tipo que se utiliza como separador para concatena cadenas. Puede ser literal o una variable. 

*expression*  
Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo. Las expresiones se convierten en `NVARCHAR` o `VARCHAR` tipos durante la concatenación. Tipos de cadena no se convierten en `NVARCHAR` tipo.


< order_clause >   
Opcionalmente, especificar el orden de resultados concatenados con `WITHIN GROUP` cláusula:
```
WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )
```   
< order_by_expression_list >   
 
  Una lista de no sea constante [expresiones](../../t-sql/language-elements/expressions-transact-sql.md) que se puede utilizar para ordenar los resultados. Solo un `order_by_expression` permitido por cada consulta. El criterio de ordenación predeterminado es ascendente.   
  

## <a name="return-types"></a>Tipos devueltos 

Tipo de valor devuelto es depende en el primer argumento (expresión). Si el argumento de entrada es de tipo string (`NVARCHAR`, `VARCHAR`), el tipo de resultado será igual que el tipo de entrada. En la tabla siguiente se enumera las conversiones automáticas:  

|Tipo de expresión de entrada |Resultado | 
|-------|-------|
|NVARCHAR(MAX) |NVARCHAR(MAX) |
|VARCHAR(MAX) |VARCHAR(MAX) |
|NVARCHAR (1.. 4000) |NVARCHAR (4000) |
|VARCHAR (1.. 8000) |VARCHAR(8000) |
|int, bigint, smallint, tinyint, numeric, float, real, bit, decimal, smallmoney, money, datetime, datetime2, |NVARCHAR (4000) |


## <a name="remarks"></a>Comentarios  
 
`STRING_AGG`agregado toma todas las expresiones de las filas y los concatena en una sola cadena. Valores de la expresión se convierte implícitamente en tipos de cadena y, a continuación, concatenar. La conversión implícita de cadenas sigue las reglas existentes para las conversiones de tipos de datos. Para obtener más información acerca de las conversiones de tipo de datos, vea [CAST y CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md). 

Si la expresión de entrada es de tipo `VARCHAR`, el separador no puede ser de tipo `NVARCHAR`. 

Se omiten los valores NULL y no se agrega el separador correspondiente. Para devolver un marcador de posición para valores null, utilice la `ISNULL` funcione como se muestra en el ejemplo B.

`STRING_AGG`está disponible en cualquier nivel de compatibilidad.


## <a name="examples"></a>Ejemplos 

### <a name="a-generate-list-of-names-separated-in-new-lines"></a>A. Generar la lista de nombres separados en las líneas nuevas 
En el ejemplo siguiente se genera una lista de nombres en una celda individual de resultados, separados por retornos de carro.
```tsql
SELECT STRING_AGG (FirstName, CHAR(13)) AS csv 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|csv | 
|--- |
|Syed <br />Catherine <br />Kim <br />Kim <br />Kim <br />Hazem <br />... | 

`NULL`valores que se encuentran en `name` celdas no se devuelven en el resultado.   
> [!NOTE]  
>  Si utiliza el Editor de consultas de Management Studio, el **resultados a cuadrícula** opción no puede implementar el retorno de carro. Cambie a **resultados a texto** ver el resultado establecido correctamente.   


### <a name="b-generate-list-of-names-separated-with-comma-without-null-values"></a>B. Generar la lista de nombres separados por coma sin valores NULL   
En el ejemplo siguiente se reemplaza los valores null con n '/' y devuelve los nombres separados por comas en una celda individual de resultados.  
```tsql
SELECT STRING_AGG ( ISNULL(FirstName,'N/A'), ',') AS csv 
FROM Person.Person; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
 

|CSV | 
|--- |
|John, n /, Mike, Peter, n /, n /, Alice, Bob |  


### <a name="c-generate-comma-separated-values"></a>C. Generar valores separados por comas 

```tsql   
SELECT 
STRING_AGG(CONCAT(FirstName, ' ', LastName, ' (', ModifiedDate, ')'), CHAR(13)) 
  AS names 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|nombres | 
|--- |
|Ken Sánchez (8 de febrero de 2003 12:00 A.M.) <br />Terri Duffy (24 de febrero de 2002 12:00 A.M.) <br />Roberto Tamburello (5 de diciembre de 2001 12:00 A.M.) <br />Rob Walters (29 de diciembre de 2001 12:00 A.M.) <br />... |

> [!NOTE]  
>  Si utiliza el Editor de consultas de Management Studio, el **resultados a cuadrícula** opción no puede implementar el retorno de carro. Cambie a **resultados a texto** ver el resultado establecido correctamente.   
 

### <a name="d-return-news-articles-with-related-tags"></a>D. Devolver artículos de noticias con etiquetas relacionadas 

Artículo y sus etiquetas se dividen en tablas diferentes. Programador desea devolver una fila por cada artículo con todas las etiquetas asociadas. Uso de consulta siguiente: 
```tsql
SELECT a.articleId, title, STRING_AGG (tag, ',') as tags 
FROM dbo.Article AS a       
LEFT JOIN dbo.ArticleTag AS t 
    ON a.ArticleId = t.ArticleId 
GROUP BY a.articleId, title;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|identificador de artículo |title |etiquetas |
|--- |--- |--- |
|172 |Sondeos indican elección Cerrar resultados |política, sondeos, Consejo de ciudad | 
|176 |Se esperaba autopista de nuevo reducir la congestión |NULL |
|177 |Dogs siguen siendo más popular que gatos |sondeos, animales| 

### <a name="e-generate-list-of-emails-per-towns"></a>E. Generar la lista de mensajes de correo electrónico por ciudades

La siguiente consulta busca las direcciones de correo electrónico de los empleados y los agrupa por ciudades: 
```tsql
SELECT town, STRING_AGG (email, ';') AS emails 
FROM dbo.Employee 
GROUP BY town; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|Ciudad |mensajes de correo electrónico |
|--- |--- |
|Seattle |syed0@adventure-works.com;catherine0@adventure-works.com;kim2@adventure-works.com |
|LA |sam1@adventure-works.com;hazem0@adventure-works.com |

Mensajes de correo electrónico se devuelven en los correos electrónicos de columna se puede utilizar directamente para enviar mensajes de correo electrónico al grupo de personas que trabajan en algunas ciudades determinados. 

### <a name="f-generate-a-sorted-list-of-emails-per-towns"></a>F. Generar una lista ordenada de mensajes de correo electrónico por ciudades   
   
Similar al ejemplo anterior, la siguiente consulta busca las direcciones de correo electrónico de los empleados, los agrupa por ciudad y ordena alfabéticamente los correos electrónicos:   
```tsql
SELECT town, 
    STRING_AGG (email, ';') WITHIN GROUP (ORDER BY email ASC) AS emails 
FROM dbo.Employee 
GROUP BY town; 
```
   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|Ciudad |mensajes de correo electrónico |
|--- |--- |
|Seattle |catherine0@adventure-works.com;kim2@adventure-works.com;syed0@adventure-works.com |
|LA |hazem0@adventure-works.com;sam1@adventure-works.com |


## <a name="see-also"></a>Vea también  

[Funciones de cadena (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  


