---
title: Importar documentos JSON en SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e908ec0-7173-4cd2-8f48-2700757b53a5
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 1c842fde925e89901971a525c3e171ffce050269
ms.contentlocale: es-es
ms.lasthandoff: 06/09/2017

---
# <a name="import-json-documents-into-sql-server"></a>Importar documentos JSON en SQL Server
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

En este tema se describe cómo importar archivos JSON a SQL Server. Actualmente hay una gran cantidad de documentos JSON almacenados en archivos. Información de registro de aplicaciones en archivos JSON, sensores generan información que se almacena en archivos JSON y así sucesivamente. Es importante ser capaz de leer los datos JSON almacenados en archivos, cargar los datos en SQL Server y analizarlos.

## <a name="import-a-json-document-into-a-single-column"></a>Importar un documento JSON en una sola columna
**OPENROWSET(BULK)** es una función con valores de tabla que puede leer datos de cualquier archivo que se encuentre en la unidad local o la red, si SQL Server tiene acceso de lectura a esa ubicación. Devuelve una tabla con una sola columna con el contenido del archivo. Hay varias opciones que puede utilizar con la función OPENROWSET(BULK), como pueden ser los separadores. Pero en el caso más simple, solamente puede cargar todo el contenido de un archivo como un valor de texto. (Este valor grande único se conoce como un objeto grande de carácter único o SINGLE_CLOB). 

Este es un ejemplo de la función **OPENROWSET(BULK)** que lee el contenido de un archivo JSON y lo devuelve al usuario como un valor único:

```sql
SELECT BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

OPENJSON(BULK) lee el contenido del archivo y lo devuelve en `BulkColumn`.

También puede cargar el contenido del archivo en una variable local o en una tabla, como se muestra en el ejemplo siguiente:

```sql
-- Load file contents into a variable
SELECT @json = BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j

-- Load file contents into a table 
SELECT BulkColumn
 INTO #temp 
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

Después de cargar el contenido del archivo JSON, puede guardar el texto JSON en una tabla.

## <a name="import-multiple-json-documents"></a>Importar varios documentos JSON
Puede usar el mismo enfoque para cargar un conjunto de archivos JSON desde el sistema de archivos en una variable local de uno en uno. Supongamos que los archivos se llaman `book<index>.json`.
  
```sql
DECLARE @i INT = 1
DECLARE @json AS NVARCHAR(MAX)

WHILE(@i < 10)
BEGIN
    SET @file = 'C:\JSON\Books\book' + cast(@i AS VARCHAR(5)) + '.json';
    SELECT @json = BulkColumn FROM OPENROWSET (BULK (@file), SINGLE_CLOB) AS j
    SELECT * FROM OPENJSON(@json) AS json
    -- Optionally, save the JSON text in a table.
    SET @i = @i + 1 ;
END
```

## <a name="import-json-documents-from-azure-file-storage"></a>Importar documentos JSON desde Azure File Storage
También puede utilizar OPENROWSET como se describió anteriormente para leer archivos JSON de otras ubicaciones de archivos que puede tener acceso SQL Server. Por ejemplo, Azure File Storage admite el protocolo SMB. Como resultado, puede asignar una unidad virtual local al recurso compartido de Azure File Storage mediante el procedimiento siguiente:
1.  Cree una cuenta de almacenamiento de archivos (por ejemplo, `mystorage`), un recurso compartido de archivos (por ejemplo, `sharejson`) y una carpeta de archivos en Azure File Storage mediante Azure Portal o Azure PowerShell.
2.  Cargue algunos archivos JSON en el recurso compartido de almacenamiento de archivos.
3.  Cree una regla de firewall de salida en el Firewall de Windows en el equipo que permite el puerto 445. Tenga en cuenta que su proveedor de servicio de Internet puede bloquear este puerto. Si recibe un error DNS (error 53) en el paso siguiente, es que no ha abierto el puerto 445 o su ISP lo bloquea.
4. Montar el recurso compartido de almacenamiento de archivos de Azure como una unidad local (por ejemplo `T:`).

    Aquí se muestra la sintaxis de comando:

    ```
    net use [drive letter] \\[storage name].file.core.windows.net\[share name] /u:[storage account name] [storage account access key]
    ```

    Este es un ejemplo que asigna la letra de unidad local `T:` al recurso compartido de almacenamiento de archivos de Azure:

    ```
    net use t: \\mystorage.file.core.windows.net\sharejson /u:myaccount hb5qy6eXLqIdBj0LvGMHdrTiygkjhHDvWjUZg3Gu7bubKLg==
    ```

    Puede encontrar la clave de la cuenta de almacenamiento y la clave de acceso de la cuenta de almacenamiento principal o secundaria en la sección Claves de Configuración en Azure Portal.

