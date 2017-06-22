---
title: "Indexación de datos JSON | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, indexing JSON data
- indexing JSON data
ms.assetid: ced241e1-ff09-4d6e-9f04-a594a9d2f25e
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 3ed7a51b28d2b17b3239f971d0f4f684bec145cd
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="index-json-data"></a>Indexación de datos JSON
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

En SQL Server 2016, JSON no es un tipo de datos integrado y SQL Server no tiene índices personalizados JSON. Sin embargo, puede optimizar las consultas en documentos JSON, mediante índices estándar. 

Índices de base de datos mejoran el rendimiento de las operaciones de filtro y ordenación. Sin ellos, SQL Server debe realizar un examen completo de la tabla cada vez que realice consultas de datos.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>Indexación de propiedades JSON mediante columnas calculadas  
Al almacenar datos JSON en SQL Server, normalmente querrá filtrar u ordenar resultados de la consulta por uno o varios *propiedades* de los documentos JSON.  

### <a name="example"></a>Ejemplo 
En este ejemplo, suponga que AdventureWorks `SalesOrderHeader` tabla tiene un `Info` columna que contiene diversa información en formato JSON sobre pedidos de venta. Por ejemplo, contiene información sobre clientes, vendedores, direcciones de envío y facturación y así sucesivamente. Desea usar los valores de la `Info` columna para filtrar los pedidos de ventas para un cliente.

### <a name="query-to-optimize"></a>Consulta para optimizar
Este es un ejemplo del tipo de consulta que se desea optimizar mediante un índice.  
  
```sql  
SELECT SalesOrderNumber,
    OrderDate,
    JSON_VALUE(Info, '$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info, '$.Customer.Name') = N'Aaron Campbell' 
```  

### <a name="example-index"></a>Índice del ejemplo
Si desea acelerar los filtros o `ORDER BY` cláusulas en una propiedad de un documento JSON, puede usar los mismos índices que ya está usando en otras columnas. Sin embargo, no se puede *directamente* hacer referencia a propiedades de los documentos JSON.
    
1.  En primer lugar, tendrá que crear una "columna virtual" que devuelva los valores que desea usar para filtrar.
2.  Después, debe crear un índice de esa columna virtual.  
  
En el ejemplo siguiente se crea una columna calculada que se puede usar para la indización. A continuación, crea un índice en la nueva columna calculada. Este ejemplo crea una columna que muestra el nombre del cliente, que se almacena en la `$.Customer.Name` ruta de acceso en los datos JSON. 
  
```sql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
### <a name="more-info-about-the-computed-column"></a>Para obtener más información acerca de la columna calculada 
La columna calculada no se conserva. Se calcula solo cuando hay que volver a generar el índice. No ocupa espacio adicional en la tabla.   
  
Es importante que crea la columna calculada con la misma expresión que va a usar en las consultas; en este ejemplo, la expresión es `JSON_VALUE(Info, '$.Customer.Name')`.  
  
No tiene que volver a escribir las consultas. Si se usan expresiones con la `JSON_VALUE` función, como se muestra en la consulta de ejemplo anterior, SQL Server considera que hay una columna calculada equivalente con la misma expresión y aplica un índice si es posible.

### <a name="execution-plan-for-this-example"></a>Plan de ejecución de este ejemplo
Este es el plan de ejecución de la consulta en este ejemplo.  
  
![Plan de ejecución](../../relational-databases/json/media/jsonindexblog1.png "Plan de ejecución")  
  
En lugar examinar toda la tabla, SQL Server busca un índice en el índice no agrupado e identifica las filas que satisfacen las condiciones especificadas. A continuación, usa una búsqueda de claves en el `SalesOrderHeader` tabla para capturar las otras columnas que se hace referencia en la consulta: en este ejemplo, `SalesOrderNumber` y `OrderDate`.  
 
### <a name="optimize-the-index-further-with-included-columns"></a>Optimizar aún más el índice con columnas incluidas
Puede evitar esta búsqueda adicional en la tabla si agrega las columnas necesarias en el índice. Puede agregar estas columnas como columnas incluidas estándar, tal como se muestra en el ejemplo siguiente, que amplía el `CREATE INDEX` ejemplo mostrado anteriormente.  
  
```sql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
En este caso no tiene SQL Server leer datos adicionales desde la `SalesOrderHeader` tabla, ya que todo lo que necesita se incluye en el índice JSON no agrupado. Se trata de una buena forma de combinar datos JSON de columna en las consultas y crear índices óptimos para la carga de trabajo.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>Los índices JSON son índices de intercalación  
Una característica importante de los índices basados en datos JSON es que los índices son compatibles con la intercalación. El resultado de la `JSON_VALUE` función que se usa cuando se crea la columna calculada es un valor de texto que hereda la intercalación de la expresión de entrada. Por lo tanto, los valores en el índice se ordenan con las reglas de intercalación definidas en las columnas de origen.  
  
