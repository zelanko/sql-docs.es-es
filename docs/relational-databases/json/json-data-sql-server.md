---
title: "Datos JSON (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "JSON"
  - "JSON, compatibilidad integrada"
ms.assetid: c9a4e145-33c3-42b2-a510-79813e67806a
caps.latest.revision: 47
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# Datos JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  JSON es un formato de datos de texto muy popular que se usa para intercambiar datos en las aplicaciones web y móviles de hoy día. JSON también sirve para almacenar los datos no estructurados en archivos de registro o en bases de datos NoSQL, como Microsoft Azure DocumentDB. Muchos servicios web REST devuelven resultados con formato de texto JSON o bien aceptan datos con este formato. La mayoría de los servicios de Azure, como Búsqueda de Azure, Almacenamiento de Azure o Azure DocumentDB, cuentan con puntos de conexión REST que devuelven o usan JSON. JSON es también el formato principal para intercambiar datos entre páginas web y servidores web a través de llamadas AJAX.  
  
 Este es un ejemplo de texto JSON:  
  
```json  
[   
   { "name": "John", "skills":["SQL","C#","Azure"] },  
   { "name": "Jane", "surname": "Doe" }  
]  
```  
  
 SQL Server proporciona funciones y operadores integrados que permiten hacer lo siguiente.  
  
-   Analizar texto JSON y leer o modificar valores.  
  
-   Transformar matrices de objetos JSON a formato de tabla.  
  
-   Usar cualquier consulta Transact SQL en los objetos JSON convertidos.  
  
-   Dar formato JSON a los resultados de consultas de Transact-SQL.  
  
 ![Overview of built-in JSON support](../../relational-databases/json/media/jsonslides1overview.png "Overview of built-in JSON support")  
  
 Estas son las principales funciones que SQL Server ofrece.  
  
 **Extraer valores de texto JSON y usarlos en consultas.** Si tiene texto JSON almacenado en tablas de base de datos, puede usar las funciones integradas para leer o modificar los valores de ese texto JSON.  
  
-   Use la función **JSON_VALUE** para extraer un valor escalar de una cadena JSON.  
  
-   Use **JSON_QUERY** para extraer un objeto o una matriz.  
  
-   Use la función **ISJSON** para comprobar si una cadena contiene JSON válido.  
  
 En el siguiente ejemplo vemos la consulta que usa datos tanto relacionales como JSON (almacenados en la columna jsonCol) de una tabla:  
  