5.  Ahora puede acceder los archivos JSON desde el recurso compartido de almacenamiento de archivos de Azure mediante el uso de la unidad asignada, como se muestra en el ejemplo siguiente:

    ```sql
    SELECT book.* FROM
     OPENROWSET(BULK N't:\books\books.json', SINGLE_CLOB) AS json
     CROSS APPLY OPENJSON(BulkColumn)
     WITH( id nvarchar(100), name nvarchar(100), price float,
        pages_i int, author nvarchar(100)) AS book
    ```

Para más información sobre Azure File Storage, vea [File Storage](https://azure.microsoft.com/en-us/services/storage/files/).

## <a name="import-json-documents-from-azure-blob-storage"></a>Importar documentos JSON desde Azure Blob Storage

Puede cargar archivos directamente en la base de datos de SQL de Azure desde el almacenamiento de blobs de Azure con el comando T-SQL BULK INSERT o la función OPENROWSET.

En primer lugar, cree un origen de datos externo, como se muestra en el ejemplo siguiente.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
 WITH ( TYPE = BLOB_STORAGE,
        LOCATION = 'https://myazureblobstorage.blob.core.windows.net',
        CREDENTIAL= MyAzureBlobStorageCredential);
```

A continuación, ejecute un comando BULK INSERT con la opción DATA_SOURCE.

```sql
BULK INSERT Product
FROM 'data/product.dat'
WITH ( DATA_SOURCE = 'MyAzureBlobStorage');
```

Para obtener más información y un ejemplo que utiliza OPENROWSET, vea [cargar archivos desde el almacenamiento de blobs de Azure en la base de datos de SQL Azure](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/02/23/loading-files-from-azure-blob-storage-into-azure-sql-database/).

## <a name="parse-json-documents-into-rows-and-columns"></a>Analizar documentos JSON en filas y columnas
En lugar de leer un archivo JSON completo como un valor único, puede que desee analizarlos y devolver los libros en el archivo y sus propiedades en filas y columnas. En el ejemplo siguiente se usa un archivo JSON de [este sitio](https://github.com/tamingtext/book/blob/master/apache-solr/example/exampledocs/books.json) que contiene una lista de libros.

### <a name="example-1"></a>Ejemplo 1
En el ejemplo más simple, solo puede cargar toda la lista desde el archivo. 

```sql
SELECT value
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
```

### <a name="example-2"></a>Ejemplo 2
OPENROWSET lee un solo valor de texto del archivo, lo devuelve como BulkColumn y lo pasa a la función OPENJSON. OPENJSON recorre en iteración la matriz de objetos JSON de la matriz BulkColumn y devuelve un libro en cada fila, con formato JSON:

```
{"id":"978-0641723445″, "cat":["book","hardcover"], "name":"The Lightning Thief", … 
{"id":"978-1423103349″, "cat":["book","paperback"], "name":"The Sea of Monsters", … 
{"id":"978-1857995879″, "cat":["book","paperback"], "name":"Sophie’s World : The Greek … 
{"id":"978-1933988177″, "cat":["book","paperback"], "name":"Lucene in Action, Second … 
```

### <a name="example-3"></a>Ejemplo 3
La función OPENJSON puede analizar el contenido JSON y transformarlo en una tabla o un conjunto de resultados. En el ejemplo siguiente se carga el contenido, se analiza el JSON cargado y se devuelven los cinco campos como columnas:

```sql
SELECT book.*
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
 WITH( id nvarchar(100), name nvarchar(100), price float,
 pages_i int, author nvarchar(100)) AS book
```

En este ejemplo, OPENROWSET(BULK) lee el contenido del archivo y pasa ese contenido a la función OPENJSON con un esquema definido para la salida. OPENJSON hace coincidir las propiedades de los objetos JSON utilizando nombres de columna. Por ejemplo, la propiedad `price` se devuelve como una columna `price` y se convierte al tipo de datos float. He aquí los resultados:

|Identificador|Nombre|price|pages_i|Autor
|---|---|---|---|---|
978-0641723445|The Lightning Thief|12,5|384|Rick Riordan| 
978-1423103349|The Sea of Monsters|6,49|304|Rick Riordan| 
978-1857995879|Sophie’s World : The Greek Philosophers|3,07|64|Jostein Gaarder| 
978-1933988177|Lucene in Action, Second Edition|30,5|475|Michael McCandless| 

Ahora puede devolver esta tabla al usuario o cargar los datos en otra tabla.

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Obtener más información sobre la compatibilidad integrada de JSON en SQL Server  
Para una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte el [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en la base de datos de SQL de Azure mediante el Administrador de programas de Microsoft Jovan Popovic.
  
## <a name="see-also"></a>Vea también
[Convertir datos JSON en filas y columnas con OPENJSON](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)


