---
title: Acceso en bloque a datos en Azure Blob Storage
ms.description: Transact-SQL examples that use BULK INSERT and OPENROWSET to access data in an Azure Blob storage account.
ms.date: 10/22/2019
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
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 08e81abbc21671881affc80fc9b7f0346cd490f7
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056004"
---
# <a name="examples-of-bulk-access-to-data-in-azure-blob-storage"></a>Ejemplos de Acceso en bloque a datos en Azure Blob Storage

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Las instrucciones `BULK INSERT` y `OPENROWSET` pueden obtener acceso directamente a un archivo en Azure Blob Storage. En los ejemplos siguientes se usan datos de un archivo CSV (valores separados por comas) (denominado `inv-2017-01-19.csv`), almacenado en un contenedor (denominado `Week3`), almacenado en una cuenta de almacenamiento (denominada `newinvoices`). Se puede usar la ruta de acceso al archivo de formato, pero no se incluye en estos ejemplos.

El acceso masivo a Azure Blob Storage desde SQL Server, necesita al menos [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.

> [!IMPORTANT]
> Todas las rutas de acceso al contenedor y a los archivos de blob son `CASE SENSITIVE`. Si no es correcto, es posible que se devuelva el error "No se puede realizar la carga masiva. El archivo "file.csv" no existe o no tiene derechos de acceso al archivo."

## <a name="create-the-credential"></a>Crear la credencial

Todos los ejemplos siguientes requieren una credencial con ámbito de base de datos que haga referencia a una firma de acceso compartido.

> [!IMPORTANT]
> El origen de datos externo debe crearse con una credencial con ámbito de base de datos que use la identidad `SHARED ACCESS SIGNATURE`. Para crear una firma de acceso compartido para la cuenta de almacenamiento, vea la propiedad **Firma de acceso compartido** en la página de propiedades de la cuenta de almacenamiento, en Azure Portal. Para más información sobre las firmas de acceso compartido, vea [Uso de Firmas de acceso compartido (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1). Para más información sobre las credenciales, vea [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

Cree una credencial con ámbito de base de datos mediante `IDENTITY` que debe ser `SHARED ACCESS SIGNATURE`. Use el token de SAS creado para la cuenta de almacenamiento de blobs. Compruebe que el token de SAS no tenga un valor `?` inicial, que tenga al menos permiso de lectura sobre el objeto que debe cargarse y que el período de expiración sea válido (todas las fechas están en hora UTC).

Por ejemplo:

```sql
CREATE DATABASE SCOPED CREDENTIAL UploadInvoices
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'sv=2018-03-28&ss=b&srt=sco&sp=rwdlac&se=2019-08-31T02:25:19Z&st=2019-07-30T18:25:19Z&spr=https&sig=KS51p%2BVnfUtLjMZtUTW1siyuyd2nlx294tL0mnmFsOk%3D';
```

## <a name="accessing-data-in-a-csv-file-referencing-an-azure-blob-storage-location"></a>Acceso a datos en un archivo CSV que hace referencia a una ubicación de Azure Blob Storage

En el ejemplo siguiente se usa un origen de datos externo que apunta a una cuenta de almacenamiento de Azure, denominada `MyAzureInvoices`.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net',
        CREDENTIAL = UploadInvoices
    );
```

Después, la instrucción agrega `OPENROWSET` el nombre del contenedor (`week3`) a la descripción del archivo. El archivo se denomina `inv-2017-01-19.csv`.

```sql
SELECT * FROM OPENROWSET(
   BULK 'week3/inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   FORMAT = 'CSV',
   FORMATFILE='invoices.fmt',
   FORMATFILE_DATA_SOURCE = 'MyAzureInvoices'
   ) AS DataFile;   
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
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = UploadInvoices
    );
```

Después, la instrucción `OPENROWSET` no incluye el nombre del contenedor en la descripción del archivo:

```sql
SELECT * FROM OPENROWSET(
   BULK 'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoicesContainer',
   FORMAT = 'CSV',
   FORMATFILE='invoices.fmt',
   FORMATFILE_DATA_SOURCE = 'MyAzureInvoices'
   ) AS DataFile;
```

Con `BULK INSERT`, no use el nombre del contenedor en la descripción del archivo:

```sql
BULK INSERT Colors2
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoicesContainer',
      FORMAT = 'CSV');
```

## <a name="see-also"></a>Consulte también

- [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)
- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)
- [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
