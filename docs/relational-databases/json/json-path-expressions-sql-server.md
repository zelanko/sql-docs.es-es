---
description: Expresiones de ruta de acceso JSON (SQL Server)
title: Expresiones de ruta de acceso JSON
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, path expressions
- path expressions (JSON)
ms.assetid: 25ea679c-84cc-4977-867c-2cbe9d192553
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 558f11fdac7b8475054500cf5d002bfec107cb7f
ms.sourcegitcommit: 28fecbf61ae7b53405ca378e2f5f90badb1a296a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2020
ms.locfileid: "96595031"
---
# <a name="json-path-expressions-sql-server"></a>Expresiones de ruta de acceso JSON (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sqlserver2016-asdb.md)]

 Use expresiones de rutas de acceso JSON para hacer referencia a las propiedades de los objetos JSON.  
  
 Al llamar a las siguientes funciones, hay que proporcionar una expresión de ruta de acceso.  
  
-   Cuando se llama a **OPENJSON** para crear una vista relacional de los datos JSON. Para obtener más información, vea [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
-   Cuando se llama a **JSON_VALUE** para extraer un valor de texto JSON. Para obtener más información, vea [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
-   Cuando se llama a **JSON_QUERY** para extraer un objeto JSON o una matriz. Para obtener más información, vea [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
-   Cuando se llama a **JSON_MODIFY** para actualizar el valor de una propiedad en una cadena JSON. Para obtener más información, vea [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  

## <a name="parts-of-a-path-expression"></a>Partes de una expresión de ruta de acceso
 Una expresión de ruta de acceso tiene dos componentes.  
  
1.  El [modo de ruta de acceso](#PATHMODE) opcional, con un valor de **lax** o **strict**.  
  
2.  La [ruta de acceso](#PATH) en sí.  

##  <a name="path-mode"></a><a name="PATHMODE"></a> Path mode  
 Al principio de la expresión de ruta de acceso, puede optar por declarar el modo de la ruta de acceso con las palabras clave **lax** o **strict**. El valor predeterminado es **lax**.  
  
-   En el modo **lax**, las funciones devuelven valores vacíos si la expresión de ruta de acceso contiene un error. Por ejemplo, si se solicita el valor **$.name** y el texto JSON no contiene una clave **name**, la función devuelve NULL, pero no genera ningún error.  
  
-   En el modo **strict**, las funciones generan un error si la expresión de ruta de acceso contiene un error.  

La consulta siguiente especifica explícitamente el modo `lax` en la expresión de ruta de acceso.

```sql  
DECLARE @json NVARCHAR(MAX);
SET @json=N'{ ... }';

SELECT * FROM OPENJSON(@json, N'lax $.info');
```  
  
##  <a name="path"></a><a name="PATH"></a> Path  
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
  
|Expresión de ruta de acceso|Value|  
|---------------------|-----------|  
|$.people[0].name|John|  
|$.people[1]|{ "name": "Jane",  "surname": null, "active": true }|  
|$.people[1].surname|null|  
|$|{ "people": [ { "name": "John",  "surname": "Doe" },<br />   { "name": "Jane",  "surname": null, "active": true } ] }|  
  
## <a name="how-built-in-functions-handle-duplicate-paths"></a>Control de las rutas de acceso duplicadas por las funciones integradas  
 Si el texto JSON contiene propiedades duplicadas (por ejemplo, dos claves con el mismo nombre en el mismo nivel), las funciones **JSON_VALUE** y **JSON_QUERY** devuelven solo el primer valor que coincida con la ruta de acceso. Para analizar un objeto JSON que contiene claves duplicadas y devuelve todos los valores, use **OPENJSON**, como se muestra en el siguiente ejemplo.  
  
```sql  
DECLARE @json NVARCHAR(MAX);
SET @json=N'{"person":{"info":{"name":"John", "name":"Jack"}}}';

SELECT value
  FROM OPENJSON(@json,'$.person.info');
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Más información sobre JSON en SQL Server y Azure SQL Database  
  
### <a name="microsoft-videos"></a>Vídeos de Microsoft

Para obtener una introducción visual a la compatibilidad integrada de JSON en SQL Server y Azure SQL Database, vea los siguientes vídeos:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 y compatibilidad con JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso de JSON en SQL Server 2016 y Azure SQL Database)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON como puente entre los universos NoSQL y relacional)
  
## <a name="see-also"></a>Consulte también  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
  
