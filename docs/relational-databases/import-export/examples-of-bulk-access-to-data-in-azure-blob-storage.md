---
title: Ejemplos de acceso masivo a datos en Azure Blob Storage | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], from Azure blob storage
- Azure blob storage, bulk import to SQL Server
- BULK INSERT, Azure blob storage
- OPENROWSET, Azure blob storage
ms.assetid: f7d85db3-7a93-400e-87af-f56247319ecd
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7bbc70dbfec864052c4c877794561c8692cdfcfb
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560412"
---
# <a name="examples-of-bulk-access-to-data-in-azure-blob-storage"></a>Ejemplos de acceso masivo a datos en Azure Blob Storage
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Las instrucciones `BULK INSERT` y `OPENROWSET` pueden obtener acceso directamente a un archivo en Azure Blob Storage. En los ejemplos siguientes se usan datos de un archivo CSV (valores separados por comas) (denominado `inv-2017-01-19.csv`), almacenado en un contenedor (denominado `Week3`), almacenado en una cuenta de almacenamiento (denominada `newinvoices`). Se puede usar la ruta de acceso al archivo de formato, pero no se incluye en estos ejemplos. 

El acceso masivo a Azure Blob Storage desde SQL Server, necesita al menos [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.

>  [!IMPORTANT]
>  Todas las rutas de acceso al contenedor y a los archivos de blob son `CASE SENSITIVE`. Si no es correcto, es posible que se devuelva el error "No se puede realizar la carga masiva. El archivo "file.csv" no existe o no tiene derechos de acceso al archivo."
"


## <a name="create-the-credential"></a>Crear la credencial   
   
Todos los ejemplos siguientes requieren una credencial con ámbito de base de datos que haga referencia a una firma de acceso compartido.   

>  [!IMPORTANT]
>  El origen de datos externo debe crearse con una credencial con ámbito de base de datos que use la identidad `SHARED ACCESS SIGNATURE`. Para crear una firma de acceso compartido para la cuenta de almacenamiento, vea la propiedad **Firma de acceso compartido** en la página de propiedades de la cuenta de almacenamiento, en Azure Portal. Para más información sobre las firmas de acceso compartido, vea [Uso de Firmas de acceso compartido (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1). Para más información sobre las credenciales, vea [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
 
Cree una credencial con ámbito de base de datos mediante `IDENTITY` que debe ser `SHARED ACCESS SIGNATURE`. Use el secreto de Azure Portal. Por ejemplo:  

```sql
CREATE DATABASE SCOPED CREDENTIAL UploadInvoices  
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'QLYMgmSXMklt%2FI1U6DcVrQixnlU5Sgbtk1qDRakUBGs%3D';
```


## <a name="accessing-data-in-a-csv-file-referencing-an-azure-blob-storage-location"></a>Acceso a datos en un archivo CSV que hace referencia a una ubicación de Azure Blob Storage   
En el ejemplo siguiente se usa un origen de datos externo que apunta a una cuenta de almacenamiento de Azure, denominada `newinvoices`.   
```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net', 
        CREDENTIAL = UploadInvoices  
    );
```   

Después, la instrucción agrega `OPENROWSET` el nombre del contenedor (`week3`) a la descripción del archivo. El archivo se denomina `inv-2017-01-19.csv`.
```sql     
SELECT * FROM OPENROWSET(
   BULK  'week3/inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   SINGLE_CLOB) AS DataFile;
```

Con `BULK INSERT`, use el contenedor y la descripción del archivo:

```sql
BULK INSERT Colors2
FROM 'week3/inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
      FORMAT = 'CSV'); 
```

## <a name="accessing-data-in-a-csv-file-referencing-a-container-in-an-azure-blob-storage-location"></a>Acceso a datos en un archivo CSV que hace referencia a un contenedor en una ubicación de Azure Blob Storage   

En el ejemplo siguiente se usa un origen de datos externo que apunta a un contenedor (denominado`week3`) en cuenta de almacenamiento de Azure.   
```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoicesContainer
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3', 
        CREDENTIAL = UploadInvoices  
    );
```  
  
Después, la instrucción `OPENROWSET` no incluye el nombre del contenedor en la descripción del archivo:
```sql
SELECT * FROM OPENROWSET(
   BULK  'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoicesContainer',
   SINGLE_CLOB) AS DataFile;
```   

Con `BULK INSERT`, no use el nombre del contenedor en la descripción del archivo: 

```sql
BULK INSERT Colors2
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoicesContainer',
      FORMAT = 'CSV'); 
```

## <a name="see-also"></a>Ver también   

[CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
[CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)   
[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)   
[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)   

