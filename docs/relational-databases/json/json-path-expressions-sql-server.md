---
title: "Expresiones de ruta de acceso JSON (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/23/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "JSON, expresiones de ruta de acceso"
  - "expresiones de ruta de acceso (JSON)"
ms.assetid: 25ea679c-84cc-4977-867c-2cbe9d192553
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# Expresiones de ruta de acceso JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Use rutas de acceso JSON para hacer referencia a las propiedades de los objetos JSON. Las rutas de acceso JSON emplean una sintaxis similar a la de Javascript.  
  
 Al llamar a las siguientes funciones, hay que proporcionar una expresión de ruta de acceso.  
  
-   Cuando se llama a **OPENJSON** para crear una vista relacional de los datos JSON. Para obtener más información, vea [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
-   Cuando se llama a **JSON_VALUE** para extraer un valor de texto JSON. Para obtener más información, vea [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
-   Cuando se llama a **JSON_QUERY** para extraer un objeto JSON o una matriz. Para obtener más información, vea [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
-   Cuando se llama a **JSON_MODIFY** para actualizar el valor de una propiedad en una cadena JSON. Para obtener más información, vea [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  
  
 Una expresión de ruta de acceso tiene dos componentes.  
  
1.  El [modo de ruta de acceso](#PATHMODE)(lax o strict), que es opcional.  
  
2.  La [ruta de acceso](#PATH) en sí.  
  
##  <a name="PATHMODE"></a> modo de ruta de acceso  
 Al principio de la expresión de ruta de acceso, puede optar por declarar el modo de la ruta de acceso con las palabras clave **lax** o **strict**. El valor predeterminado es **lax**.  
  
-   En el modo **lax** , las funciones devuelven valores vacíos si la expresión de ruta de acceso contiene un error. Por ejemplo, si se solicita el valor **$.name**y el texto JSON no contiene una clave **name** , la función devuelve NULL.  
  
-   En el modo **strict** , las funciones generan un error si la expresión de ruta de acceso contiene un error.  
  
##  <a name="PATH"></a> ruta de acceso  
 Después de declarar (opcionalmente) el modo de ruta de acceso, se especifica la ruta de acceso.  
  
-   El signo de dólar ($) es el elemento de contexto.  
  
-   La ruta de acceso de propiedad es un conjunto de pasos de ruta de acceso. Los pasos de ruta de acceso pueden contener los siguientes elementos y operadores.  
  
    -   Nombres de clave. Si el nombre de clave comienza por un signo de dólar o contiene caracteres especiales (como espacios), insértelo entre comillas. Por ejemplo, `$.name` y `$."first name"`.  
  
    -   Elementos de matriz. Por ejemplo, `$.product[3]`. Las matrices tienen una base cero.  
  
    -   El operador de punto (.) señala un miembro de un objeto.  
  
## Ejemplos  
 Los ejemplos de esta sección hacen referencia al siguiente texto JSON.  
  
```json  
{ "people":  
  [  
    { "name": "John", "surname": "Doe" },  
    { "name": "Jane", "surname": null, "active": true }  
  ]  
}  
```  
  
 En la siguiente tabla se muestran algunos ejemplos de expresiones de ruta de acceso.  
  
|Expresión de ruta de acceso|Valor|  
|---------------------|-----------|  
|$.people[0].name|John|  
|$.people[1]|{ "name": "Jane",  "surname": null, "active": true }|  
|$.people[1].surname|null|  
|$|{ "people": [ { "name": "John",  "surname": "Doe" },<br />   { "name": "Jane",  "surname": null, "active": true } ] }|  
  
## Cómo tratar las rutas de acceso duplicadas  
 Si el texto JSON contiene propiedades duplicadas (por ejemplo, dos claves con el mismo nombre en el mismo nivel), las funciones JSON_VALUE y JSON_QUERY devuelven el primer valor que coincida con la ruta de acceso. Para analizar un objeto JSON que contiene claves duplicadas, use OPENJSON, como se muestra en el siguiente ejemplo.  
  
```tsql  
DECLARE @json NVARCHAR(MAX) = N'{"person":{"info":{"name":"John", "name":"Jack"}}}'  
  
SELECT value FROM OPENJSON(@json, '$.person.info')  
```  
  
## Vea también  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
  