```tsql  
  
SELECT Name, Surname,     
    JSON_VALUE(jsonCol, '$.info.address.PostCode') as PostCode,  
    JSON_VALUE(jsonCol, '$.info.address."Address Line 1"') +  ' ' + JSON_VALUE(jsonCol, '$.info.address."Address Line 2"') AS Address,  
    JSON_QUERY(jsonCol, '$.info.skills') as Skills  
FROM PeopleCollection  
WHERE ISJSON(jsonCol) > 0   
  AND JSON_VALUE(jsonCol, '$.info.address.town') = 'Belgrade'  
  AND Status = 'Active'  
ORDER BY JSON_VALUE(@jsonInfo, '$.info.address.PostCode')  
  
```  
  
 Las herramientas y aplicaciones no distinguen entre los valores extraídos de las columnas de la tabla escalar y los valores de las columnas JSON. Los valores del texto JSON se pueden usar en cualquier parte de la consulta de Transact-SQL (incluidas las cláusulas WHERE, ORDER BY o GROUP BY, en agregados de ventana, etc.). Las funciones JSON usan una sintaxis parecida a la de JavaScript para hacer referencia a los valores de texto JSON. Para obtener más información, vea [Validar, consultar y cambiar datos JSON con funciones integradas &#40;SQL Server&#41;](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md), [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md) y [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
 **Cambie valores JSON.** Si necesita modificar partes del texto JSON, puede usar la función **JSON_MODIFY** para actualizar el valor de una propiedad en una cadena JSON y devolver la cadena JSON actualizada. En el siguiente ejemplo se actualiza el valor de una propiedad de una variable que contiene JSON.  
  
```tsql  
SET @jsonInfo = JSON_MODIFY(@jsonInfo, '$.info.address[0].town', 'London')  
```  
  
 **Convierta colecciones de JSON en un conjunto de filas.** No es necesario un lenguaje de consulta personalizado para consultar JSON en SQL Server. Para consultar datos JSON, puede usar T-SQL estándar. Si necesita crear una consulta o un informe sobre datos JSON, puede convertir los datos JSON fácilmente en filas y columnas; para ello, debe llamar a la función de conjunto de filas **OPENJSON**. Use la función **OPENJSON** para importar datos JSON a SQL Server o para convertir datos JSON en filas y columnas. Para obtener más información, vea [Convert JSON Data to Rows and Columns with OPENJSON &#40;SQL Server&#41; (Convertir datos JSON en filas y columnas con OPENJSON &#40;SQL Server&#41;)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md).  
  
 En el siguiente ejemplo se llama a **OPENJSON** , que transforma la matriz de objetos almacenada en la variable **@json** en un conjunto de filas que se puede consultar con la instrucción estándar SELECT de SQL:  
  
```tsql  
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
  
 **OPENJSON** transforma la matriz de objetos JSON en una tabla, donde cada objeto se representa como una fila y los pares clave-valor se devolverán como celdas. **OPENJSON** convierte los valores JSON en los tipos especificados. **OPENJSON** se puede encargar tanto de los pares clave-valor sin formato como de los objetos anidados organizados jerárquicamente. No hay que devolver todos los campos incluidos en el texto JSON. **OPENJSON** devuelve valores NULL cuando no existen valores JSON. Opcionalmente, también puede especificar una ruta de acceso después de la especificación de tipo para hacer referencia a una propiedad anidada o a una propiedad con un nombre diferente. El prefijo opcional **strict** en la ruta de acceso señala que los valores de las propiedades especificadas deben existir en el texto JSON. Para obtener más información, vea [Convert JSON Data to Rows and Columns with OPENJSON &#40;SQL Server&#41; (Convertir datos JSON en filas y columnas con OPENJSON &#40;SQL Server&#41;)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md) y [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
 **Convertir datos de SQL Server a JSON o exportar JSON.** Para dar formato JSON a los datos de SQL Server o a los resultados de las consultas, agregue la cláusula **FOR JSON** a una instrucción **SELECT**. Use FOR JSON para delegar en SQL Server la aplicación de formato de los resultados de JSON de las aplicaciones cliente. Para obtener más información, vea [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Dar formato JSON a los resultados de consulta con FOR JSON &#40;SQL Server&#41;)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
 En el siguiente ejemplo se usa el modo PATH con la cláusula FOR JSON.  
  
```tsql  
SELECT id, firstName AS "info.name", lastName AS "info.surname", age, dateOfBirth as dob  
FROM People  
FOR JSON PATH  
```  
  
 El   
La cláusula     **FOR JSON** cambia el formato de los resultados SQL a texto JSON que podrá usarse en cualquier aplicación que comprenda JSON. En la opción PATH se usan alias separados por puntos en la cláusula SELECT para anidar objetos en los resultados de la consulta.  
  
 **Resultado**  
  
```json  
[  
      { "id" : 2,"info": { "name": "John", "surname": "Smith" }, "age": 25 },  
      { "id" : 5,"info": { "name": "Jane", "surname": "Smith" }, "dob": "2005-11-04T12:00:00" }  
]  
```  
  
 Para obtener más información, vea [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Dar formato JSON a los resultados de consulta con FOR JSON &#40;SQL Server&#41;)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md) y [FOR &#40;Cláusula de Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md).  
  
## Casos de uso  
 SQL Server proporciona un modelo híbrido para almacenar y procesar datos JSON y relacionales con lenguaje Transact-SQL estándar. Este modelo permite organizar recopilaciones de documentos JSON en tablas, establecer relaciones entre ellas, combinar columnas escalares fuertemente tipadas y almacenadas en tablas con pares clave-valor flexibles almacenados en columnas JSON y, además, consultar valores JSON y escalares en una o varias tablas mediante Transact-SQL. El texto JSON se suele almacenar en columnas varchar o nvarchar y se indexa como texto sin formato. Cualquier componente o característica de SQL Server que admita texto admite JSON, por lo que no hay casi ninguna restricción en cuanto a la interacción entre JSON y otras características de SQL Server. Así, JSON se puede almacenar en tablas temporales o tablas en memoria, se pueden aplicar predicados de seguridad de nivel de fila al texto JSON, etc. Si tiene cargas de trabajo JSON puras en las que quiera usar algún tipo de lenguaje de consulta personalizado para procesar documentos JSON, sopese la posibilidad de usar Microsoft Azure [DocumentDB](https://azure.microsoft.com/services/documentdb/).  
  
 Estos son algunos casos de uso que muestran cómo se puede usar la compatibilidad integrada de JSON en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Obtener datos de una tabla de SQL Server con formato JSON  
 Si tiene un servicio web que toma datos de la capa de base de datos y los devuelve en formato JSON o en bibliotecas o marcos de trabajo de JavaScript que aceptan datos con formato JSON, puede dar formato a los resultados directamente en una consulta SQL. En lugar de escribir código o incluir una biblioteca para convertir los resultados de consulta tabulares para, luego, serializar esos objetos en formato JSON, puede usar FOR JSON para delegar en SQL Server la aplicación de formato JSON.  
  
 Por ejemplo, imaginemos que quiere generar un resultado JSON que sea compatible con la especificación OData. El servicio web espera una solicitud y una respuesta en el siguiente formato.  
  
-   Solicitud: `/Northwind/Northwind.svc/Products(1)?$select=ProductID,ProductName`  
  
-   Respuesta: `{"@odata.context":"http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity","ProductID":1,"ProductName":"Chai"}`  
  
 Esta dirección URL de OData representa una solicitud de las columnas ProductID y ProductName del producto con el identificador 1. Puede usar FOR JSON para aplicar al resultado el formato que SQL Server espera.  
  
```tsql  
SELECT 'http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity' AS '@odata.context',   
ProductID, Name as ProductName   
FROM Production.Product  
WHERE ProductID = 1  
FOR JSON AUTO  
  
```  
  
 El resultado de esta consulta es un texto JSON totalmente compatible con la especificación OData. SQL Server se encarga de aplicar el formato y las secuencias de escape. SQL Server puede aplicar cualquier tipo de formato a los resultados de una consulta, como JSON de OData o GeoJSON. Vea [Returning spatial data in GeoJSON format](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/returning-spatial-data-in-geojson-format-part-1) (Devolver datos espaciales en formato GeoJSON).  
  
## Analizar datos JSON con consultas SQL  
 Si necesita filtrar o agregar datos JSON para elaborar informes, puede usar OPENJSON para transformar JSON en formato relacional. Luego, use el lenguaje [!INCLUDE[tsql](../../includes/tsql-md.md)] estándar y las funciones integradas para preparar los informes.  
  
```tsql  
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
  
 En la misma consulta se pueden usar tanto valores como columnas de tabla estándar de texto JSON. Puede agregar índices en la expresión JSON_VALUE JSON_VALUE(Tab.json, '$.Status') para mejorar el rendimiento de la consulta.  
  
## Importar datos JSON a tablas de SQL Server  
 Si tiene que cargar los datos JSON desde un servicio externo en SQL Server, puede usar OPENJSON para importar los datos a SQL Server, en lugar de analizarlos en el nivel de la aplicación.  
  
```tsql  
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
  
 El contenido de la variable JSON puede proceder de algún servicio REST externo, enviarse como un parámetro de algún marco de trabajo de JavaScript de cliente o bien cargarse desde un archivo externo. Los resultados de texto JSON se pueden insertar, actualizar o combinar fácilmente en tablas de SQL Server. Para obtener más información sobre este escenario, consulte [Importing JSON data in SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/09/22/openjson-the-easiest-way-to-import-json-text-into-table/)(Importar datos JSON en SQL Server), [Upsert JSON documents in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/03/upsert-json-documents-in-sql-server-2016), (Insertar y actualizar documentos JSON en SQL Server 2016) y [Loading GeoJSON data into SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/loading-geojson-data-into-sql-server/)(Cargar datos GeoJSON en SQL Server 2016).  
  
## Cargar archivos JSON en SQL Server  
 Se puede aplicar formato JSON o JSON delimitado por filas estándar a la información almacenada en archivos. SQL Server puede importar el contenido de archivos JSON, analizarlos con las funciones OPENJSON o JSON_VALUE y cargarlos en tablas.  
  
 Si los archivos JSON están en un archivo local, en una unidad de red compartida o en una ubicación de Almacenamiento de archivos de Azure a los que SQL Server tiene acceso, puede realizar una operación de importación masiva para cargar los datos JSON en SQL Server. Para obtener más información sobre este escenario, vea [Importing JSON files into SQL Server using OPENROWSET (BULK)](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2015/10/07/importing-json-files-into-sql-server-using-openrowset-bulk.aspx) (Importar archivos JSON a SQL Server con OPENROWSET (BULK)).  
  
 Si los archivos JSON delimitados por línea se encuentran en un sistema de archivos de Hadoop o de un almacenamiento de blobs de Azure, puede usar Polybase para cargar el texto JSON, analizarlo en código de Transact-SQL y cargarlo en tablas.  
  
## Probar la compatibilidad integrada de JSON  
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
  
## Más información sobre la compatibilidad integrada de JSON  
  
### Temas de esta sección  
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
  
 [Preguntas más frecuentes sobre JSON en SQL Server](../Topic/Frequently%20Asked%20Questions%20about%20JSON%20in%20SQL%20Server.md)  
 Encuentre respuestas a algunas preguntas habituales sobre la compatibilidad integrada de JSON en SQL Server.  
  
### Entrada de blog de Microsoft  
  
-   [Entradas de blog del administrador de programas de Microsoft Jovan Popovic](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
### Temas de referencia  
  
-   [Cláusula FOR &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md) (FOR JSON)  
  
-   [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
-   [JSON Functions &#40;Transact-SQL&#41;](../../t-sql/functions/json-functions-transact-sql.md)  
  
    -   [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)  
  
    -   [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)  
  
    -   [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
    -   [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)  
  
  