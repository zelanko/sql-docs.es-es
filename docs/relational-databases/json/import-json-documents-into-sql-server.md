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
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fafe626643707982162ce03a02b9f707b6be2995
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="import-json-documents-into-sql-server"></a>Importar documentos JSON en SQL Server
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

En este tema se describe cómo importar archivos JSON en SQL Server. Actualmente, puede encontrar muchos documentos JSON almacenados en archivos. Los sensores generan información que se almacena en archivos JSON, información de registro de aplicaciones que se almacena en archivos JSON, etc. Es importante ser capaz de leer los datos JSON almacenados en archivos, cargar los datos en SQL Server y analizarlos.

## <a name="import-a-json-document-into-a-single-column"></a>Importar un documento JSON en una sola columna
**OPENROWSET(BULK)** es una función con valores de tabla que puede leer datos de cualquier archivo que se encuentre en la unidad local o la red, si SQL Server tiene acceso de lectura a esa ubicación. Devuelve una tabla con una sola columna con el contenido del archivo. Hay varias opciones que puede utilizar con la función OPENROWSET(BULK), como pueden ser los separadores. Pero en el caso más simple, solamente puede cargar todo el contenido de un archivo como un valor de texto. A continuación, puede cargar el contenido de ese valor en una variable o una tabla. (Este valor grande único se conoce como un objeto grande de carácter único o SINGLE_CLOB). 

Este es un ejemplo de la función **OPENROWSET(BULK)** que lee el contenido de un archivo JSON y lo devuelve al usuario como un valor único:

```tsql
SELECT BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
 ```

OPENJSON(BULK) lee el contenido del archivo y lo devuelve en `BulkColumn`.

También puede cargar el contenido del archivo en una variable local o en una tabla, como se muestra en el ejemplo siguiente:

```tsql
-- Load file contents into a variable
SELECT @json = BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j

-- Load file contents into a table 
SELECT BulkColumn
 INTO #temp 
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

## <a name="import-multiple-json-documents"></a>Importar varios documentos JSON
Puede utilizar el mismo enfoque para cargar un conjunto de archivos JSON desde el sistema de archivos en variables locales. Supongamos que los archivos se llaman `book<index>.json`.
  
```tsql
declare @i int = 1
declare @json AS nvarchar(MAX)

while(@i < 10)
begin
    SET @file = 'C:\JSON\Books\book' + cast(@i as varchar(5)) + '.json';
    SELECT @json = BulkColumn FROM OPENROWSET (BULK (@file), SINGLE_CLOB) as j
    SELECT * FROM OPENJSON(@json) as json
    set @i = @i + 1 ;
