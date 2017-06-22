---
title: Expresiones de ruta de acceso JSON (SQL Server) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 01/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, path expressions
- path expressions (JSON)
ms.assetid: 25ea679c-84cc-4977-867c-2cbe9d192553
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 44bfd54aa494dd52174eeed8479e14a99d810af3
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="json-path-expressions-sql-server"></a>Expresiones de ruta de acceso JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Usar expresiones de ruta de acceso JSON para hacer referencia a las propiedades de objetos JSON.  
  
 Al llamar a las siguientes funciones, hay que proporcionar una expresión de ruta de acceso.  
  
-   Cuando se llama a **OPENJSON** para crear una vista relacional de los datos JSON. Para obtener más información, vea [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
-   Cuando se llama a **JSON_VALUE** para extraer un valor de texto JSON. Para obtener más información, vea [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
-   Cuando se llama a **JSON_QUERY** para extraer un objeto JSON o una matriz. Para obtener más información, vea [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
-   Cuando se llama a **JSON_MODIFY** para actualizar el valor de una propiedad en una cadena JSON. Para obtener más información, vea [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  

## <a name="parts-of-a-path-expression"></a>Partes de una expresión de ruta de acceso
 Una expresión de ruta de acceso tiene dos componentes.  
  
1.  Opcional [modo path](#PATHMODE), con un valor de **lax** o **estricta**.  
  
2.  La [ruta de acceso](#PATH) en sí.  

##  <a name="PATHMODE"></a> Path mode  
 Al principio de la expresión de ruta de acceso, puede optar por declarar el modo de la ruta de acceso con las palabras clave **lax** o **strict**. El valor predeterminado es **lax**.  
  
-   En **lax** modo, la función devuelve valores vacíos si la expresión de ruta de acceso contiene un error. Por ejemplo, si se solicita el valor **$.name**, y el texto JSON no contiene un **nombre** clave, la función devuelve null, pero no genera un error.  
  
-   En **estricta** modo, la función genera un error si la expresión de ruta de acceso contiene un error.  

La consulta siguiente especifica explícitamente `lax` modo en la expresión de ruta de acceso.

```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{ ... }'

SELECT * FROM OPENJSON(@json, N'lax $.info')
```  
  
##  <a name="PATH"></a> Path  
 Después de declarar (opcionalmente) el modo de ruta de acceso, se especifica la ruta de acceso.  
  
-   El signo de dólar (`$`) representa el elemento de contexto.  
  
-   La ruta de acceso de propiedad es un conjunto de pasos de ruta de acceso. Los pasos de ruta de acceso pueden contener los siguientes elementos y operadores.  
  
    -   Nombres de clave. Por ejemplo, `$.name` y `$."first name"`. Si el nombre de clave comienza por un signo de dólar o contiene caracteres especiales (como espacios), insértelo entre comillas.   
  
    -   Elementos de matriz. Por ejemplo, `$.product[3]`. Las matrices tienen una base cero.  
  
    -   El operador de punto (`.`) indica un miembro de un objeto. Por ejemplo, en `$.people[1].surname`, `surname` es un elemento secundario de `people`.
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos de esta sección hacen referencia al siguiente texto JSON.  
  
```json  
{
    "people": [{
        "name": "John",
        "surname": "Doe"
    }, {
        "name": "Jane",
        "surname": null,
        "active": true
    }]
}
```  
  
 En la siguiente tabla se muestran algunos ejemplos de expresiones de ruta de acceso.  
  
|Expresión de ruta de acceso|Valor|  
|---------------------|-----------|  
|$.people[0].name|John|  
|$.people[1]|{ "name": "Jane",  "surname": null, "active": true }|  
|$.people[1].surname|null|  
|$|{ "people": [ { "name": "John",  "surname": "Doe" },<br />   { "name": "Jane",  "surname": null, "active": true } ] }|  
  
## <a name="how-built-in-functions-handle-duplicate-paths"></a>Control de las rutas de acceso duplicadas por las funciones integradas  
 Si el texto JSON contiene propiedades duplicadas: por ejemplo, dos claves con el mismo nombre en el mismo nivel - el **JSON_VALUE** y **JSON_QUERY** funciones devuelven solo el primer valor que coincide con la ruta de acceso. Para analizar un objeto JSON que contiene las claves duplicadas y devolver todos los valores, utilice **OPENJSON**, tal y como se muestra en el ejemplo siguiente.  
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{"person":{"info":{"name":"John", "name":"Jack"}}}'

SELECT value
FROM OPENJSON(@json,'$.person.info') 
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Obtener más información sobre la compatibilidad integrada de JSON en SQL Server  
Para una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte el [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en la base de datos de SQL de Azure mediante el Administrador de programas de Microsoft Jovan Popovic.
  
## <a name="see-also"></a>Vea también  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
  

