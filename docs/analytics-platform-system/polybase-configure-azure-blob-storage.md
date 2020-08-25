---
title: Uso de polybase para acceder a datos externos en Azure BLOB Storage
description: Explica cómo configurar polybase en el almacenamiento de datos paralelos para conectarse a Hadoop externo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ea61ea7e6983f9601783957eee6776f36eccfb4
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400726"
---
# <a name="configure-polybase-to-access-external-data-in-azure-blob-storage"></a>Configuración de polybase para acceder a datos externos en Azure BLOB Storage

En el artículo se explica cómo usar polybase en una instancia de SQL Server para consultar datos externos en Azure BLOB Storage.

> [!NOTE]
> APS actualmente solo admite Azure BLOB Storage estándar de uso general (LRS) con redundancia local (LRS).

## <a name="prerequisites"></a>Prerrequisitos

 - Almacenamiento de blobs de Azure en su suscripción.
 - Un contenedor creado en el almacenamiento de blobs de Azure.

### <a name="configure-azure-blob-storage-connectivity"></a>Configuración de la conectividad de almacenamiento de blobs de Azure

En primer lugar, configure APS para usar el almacenamiento de blobs de Azure.

1. Ejecute [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) con "conectividad de Hadoop" establecida en un proveedor de almacenamiento de blobs de Azure. Para hallar el valor de los proveedores, consulte [Configuración de la conectividad de PolyBase](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure Blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. Reinicie la región APS mediante la página estado del servicio en el [Configuration Manager del dispositivo](launch-the-configuration-manager.md).
  
## <a name="configure-an-external-table"></a>Configurar una tabla externa

Para consultar los datos en el almacenamiento de blobs de Azure, debe definir una tabla externa que se usará en las consultas de Transact-SQL. Los pasos siguientes describen cómo configurar la tabla externa.

1. Cree una clave maestra en la base de datos. Es necesario cifrar el secreto de la credencial.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

1. Cree una credencial con ámbito de base de datos para el almacenamiento de blobs de Azure.

   ```sql
   -- IDENTITY: any string (this is not used for authentication to Azure storage).  
   -- SECRET: your Azure storage account key.  
   CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
   WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';
   ```

1. Cree un origen de datos externo con [Crear origen de datos externo](../t-sql/statements/create-external-data-source-transact-sql.md).

   ```sql
   -- LOCATION:  Azure account storage account name and blob container name.  
   -- CREDENTIAL: The database scoped credential created above.  
   CREATE EXTERNAL DATA SOURCE AzureStorage with (  
         TYPE = HADOOP,
         LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
         CREDENTIAL = AzureStorageCredential  
   );  
   ```

1. Cree un formato de archivo externo con [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md).

   ```sql
   -- FORMAT TYPE: Type of format in Azure Blob storage (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   -- In this example, the files are pipe (|) delimited
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

1. Cree una tabla externa que señale a los datos almacenados en Azure Storage con [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md). En este ejemplo, los datos externos contienen datos de sensor de vehículo.

   ```sql
   -- LOCATION: path to file or directory that contains the data (relative to HDFS root).  
   CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
         [SensorKey] int NOT NULL,
         [CustomerKey] int NOT NULL,
         [GeographyKey] int NULL,
         [Speed] float NOT NULL,
         [YearMeasured] int NOT NULL  
   )  
   WITH (LOCATION='/Demo/',
         DATA_SOURCE = AzureStorage,  
         FILE_FORMAT = TextFileFormat  
   );  
   ```

1. Cree estadísticas en una tabla externa.

   ```sql
   CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
   ```

## <a name="polybase-queries"></a>Consultas de PolyBase

PolyBase es adecuado para realizar tres funciones:  
  
- Consultas ad hoc en tablas externas.  
- Importar datos.  
- Exportar datos.  

Las siguientes consultas proporcionan un ejemplo con datos de sensor de vehículo ficticios.

### <a name="ad-hoc-queries"></a>Consultas ad hoc  

La siguiente consulta ad hoc combina relacional con los datos de Azure BLOB Storage. Selecciona los clientes que tienen más de 35 mph y combinan datos de clientes estructurados almacenados en SQL Server con datos de sensor de automóviles almacenados en Azure BLOB Storage.  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
```  

### <a name="importing-data"></a>Importar datos  

La siguiente consulta importa datos externos en APS. En este ejemplo se importan los datos de los controladores rápidos en APS para realizar análisis más profundos. Para mejorar el rendimiento, aprovecha la tecnología de almacén de columnas en APS.  

```sql
CREATE TABLE Fast_Customers
WITH
(CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH (CustomerKey))
AS
SELECT DISTINCT
      Insured_Customers.CustomerKey, Insured_Customers.FirstName, Insured_Customers.LastName,   
      Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
from Insured_Customers INNER JOIN   
(  
      SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
```  

### <a name="exporting-data"></a>Exportación de datos  

La siguiente consulta exporta datos de APS a Azure BLOB Storage. Se puede usar para archivar datos relacionales en el almacenamiento de blobs de Azure y, al mismo tiempo, poder consultarlos.

```sql
-- Export data: Move old data to Azure Blob storage while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = AzureStorage,  
      FILE_FORMAT = TextFileFormat
)  
AS
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  

## <a name="view-polybase-objects-in-ssdt"></a>Ver objetos de polybase en SSDT  

En SQL Server Data Tools, las tablas externas se muestran en una carpeta independiente **tablas externas**. Los orígenes de datos y los formatos de archivo externos se encuentran en subcarpetas de **Recursos externos**.  
  
![Objetos polybase en SSDT](media/polybase/external-tables-datasource.png)  

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre PolyBase, consulte [¿Qué es PolyBase?](../relational-databases/polybase/polybase-guide.md) 

