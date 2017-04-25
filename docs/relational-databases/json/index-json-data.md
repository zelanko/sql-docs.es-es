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
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cf3c58c7d71a98bfaa1f27611762bf7fb3fe8725
ms.lasthandoff: 04/11/2017

---
# <a name="index-json-data"></a>Indexación de datos JSON
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Los índices de la base de datos mejoran el rendimiento de las operaciones de filtro y ordenación. Sin ellos, SQL Server debe realizar un examen completo de la tabla cada vez que realice consultas de datos.  
  
 JSON no es un tipo de datos integrado en SQL Server 2016 y esta solución no tiene índices personalizados JSON. Sin embargo, puede optimizar las consultas en documentos JSON mediante índices estándar.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>Indexación de propiedades JSON mediante columnas calculadas  
 Al almacenar datos JSON en SQL Server, normalmente querrá filtrar u ordenar resultados de consultas por propiedades de los documentos JSON.  
  
 En este ejemplo, la tabla SalesOrderHeader de AdventureWorks tiene una columna "Info" que contiene diversa información sobre pedidos de ventas; por ejemplo, datos sobre clientes, vendedores, direcciones de envío y facturación, etc. Desea usar los valores de la columna Info para filtrar los pedidos de venta de un cliente. Esta es la consulta que desea optimizar mediante un índice.  
  
```tsql  
SELECT SalesOrderNumber,OrderDate,JSON_VALUE(Info,'$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info,'$.Customer.Name')=N'Aaron Campbell' 
```  
  
 Si desea acelerar los filtros o cláusulas ORDER BY en una propiedad de un documento JSON, puede usar los mismos índices que esté usando en otras columnas. Sin embargo, no puede hacer referencia directamente a las propiedades de los documentos JSON. Primero, tiene que crear una "columna virtual" que devuelva los valores que desea usar para las operaciones de filtro. Después, debe crear un índice de esa columna virtual.  
  
 En el ejemplo siguiente se crea una columna calculada que puede utilizarse para la indización y, después, se crea un índice de esa columna. En este ejemplo se crea una columna que muestra el nombre del cliente, que se almacena en la ruta de acceso $.Customer.Name de los documentos JSON.  
  
```tsql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
  
 La columna calculada no se conserva. No ocupa espacio adicional en la tabla. Se calcula solo cuando hay que volver a generar el índice.  
  
 Es importante crear la columna calculada con la misma expresión que tiene pensado usar en las consultas; en este ejemplo, `JSON_VALUE(Info, '$.Customer.Name')`.  
  
 No tiene que volver a escribir las consultas. Si se usan expresiones con la función JSON_VALUE, SQL Server considera que hay una columna calculada equivalente con la misma expresión y aplica un índice si es posible. Este es el plan de ejecución de la consulta en este ejemplo.  
  
 ![Plan de ejecución](../../relational-databases/json/media/jsonindexblog1.png "Plan de ejecución")  
  
 En lugar examinar toda la tabla, SQL Server busca un índice en el índice no agrupado e identifica las filas que satisfacen las condiciones especificadas. Después, realiza una búsqueda de claves en la tabla SalesOrderHeader para capturar otras columnas a las que se hacen referencia en la consulta: en este ejemplo, SalesOrderNumber y OrderDate.  
  
 Puede evitar esta búsqueda adicional en la tabla si agrega las columnas necesarias en el índice JSON. Puede agregar estas columnas como columnas incluidas estándar, tal y como se muestra en el ejemplo siguiente.  
  
```tsql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
 En este caso, SQL Server no lee más datos de la tabla SalesOrderHeader, ya que todo lo que necesita se incluye en el índice JSON no agrupado. Se trata de una buena forma de combinar datos JSON de columna en las consultas y de crear índices óptimos para la carga de trabajo.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>Los índices JSON son índices de intercalación  
 Una característica importante de los índices JSON es que son índices de intercalación. El resultado de la función JSON_VALUE es un valor de texto que hereda la intercalación de la expresión de entrada. Por lo tanto, los valores del índice se ordenan con las reglas de intercalación definidas en las columnas de origen.  
  
 Para demostrar esto, en el ejemplo siguiente se crea una tabla de colección simple con una clave principal y el contenido JSON.  
  
```tsql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
 El comando anterior especifica la intercalación del serbio (cirílico) para la columna JSON. En el ejemplo siguiente se rellena la tabla y crea un índice en la propiedad name.  
  
```tsql  
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
  
 Los comandos anteriores crean un índice estándar de la columna calculada vName, que representa el valor de la propiedad JSON $.name. En la página de códigos del serbio (cirílico), el orden de las letras es 'А', 'Б', 'В', 'Г', 'Д', 'Ђ', 'Е', etc. El orden de los elementos del índice cumple las reglas del serbio (cirílico) porque el resultado de la función JSON_VALUE hereda la intercalación de la columna de origen. En el ejemplo siguiente se realiza una consulta de esta colección y se ordenan los resultados por nombre.  
  
```tsql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 Si observa el plan de ejecución real, verá que emplea los valores ordenados del índice no agrupado.  
  
 ![Plan de ejecución](../../relational-databases/json/media/jsonindexblog2.png "Plan de ejecución")  
  
 Aunque la consulta tiene una cláusula ORDER BY, el plan de ejecución no usa un operador Sort. El índice JSON ya está ordenado según reglas del serbio (cirílico). Por lo tanto, SQL Server puede utilizar el índice no agrupado donde los resultados ya están ordenados.  
  
 Pero si cambiamos la intercalación de la orden mediante una expresión (por ejemplo, si colocamos `COLLATE French_100_CI_AS_SC` después de la función JSON_VALUE), obtenemos un plan de ejecución de consulta diferente.  
  
 ![Plan de ejecución](../../relational-databases/json/media/jsonindexblog3.png "Plan de ejecución")  
  
 Puesto que el orden de los valores en el índice no cumple las reglas de intercalación del francés, SQL Server no puede utilizar el índice para ordenar los resultados. Por lo tanto, agrega un operador Sort que ordena los resultados mediante las reglas de intercalación del francés.  
  
  