Para demostrar esto, en el ejemplo siguiente se crea una tabla de colección simple con una clave principal y el contenido JSON.  
  
```sql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
El comando anterior especifica la intercalación del serbio (cirílico) para la columna JSON. En el ejemplo siguiente se rellena la tabla y crea un índice en la propiedad name.  
  
```sql  
INSERT INTO JsonCollection
VALUES
(N'{"name":"Иво","surname":"Андрић"}'),
(N'{"name":"Андрија","surname":"Герић"}'),
(N'{"name":"Владе","surname":"Дивац"}'),
(N'{"name":"Новак","surname":"Ђоковић"}'),
(N'{"name":"Предраг","surname":"Стојаковић"}'),
(N'{"name":"Михајло","surname":"Пупин"}'),
(N'{"name":"Борислав","surname":"Станковић"}'),
(N'{"name":"Владимир","surname":"Грбић"}'),
(N'{"name":"Жарко","surname":"Паспаљ"}'),
(N'{"name":"Дејан","surname":"Бодирога"}'),
(N'{"name":"Ђорђе","surname":"Вајферт"}'),
(N'{"name":"Горан","surname":"Бреговић"}'),
(N'{"name":"Милутин","surname":"Миланковић"}'),
(N'{"name":"Никола","surname":"Тесла"}')
GO
  
ALTER TABLE JsonCollection
ADD vName AS JSON_VALUE(json,'$.name')

CREATE INDEX idx_name
ON JsonCollection(vName)
```  
  
Los comandos anteriores crean un índice estándar en la columna calculada `vName`, que representa el valor de la JSON `$.name` propiedad. En la página de códigos del serbio (cirílico), el orden de las letras es 'А', 'Б', 'В', 'Г', 'Д', 'Ђ', 'Е', etc. El orden de los elementos en el índice es compatible con las reglas del serbio (cirílico) porque el resultado de la `JSON_VALUE` función hereda la intercalación de la columna de origen. En el ejemplo siguiente se realiza una consulta de esta colección y se ordenan los resultados por nombre.  
  
```sql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 Si observa el plan de ejecución real, verá que emplea los valores ordenados del índice no agrupado.  
  
 ![Plan de ejecución](../../relational-databases/json/media/jsonindexblog2.png "Plan de ejecución")  
  
 Aunque la consulta tiene un `ORDER BY` cláusula, el plan de ejecución no usa un operador de ordenación. El índice JSON ya está ordenado según reglas del serbio (cirílico). Por lo tanto, SQL Server puede utilizar el índice no agrupado donde los resultados ya están ordenados.  
  
 Sin embargo, si cambiamos la intercalación de la `ORDER BY` expresión — por ejemplo, si colocamos `COLLATE French_100_CI_AS_SC` después de la `JSON_VALUE` función - obtenemos un plan de ejecución de consulta diferente.  
  
 ![Plan de ejecución](../../relational-databases/json/media/jsonindexblog3.png "Plan de ejecución")  
  
 Puesto que el orden de los valores en el índice no cumple las reglas de intercalación del francés, SQL Server no puede utilizar el índice para ordenar los resultados. Por lo tanto, agrega un operador Sort que ordena los resultados mediante las reglas de intercalación del francés.  
 
## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Obtener más información sobre la compatibilidad integrada de JSON en SQL Server  
Para una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte el [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en la base de datos de SQL de Azure mediante el Administrador de programas de Microsoft Jovan Popovic.

