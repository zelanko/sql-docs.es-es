---
title: Datos JSON (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- JSON
- JSON, built-in support
ms.assetid: c9a4e145-33c3-42b2-a510-79813e67806a
caps.latest.revision: "47"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: b8479ec695d01cfc6963fd6b57c55a8605e25d16
ms.sourcegitcommit: 19e1c4067142d33e8485cb903a7a9beb7d894015
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2017
---
# <a name="json-data-sql-server"></a>Datos JSON (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

JSON es un formato de datos de texto muy popular que se usa para intercambiar datos en las aplicaciones web y móviles de hoy día. JSON también sirve para almacenar los datos no estructurados en archivos de registro o en bases de datos NoSQL, como Microsoft Azure Cosmos DB. Muchos servicios web REST devuelven resultados con formato de texto JSON o bien aceptan datos con este formato. Por ejemplo, la mayoría de los servicios de Azure, como Azure Search, Azure Storage y Azure Cosmos DB, cuentan con puntos de conexión REST que devuelven o usan JSON. JSON es también el formato principal para intercambiar datos entre páginas web y servidores web a través de llamadas AJAX.  
  
 Este es un ejemplo de texto JSON:  
  
```json  
[{
    "name": "John",
    "skills": ["SQL", "C#", "Azure"]
}, {
    "name": "Jane",
    "surname": "Doe"
}]
```  
  
 SQL Server proporciona funciones y operadores integrados que permiten hacer lo siguiente con texto JSON.  
  
-   Analizar texto JSON y leer o modificar valores.  
  
-   Transformar matrices de objetos JSON a formato de tabla.  
  
-   Ejecutar cualquier consulta de Transact-SQL en los objetos JSON convertidos.  
  
-   Dar formato JSON a los resultados de consultas de Transact-SQL.  
  
 ![Información general de la compatibilidad de JSON integrada](../../relational-databases/json/media/jsonslides1overview.png "Información general de la compatibilidad de JSON integrada")  
  
## <a name="key-json-capabilities-of-sql-server"></a>Funcionalidades clave de JSON de SQL Server 
A continuación, se indica más información sobre las funcionalidades clave que proporciona SQL Server con su compatibilidad de JSON integrada.

### <a name="extract-values-from-json-text-and-use-them-in-queries"></a>Extraer valores de texto JSON y usarlos en consultas
Si tiene texto JSON almacenado en tablas de base de datos, puede usar las funciones integradas para leer o modificar los valores de ese texto JSON.  
  
-   Use la función **JSON_VALUE** para extraer un valor escalar de una cadena JSON.
  
-   Use **JSON_QUERY** para extraer un objeto o una matriz de una cadena JSON.
  
-   Use la función **ISJSON** para comprobar si una cadena contiene JSON válido.

-   Use la función **JSON_MODIFY** para cambiar un valor en una cadena JSON.

**Ejemplo**
  
 En el siguiente ejemplo, la consulta usa datos tanto relacionales como JSON (almacenados en la columna denominada `jsonCol`) de una tabla:  
  
```sql  
SELECT Name,Surname,
 JSON_VALUE(jsonCol,'$.info.address.PostCode') AS PostCode,
 JSON_VALUE(jsonCol,'$.info.address."Address Line 1"')+' '
  +JSON_VALUE(jsonCol,'$.info.address."Address Line 2"') AS Address,
 JSON_QUERY(jsonCol,'$.info.skills') AS Skills
FROM People
WHERE ISJSON(jsonCol)>0
 AND JSON_VALUE(jsonCol,'$.info.address.Town')='Belgrade'
 AND Status='Active'
ORDER BY JSON_VALUE(jsonCol,'$.info.address.PostCode')
```  
  
 Las herramientas y aplicaciones no distinguen entre los valores extraídos de las columnas de la tabla escalar y los valores de las columnas JSON. Puede usar los valores del texto JSON en cualquier parte de la consulta de Transact-SQL (incluidas las cláusulas WHERE, ORDER BY y GROUP BY, los agregados de ventanas, etc.). Las funciones JSON usan una sintaxis parecida a la de JavaScript para hacer referencia a los valores de texto JSON.

Para obtener más información, vea [Validar, consultar y cambiar datos JSON con funciones integradas &#40;SQL Server&#41;](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md), [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)y [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
### <a name="change-json-values"></a>Cambiar valores de JSON
Si necesita modificar partes del texto JSON, puede usar la función **JSON_MODIFY** para actualizar el valor de una propiedad en una cadena JSON y devolver la cadena JSON actualizada. En el siguiente ejemplo se actualiza el valor de una propiedad de una variable que contiene JSON.  
  
```sql  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=JSON_MODIFY(@jsonInfo,'$.info.address[0].town','London') 
```  
  
### <a name="convert-json-collections-to-a-rowset"></a>Convertir colecciones de JSON en un conjunto de filas
No es necesario un lenguaje de consulta personalizado para consultar JSON en SQL Server. Para consultar datos JSON, puede usar T-SQL estándar. Si necesita crear una consulta o un informe sobre datos JSON, puede convertir los datos JSON fácilmente en filas y columnas llamando a la función de conjunto de filas **OPENJSON**. Para obtener más información, vea [Convert JSON Data to Rows and Columns with OPENJSON &#40;SQL Server&#41; (Convertir datos JSON en filas y columnas con OPENJSON &#40;SQL Server&#41;)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md).  
  
 En el siguiente ejemplo, se llama a **OPENJSON** y se transforma la matriz de objetos almacenada en la variable `@json` en un conjunto de filas que se puede consultar con una instrucción estándar **SELECT** de SQL:  
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json =  
N'[  
       { "id" : 2,"info": { "name": "John", "surname": "Smith" }, "age": 25 },  
       { "id" : 5,"info": { "name": "Jane", "surname": "Smith" }, "dob": "2005-11-04T12:00:00" }  
 ]'  
   
SELECT *  
FROM OPENJSON(@json)  
  WITH (id int 'strict $.id',  
        firstName nvarchar(50) '$.info.name', lastName nvarchar(50) '$.info.surname',  
        age int, dateOfBirth datetime2 '$.dob')  
```  
  
 **Resultado**  
  
|id|firstName|lastName|age|dateOfBirth|  
|--------|---------------|--------------|---------|-----------------|  
|2|John|Smith|25||  
|5|Jane|Smith||2005-11-04T12:00:00|  
  
 **OPENJSON** transforma la matriz de objetos JSON en una tabla, donde cada objeto se representa como una fila y los pares clave-valor se devuelven en forma de celdas. El resultado obedece las siguientes reglas.
-   **OPENJSON** convierte valores JSON a los tipos especificados en la cláusula **WITH**.
-   **OPENJSON** se puede encargar tanto de los pares clave-valor sin formato como de los objetos anidados organizados jerárquicamente.
-   No hay que devolver todos los campos incluidos en el texto JSON.
-   **OPENJSON** devuelve valores NULL cuando no existen valores JSON.
-   Opcionalmente, puede especificar una ruta de acceso después de la especificación de tipo para hacer referencia a una propiedad anidada o a una propiedad mediante un nombre diferente.
-   El prefijo opcional **strict** en la ruta de acceso señala que los valores de las propiedades especificadas deben existir en el texto JSON.

Para obtener más información, vea [Convert JSON Data to Rows and Columns with OPENJSON &#40;SQL Server&#41; (Convertir datos JSON en filas y columnas con OPENJSON &#40;SQL Server&#41;)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md) y [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
### <a name="convert-sql-server-data-to-json-or-export-json"></a>Convertir datos de SQL Server a JSON o exportar JSON
Para dar formato JSON a los datos de SQL Server o a los resultados de las consultas, agregue la cláusula **FOR JSON** a una instrucción **SELECT** . Use FOR JSON para delegar en SQL Server la aplicación de formato de los resultados de JSON de las aplicaciones cliente. Para obtener más información, vea [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Dar formato JSON a los resultados de consulta con FOR JSON &#40;SQL Server&#41;)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
 En el siguiente ejemplo se usa el modo PATH con la cláusula FOR JSON.  
  
```sql  
SELECT id, firstName AS "info.name", lastName AS "info.surname", age, dateOfBirth as dob  
FROM People  
FOR JSON PATH  
```  
  
El **FOR JSON** cambia el formato de los resultados SQL a texto JSON que podrá usarse en cualquier aplicación que comprenda JSON. En la opción PATH se usan alias separados por puntos en la cláusula SELECT para anidar objetos en los resultados de la consulta.  
  
 **Resultado**  
  
```json  
[{
    "id": 2,
    "info": {
        "name": "John",
        "surname": "Smith"
    },
    "age": 25
}, {
    "id": 5,
    "info": {
        "name": "Jane",
        "surname": "Smith"
    },
    "dob": "2005-11-04T12:00:00"
}] 
```  
  
 Para obtener más información, vea [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Dar formato JSON a los resultados de consulta con FOR JSON &#40;SQL Server&#41;)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md) y [FOR &#40;Cláusula de Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  
  
## <a name="combine-relational-and-json-data"></a>Combinar datos relacionales y datos JSON
 SQL Server proporciona un modelo híbrido para almacenar y procesar datos JSON y relacionales con lenguaje Transact-SQL estándar. Puede organizar colecciones de documentos JSON en tablas, establecer relaciones entre ellas, combinar columnas escalares fuertemente tipadas y almacenadas en tablas con pares clave-valor flexibles almacenados en columnas JSON y, además, consultar valores JSON y escalares en una o varias tablas mediante Transact-SQL al completo.
 
El texto JSON se suele almacenar en columnas varchar o nvarchar y se indexa como texto sin formato. Cualquier componente o característica de SQL Server que admita texto admite JSON, por lo que no hay casi ninguna restricción en cuanto a la interacción entre JSON y otras características de SQL Server. Así, JSON se puede almacenar en tablas temporales o tablas en memoria, se pueden aplicar predicados de seguridad de nivel de fila al texto JSON, etc.

Si tiene cargas de trabajo JSON puras en las que quiera usar algún tipo de lenguaje de consulta personalizado para procesar documentos JSON, sopese la posibilidad de usar Microsoft Azure [Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).  
  
 Estos son algunos casos de uso que muestran cómo se puede usar la compatibilidad integrada de JSON en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-data-from-a-sql-server-table-formatted-as-json"></a>Obtener datos de una tabla de SQL Server con formato JSON  
 Si tiene un servicio web que toma datos de la capa de base de datos y los devuelve en formato JSON o en bibliotecas o marcos de trabajo de JavaScript que aceptan datos con formato JSON, puede dar formato JSON a los resultados directamente en una consulta de SQL. En lugar de escribir código o incluir una biblioteca para convertir los resultados de consulta tabulares para, luego, serializar esos objetos en formato JSON, puede usar FOR JSON para delegar en SQL Server la aplicación de formato JSON.  
  
 Por ejemplo, imaginemos que quiere generar un resultado JSON que sea compatible con la especificación OData. El servicio web espera una solicitud y una respuesta en el siguiente formato.  
  
-   Solicitud: `/Northwind/Northwind.svc/Products(1)?$select=ProductID,ProductName`  
  
-   Respuesta: `{"@odata.context":"http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity","ProductID":1,"ProductName":"Chai"}`  
  
 Esta dirección URL de OData representa una solicitud de las columnas ProductID y ProductName del producto con el identificador 1. Puede usar **FOR JSON** para aplicar al resultado el formato que SQL Server espera.  
  
```sql  
SELECT 'http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity'
 AS '@odata.context',   
 ProductID, Name as ProductName   
FROM Production.Product  
WHERE ProductID = 1  
FOR JSON AUTO  
```  
  
El resultado de esta consulta es un texto JSON totalmente compatible con la especificación OData. SQL Server se encarga de aplicar el formato y las secuencias de escape. SQL Server también puede aplicar cualquier tipo de formato a los resultados de una consulta, como JSON de OData o GeoJSON. Para obtener más información, vea [Returning spatial data in GeoJSON format](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/returning-spatial-data-in-geojson-format-part-1) (Devolver datos espaciales en formato GeoJSON).  
  
## <a name="analyze-json-data-with-sql-queries"></a>Analizar datos JSON con consultas SQL  
 Si necesita filtrar o agregar datos JSON para elaborar informes, puede usar **OPENJSON** para transformar JSON en formato relacional. Luego, use el lenguaje [!INCLUDE[tsql](../../includes/tsql-md.md)] estándar y las funciones integradas para preparar los informes.  
  
```sql  
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date  
FROM   SalesOrderRecord AS Tab  
          CROSS APPLY  
     OPENJSON (Tab.json, N'$.Orders.OrdersArray')  
           WITH (  
              Number   varchar(200) N'$.Order.Number',   
              Date     datetime     N'$.Order.Date',  
              Customer varchar(200) N'$.AccountNumber',   
              Quantity int          N'$.Item.Quantity'  
           )  
  AS SalesOrderJsonData  
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'  
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified  
```  
  
 En la misma consulta se pueden usar tanto valores como columnas de tabla estándar de texto JSON. Puede agregar índices a la expresión `JSON_VALUE(Tab.json, '$.Status')` para mejorar el rendimiento de la consulta. Para obtener más información, vea [Indexación de datos JSON](../../relational-databases/json/index-json-data.md).
  
## <a name="import-json-data-into-sql-server-tables"></a>Importar datos JSON a tablas de SQL Server  
 Si tiene que cargar los datos JSON a SQL Server desde un servicio externo, puede usar **OPENJSON** para importar los datos a SQL Server en lugar de analizarlos en el nivel de la aplicación.  
  
```sql  
DECLARE @jsonVariable NVARCHAR(MAX)

SET @jsonVariable = N'[  
        {  
          "Order": {  
            "Number":"SO43659",  
            "Date":"2011-05-31T00:00:00"  
          },  
          "AccountNumber":"AW29825",  
          "Item": {  
            "Price":2024.9940,  
            "Quantity":1  
          }  
        },  
        {  
          "Order": {  
            "Number":"SO43661",  
            "Date":"2011-06-01T00:00:00"  
          },  
          "AccountNumber":"AW73565",  
          "Item": {  
            "Price":2024.9940,  
            "Quantity":3  
          }  
       }  
  ]'
  
INSERT INTO SalesReport  
SELECT SalesOrderJsonData.*  
FROM OPENJSON (@jsonVariable, N'$.Orders.OrdersArray')  
           WITH (  
              Number   varchar(200) N'$.Order.Number',   
              Date     datetime     N'$.Order.Date',  
              Customer varchar(200) N'$.AccountNumber',   
              Quantity int          N'$.Item.Quantity'  
           )  
  AS SalesOrderJsonData;  
```  
  
 El contenido de la variable JSON puede proceder de algún servicio REST externo, enviarse como un parámetro desde un marco de trabajo de JavaScript de cliente o bien cargarse desde archivos externos. Los resultados de texto JSON se pueden insertar, actualizar o combinar fácilmente en tablas de SQL Server. Para obtener más información sobre este escenario, vea las siguentes entradas de blog.
-   [Importing JSON data in SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/09/22/openjson-the-easiest-way-to-import-json-text-into-table/)
-   [Upsert JSON documents in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/03/upsert-json-documents-in-sql-server-2016)
-   [Loading GeoJSON data into SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/loading-geojson-data-into-sql-server/).  
  
## <a name="load-json-files-into-sql-server"></a>Cargar archivos JSON en SQL Server  
 Se puede aplicar formato JSON o JSON delimitado por filas estándar a la información almacenada en archivos. SQL Server puede importar el contenido de archivos JSON, analizarlo mediante las funciones **OPENJSON** o **JSON_VALUE**, y cargarlo en tablas.  
  
-   Si los documentos JSON están almacenados en archivos locales, en unidades de red compartidas o en ubicaciones de Azure File Storage a los que SQL Server tenga acceso, puede realizar una operación de importación en bloque para cargar los datos JSON en SQL Server. Para obtener más información sobre este escenario, vea [Importing JSON files into SQL Server using OPENROWSET (BULK)](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2015/10/07/importing-json-files-into-sql-server-using-openrowset-bulk.aspx)(Importar archivos JSON a SQL Server con OPENROWSET (BULK)).  
  
-   Si los archivos JSON delimitados por línea se encuentran en un sistema de archivos de Hadoop o de un almacenamiento de blobs de Azure, puede usar Polybase para cargar el texto JSON, analizarlo en código de Transact-SQL y cargarlo en tablas.  
  
## <a name="test-drive-built-in-json-support"></a>Probar la compatibilidad integrada de JSON  
 **Pruebe la compatibilidad integrada de JSON con la base de datos de ejemplo de AdventureWorks.** Para obtener la base de datos de ejemplo de AdventureWorks, descargue al menos el archivo de base de datos y el archivo de ejemplos y scripts [aquí](https://www.microsoft.com/en-us/download/details.aspx?id=49502). Después de restaurar la base de datos de ejemplo en una instancia de SQL Server 2016, descomprima el archivo de ejemplos y abra el archivo "JSON Sample Queries procedures views and indexes.sql" desde la carpeta JSON. Ejecute los scripts de este archivo para cambiar el formato de algunos datos existentes a datos JSON, ejecutar consultas de ejemplo e informes basados en los datos JSON, indexar los datos JSON e importar y exportar JSON.  
  
 Esto es lo que se puede hacer con los scripts incluidos en el archivo.  
  
1.  Desnormalizar el esquema existente para crear columnas de datos JSON.  
  
    1.  Almacene la información SalesReasons, SalesOrderDetails, SalesPerson, Customer y otras tablas con información relativa a pedidos de ventas en columnas JSON de la tabla SalesOrder_json.  
  
    2.  Almacene información de las tablas EmailAddresses/PersonPhone en la tabla Person_json como matrices de objetos JSON.  
  
2.  Crear procedimientos y vistas que consultan datos JSON.  
  
3.  Indexar datos JSON: cree índices en las propiedades JSON e índices de texto completo.  
  
4.  Importar y exportar JSON: cree y ejecute procedimientos que exporten el contenido de las tablas Person y SalesOrder como resultados JSON. Importe y actualice las tablas Person y SalesOrder con entradas JSON.  
  
5.  Ejecutar ejemplos de consultas. Ejecute algunas consultas que llamen a las vistas y procedimientos almacenados creados en los pasos 2 y 4.  
  
6.  Limpiar scripts. No lleve esto a cabo si quiere conservar las vistas y procedimientos almacenados creados en los pasos 2 y 4.  
  
## <a name="learn-more-about-built-in-json-support"></a>Más información sobre la compatibilidad integrada de JSON  
  
### <a name="topics-in-this-section"></a>Temas de esta sección  
 [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Dar formato JSON a los resultados de consulta con FOR JSON &#40;SQL Server&#41;)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
 Use la cláusula FOR JSON para delegar en SQL Server la aplicación de formato a los resultados de JSON procedentes de aplicaciones cliente.  
  
 [Convert JSON Data to Rows and Columns with OPENJSON &#40;SQL Server&#41; (Convertir datos JSON en filas y columnas con OPENJSON &#40;SQL Server&#41;)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)  
 Use OPENJSON para importar datos JSON a SQL Server o para convertir datos JSON en un formato relacional para una aplicación o servicio que actualmente no puede usar JSON directamente (como SQL Server Integration Services).  
  
 [Validar, consultar y cambiar datos JSON con funciones integradas &#40;SQL Server&#41;](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)  
 Use estas funciones integradas para validar texto JSON y para extraer un valor escalar, un objeto o una matriz.  
  
 [Expresiones de ruta de acceso JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
 Use una expresión de ruta para especificar el texto JSON que quiera usar.  
  
 [Indexación de datos JSON](../../relational-databases/json/index-json-data.md)  
 Use columnas calculadas para crear índices de intercalación de las propiedades de documentos JSON.  
  
[Solve common issues with JSON in SQL Server](../../relational-databases/json/solve-common-issues-with-json-in-sql-server.md) (Resolver problemas comunes con JSON en SQL Server)  
 Encuentre respuestas a algunas preguntas habituales sobre la compatibilidad integrada de JSON en SQL Server.  
  
### <a name="microsoft-blog-posts"></a>Entrada de blog de Microsoft  
  
-   Para obtener una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte las [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en Azure SQL Database ofrecidas por el director de programas de Microsoft Jovan Popovic.  
  
### <a name="reference-topics"></a>Temas de referencia  
  
-   [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md) (FOR JSON)  
  
-   [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
-   [JSON Functions &#40;Transact-SQL&#41;](../../t-sql/functions/json-functions-transact-sql.md)  
  
    -   [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)  
  
    -   [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)  
  
    -   [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
    -   [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)  
  
  
