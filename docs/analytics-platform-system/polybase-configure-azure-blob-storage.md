---
title: Configurar PolyBase para obtener acceso a datos externos en Azure Blob storage | Microsoft Docs
description: Explica cómo configurar PolyBase en almacenamiento de datos paralelos para conectarse a Hadoop externo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7bbf2dface759da63bd6b9845f4e62321b1cbe76
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63027514"
---
# <a name="configure-polybase-to-access-external-data-in-azure-blob-storage"></a>Configurar PolyBase para obtener acceso a datos externos en Azure Blob storage

El artículo explica cómo usar PolyBase en una instancia de SQL Server para consultar los datos externos en Azure Blob storage.

> [!NOTE]
> APS actualmente solo admite almacenamiento estándar de uso general v1 de redundancia (LRS) de Azure Blob.

## <a name="prerequisites"></a>Requisitos previos

 - Almacenamiento de blobs de Azure en su suscripción.
 - Creada un contenedor en el almacenamiento de blobs de Azure.

### <a name="configure-azure-blob-storage-connectivity"></a>Configurar la conectividad de almacenamiento de blobs de Azure

En primer lugar, configure puntos de acceso para usar Azure Blob storage.

1. Ejecute [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) con 'hadoop connectivity' establecido en un proveedor de almacenamiento de blobs de Azure. Para hallar el valor de los proveedores, consulte [Configuración de la conectividad de PolyBase](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure Blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. Reinicie la región de APS con página de estado del servicio en [Administrador de configuración de dispositivo](launch-the-configuration-manager.md).
  
## <a name="configure-an-external-table"></a>Configurar una tabla externa

Para consultar los datos del almacenamiento de blobs de Azure, debe definir una tabla externa para usar en consultas de Transact-SQL. Los pasos siguientes describen cómo configurar la tabla externa.

1. Cree una clave maestra en la base de datos. Es necesario para cifrar el secreto de credencial.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

1. Crear una credencial con ámbito de base de datos para el almacenamiento de blobs de Azure.

   ```sql
   -- IDENTITY: any string (this is not used for authentication to Azure storage).  
   -- SECRET: your Azure storage account key.  
   CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
   WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';
   ```

1. Cree un origen de datos externo con [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md).

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

La siguiente consulta ad hoc combinaciones relacionales con datos en Azure Blob storage. Selecciona a los clientes que la unidad con más rapidez que 35 mph, combinar los datos estructurados del cliente almacenados en SQL Server con datos del sensor de vehículo almacenados en Azure Blob storage.  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
```  

### <a name="importing-data"></a>Importar datos  

La consulta siguiente importa datos externos en puntos de acceso. En este ejemplo importa datos para controladores rápidos en puntos de acceso para realizar un análisis más profundo. Para mejorar el rendimiento, aprovecha la tecnología de almacén de columnas en los puntos de acceso.  

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

La consulta siguiente exporta los datos desde puntos de acceso a Azure Blob storage. Se puede usar para archivar datos relacionales a Azure Blob storage mientras sigue poder consultarlo.

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

## <a name="view-polybase-objects-in-ssdt"></a>Ver objetos PolyBase en SSDT  

En SQL Server Data Tools, las tablas externas se muestran en una carpeta independiente **tablas externas**. Los orígenes de datos y los formatos de archivo externos se encuentran en subcarpetas de **Recursos externos**.  
  
![Objetos PolyBase en SSDT](media/polybase/external-tables-datasource.png)  

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre PolyBase, consulte [¿Qué es PolyBase?](../relational-databases/polybase/polybase-guide.md) 

