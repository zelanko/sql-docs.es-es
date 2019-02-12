---
title: Indexación de datos JSON | Microsoft Docs
ms.custom: ''
ms.date: 06/01/2016
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, indexing JSON data
- indexing JSON data
ms.assetid: ced241e1-ff09-4d6e-9f04-a594a9d2f25e
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d87675c4feb0ab784f0003143406b3784f7e8a83
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012017"
---
# <a name="index-json-data"></a>Indexación de datos JSON
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

En SQL Server y SQL Database, JSON no es un tipo de datos integrado, y SQL Server no tiene índices personalizados JSON. En cambio, puede optimizar las consultas en documentos JSON mediante índices estándar. 

Los índices de la base de datos mejoran el rendimiento de las operaciones de filtro y ordenación. Sin ellos, SQL Server debe realizar un examen completo de la tabla cada vez que realice consultas de datos.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>Indexación de propiedades JSON mediante columnas calculadas  
Al almacenar datos JSON en SQL Server, normalmente querrá filtrar u ordenar resultados de consultas por una o varias *propiedades* de los documentos JSON.  

### <a name="example"></a>Ejemplo 
En este ejemplo se supone que la tabla `SalesOrderHeader` de AdventureWorks tiene una columna `Info`, que contiene diversa información en formato JSON sobre pedidos de venta. Por ejemplo, contiene información sobre clientes, vendedores, direcciones de envío y facturación, etc. Quiere usar los valores de la columna `Info` para filtrar los pedidos de venta de un cliente.

### <a name="query-to-optimize"></a>Consulta que se optimizará
Aquí tiene un ejemplo del tipo de consulta que quiere optimizar mediante un índice.  
  
```sql  
SELECT SalesOrderNumber,
    OrderDate,
    JSON_VALUE(Info, '$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info, '$.Customer.Name') = N'Aaron Campbell' 
```  

### <a name="example-index"></a>Índice de ejemplo
Si quiere acelerar los filtros o las cláusulas `ORDER BY` en una propiedad de un documento JSON, puede usar los mismos índices que ya use en otras columnas. En cambio, no puede hacer referencia *directamente* a las propiedades de los documentos JSON.
    
1.  Primero tiene que crear una "columna virtual" que devuelva los valores que quiere usar para las operaciones de filtro.
2.  Después, debe crear un índice de esa columna virtual.  
  
En el ejemplo siguiente se crea una columna calculada que se puede usar para la indexación. Después, crea un índice en la nueva columna calculada. En este ejemplo se crea una columna que muestra el nombre del cliente, que se almacena en la ruta de acceso `$.Customer.Name` de los datos JSON. 
  
```sql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
### <a name="more-info-about-the-computed-column"></a>Más información sobre la columna calculada 
La columna calculada no se conserva. Se calcula solo cuando hay que volver a generar el índice. No ocupa espacio adicional en la tabla.   
  
Es importante que cree la columna calculada con la misma expresión que tiene pensado usar en las consultas. En este ejemplo, la expresión es `JSON_VALUE(Info, '$.Customer.Name')`.  
  
No tiene que volver a escribir las consultas. Si se usan expresiones con la función `JSON_VALUE`, como se muestra en la consulta de ejemplo anterior, SQL Server considera que hay una columna calculada equivalente con la misma expresión y aplica un índice, si es posible.

### <a name="execution-plan-for-this-example"></a>Plan de ejecución de este ejemplo
Este es el plan de ejecución de la consulta de este ejemplo.  
  
![Plan de ejecución](../../relational-databases/json/media/jsonindexblog1.png "Plan de ejecución")  
  
En lugar examinar toda la tabla, SQL Server busca un índice en el índice no agrupado e identifica las filas que satisfacen las condiciones especificadas. Después, realiza una búsqueda de claves en la tabla `SalesOrderHeader` para capturar las otras columnas a las que se hace referencia en la consulta (en este ejemplo, `SalesOrderNumber` y `OrderDate`).  
 
### <a name="optimize-the-index-further-with-included-columns"></a>Mayor optimización del índice con la inclusión de columnas
Si agrega las columnas necesarias al índice, podrá evitar esta búsqueda adicional en la tabla. Puede agregar estas columnas como columnas incluidas estándar, tal y como se muestra en el ejemplo siguiente, que amplía el ejemplo `CREATE INDEX` anterior.  
  
```sql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
En este caso, SQL Server no tiene que leer más datos de la tabla `SalesOrderHeader`, ya que todo lo que necesita se incluye en el índice JSON no agrupado. Este tipo de índice es una buena forma de combinar datos JSON y de columna en las consultas y de crear índices óptimos para la carga de trabajo.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>Los índices JSON son índices de intercalación  
Una característica importante de los índices basados en datos JSON es que son compatibles con la intercalación. El resultado de la función `JSON_VALUE` que usa al crear la columna calculada es un valor de texto que hereda la intercalación de la expresión de entrada. Por tanto, los valores del índice se ordenan con las reglas de intercalación definidas en las columnas de origen.  
  
Para demostrar que los índices son de intercalación, en el ejemplo siguiente se crea una tabla de colección simple con una clave principal y el contenido JSON.  
  
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
  
Los comandos anteriores crean un índice estándar de la columna calculada `vName`, que representa el valor de la propiedad JSON `$.name`. En la página de códigos del serbio (cirílico), el orden de las letras es "А", "Б", "В", "Г", "Д", "Ђ", "Е", etc. El orden de los elementos del índice cumple las reglas del serbio (cirílico) porque el resultado de la función `JSON_VALUE` hereda la intercalación de la columna de origen. En el ejemplo siguiente se realiza una consulta de esta colección y se ordenan los resultados por nombre.  
  
```sql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 Si observa el plan de ejecución real, verá que emplea los valores ordenados del índice no agrupado.  
  
 ![Plan de ejecución](../../relational-databases/json/media/jsonindexblog2.png "Plan de ejecución")  
  
 Aunque la consulta tiene una cláusula `ORDER BY`, el plan de ejecución no usa un operador Sort. El índice JSON ya está ordenado según reglas del serbio (cirílico). Por lo tanto, SQL Server puede utilizar el índice no agrupado donde los resultados ya están ordenados.  
  
 A pesar de esto, si cambia la intercalación de la expresión `ORDER BY` (por ejemplo, si agrega `COLLATE French_100_CI_AS_SC` después de la función `JSON_VALUE`), recibirá otro plan de ejecución de consulta.  
  
 ![Plan de ejecución](../../relational-databases/json/media/jsonindexblog3.png "Plan de ejecución")  
  
 Puesto que el orden de los valores en el índice no cumple las reglas de intercalación del francés, SQL Server no puede utilizar el índice para ordenar los resultados. Por lo tanto, agrega un operador Sort que ordena los resultados mediante las reglas de intercalación del francés.  
 
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Más información sobre JSON en SQL Server y Azure SQL Database  
  
### <a name="microsoft-videos"></a>Vídeos de Microsoft

Para obtener una introducción visual a la compatibilidad integrada de JSON en SQL Server y Azure SQL Database, vea los siguientes vídeos:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 y compatibilidad con JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso de JSON en SQL Server 2016 y Azure SQL Database)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON como puente entre los universos NoSQL y relacional)