end
```

## <a name="import-json-documents-from-azure-file-storage"></a>Importar documentos JSON desde Azure File Storage
Puede utilizar el mismo enfoque descrito anteriormente para leer archivos JSON de ubicaciones de archivo a las que SQL Server puede acceder. Por ejemplo, Azure File Storage admite el protocolo SMB. Como resultado, puede asignar una unidad virtual local al recurso compartido de Azure File Storage mediante el procedimiento siguiente:
1.  Cree una cuenta de almacenamiento de archivos (por ejemplo, `mystorage`), un recurso compartido de archivos (por ejemplo, `sharejson`) y una carpeta de archivos en Azure File Storage mediante Azure Portal o Azure PowerShell.
2.  Cargue algunos archivos JSON en el recurso compartido de almacenamiento de archivos.
3.  Cree una regla de firewall de salida en el Firewall de Windows en el equipo que permite el puerto 445. Tenga en cuenta que su proveedor de servicio de Internet puede bloquear este puerto. Si recibe un error DNS (error 53) en el paso siguiente, es que no ha abierto el puerto 445 o su ISP lo bloquea.
4.  Monte el recurso compartido de Azure File Storage como una unidad local (por ejemplo `T:`) con el siguiente comando:

    ```
    net use [drive letter] \\[storage name].file.core.windows.net\[share name] /u:[storage account name] [storage account access key]
    ```

    A continuación se muestra un ejemplo:

    ```
    net use t: \\mystorage.file.core.windows.net\sharejson /u:myaccount hb5qy6eXLqIdBj0LvGMHdrTiygkjhHDvWjUZg3Gu7bubKLg==
    ```

    Puede encontrar la clave de la cuenta de almacenamiento y la clave de acceso de la cuenta de almacenamiento principal o secundaria en la sección Claves de Configuración en Azure Portal.


5.  Ahora puede acceder a los archivos JSON con el nombre del recurso compartido, tal como se muestra en el ejemplo siguiente:

    ```tsql
    SELECT book.* FROM
     OPENROWSET(BULK N't:\books\books.json', SINGLE_CLOB) AS json
     CROSS APPLY OPENJSON(BulkColumn)
     WITH( id nvarchar(100), name nvarchar(100), price float,
        pages_i int, author nvarchar(100)) AS book
    ```

Para más información sobre Azure File Storage, vea [File Storage](https://azure.microsoft.com/en-us/services/storage/files/).

## <a name="import-json-documents-from-azure-blob-storage"></a>Importar documentos JSON desde Azure Blob Storage

Puede cargar archivos directamente en Azure SQL Database desde Azure Blob Storage con el comando BULK INSERT de T-SQL y la función OPENROWSET.

En primer lugar, cree el origen de datos externo, como se muestra en el ejemplo siguiente.

```tsql
CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
 WITH ( TYPE = BLOB_STORAGE,
        LOCATION = 'https://myazureblobstorage.blob.core.windows.net',
        CREDENTIAL= MyAzureBlobStorageCredential);
```

A continuación, ejecute un comando BULK INSERT con la opción DATA_SOURCE.

```tsql
BULK INSERT Product
FROM 'data/product.dat'
WITH ( DATA_SOURCE = 'MyAzureBlobStorage');
```

Para más información y un ejemplo de OPENROWSET, vea [Loading files from Azure Blob Storage into Azure SQL Database](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/02/23/loading-files-from-azure-blob-storage-into-azure-sql-database/) (Cargar archivos desde Azure Blob Storage en Azure SQL Database).

## <a name="parse-json-documents-into-rows-and-columns"></a>Analizar documentos JSON en filas y columnas
En lugar de leer un archivo completo de JSON como un valor único, puede interesarme analizarlo y devolver los libros del archivo y sus propiedades en filas y columnas. En este ejemplo se utiliza un archivo JSON que contiene una lista de libros tomados de [este sitio](https://github.com/tamingtext/book/blob/master/apache-solr/example/exampledocs/books.json).

En el ejemplo más simple, solo puede cargar toda la lista desde el archivo. 

```tsql
SELECT value
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
```

OPENROWSET lee un solo valor de texto del archivo, lo devuelve como BulkColumn y lo pasa a la función OPENJSON. OPENJSON itera a través de la matriz de objetos JSON de la matriz BulkColumn y devuelve un libro, con formato JSON, en cada fila:

```
{"id" : "978-0641723445″, "cat" : ["book","hardcover"], "name" : "The Lightning Thief", … 
{"id" : "978-1423103349″, "cat" : ["book","paperback"], "name" : "The Sea of Monsters", … 
{"id" : "978-1857995879″, "cat" : ["book","paperback"], "name" : "Sophie’s World : The Greek … 
{"id" : "978-1933988177″, "cat" : ["book","paperback"], "name" : "Lucene in Action, Second … 
```

La función OPENJSON puede analizar el contenido JSON y transformarlo en una tabla o un conjunto de resultados. En el ejemplo siguiente se carga el contenido, se analiza el JSON cargado y se devuelven los cinco campos como columnas:

```tsql
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

## <a name="learn-more-about-built-in-json-support-in-sql-server"></a>Más información sobre la compatibilidad integrada de JSON en SQL Server  
 [Entradas de blog del administrador de programas de Microsoft Jovan Popovic](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## <a name="see-also"></a>Vea también
[Convertir datos JSON en filas y columnas con OPENJSON](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)


