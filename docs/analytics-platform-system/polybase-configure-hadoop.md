---
title: Configurar PolyBase para obtener acceso a datos externos en Hadoop | Microsoft Docs
description: Explica cómo configurar PolyBase en almacenamiento de datos paralelos para conectarse a Hadoop externo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b0a49925ec0d0592adfd131e0ab994e5e8356f95
ms.sourcegitcommit: 3e1efbe460723f9ca0a8f1d5a0e4a66f031875aa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2018
ms.locfileid: "50236941"
---
# <a name="configure-polybase-to-access-external-data-in-hadoop"></a>Configurar PolyBase para obtener acceso a datos externos en Hadoop

El artículo explica cómo usar PolyBase en un dispositivo APS para consultar los datos externos en Hadoop.

## <a name="prerequisites"></a>Requisitos previos

PolyBase es compatible con dos proveedores de Hadoop: Hortonworks Data Platform (HDP) y Cloudera Distributed Hadoop (CDH). Hadoop sigue el patrón “Principal.Secundaria.Versión” para sus revisiones nuevas y se admiten todas las versiones dentro de una revisión principal y secundaria compatible. Se admiten los siguientes proveedores de Hadoop:
 - Hortonworks HDP 1.3 en Linux y Windows Server  
 - Hortonworks HDP 2.1 - 2.6 en Linux
 - Hortonworks HDP 2.1 - 2.3 en Windows Server  
 - Cloudera CDH 4.3 en Linux  
 - Cloudera CDH 5.1 – 5.5, 5.9 - 5.13 en Linux

### <a name="configure-hadoop-connectivity"></a>Configurar la conectividad de Hadoop

En primer lugar, configure puntos de acceso para usar el proveedor específico de Hadoop.

1. Ejecute [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) con la “conectividad de hadoop” y defina un valor adecuado para el proveedor. Para hallar el valor, consulte [Configuración de la conectividad de PolyBase](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md). 

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. Reinicie la región de APS con página de estado del servicio en [Administrador de configuración de dispositivo](launch-the-configuration-manager.md).
  
## <a id="pushdown"></a> Habilitar el cálculo de la aplicación  

Para mejorar el rendimiento de las consultas, habilite el cálculo de la aplicación para el clúster de Hadoop:  
  
1. Abra una conexión a escritorio remota al nodo de Control de PDW.

2. Busque el archivo **yarn-site.xml** en el nodo de Control. Normalmente, la ruta de acceso es:  

   ```xml  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\  
   ```  

3. En el equipo de Hadoop, busque el archivo análogo en el directorio de configuración de Hadoop. En el archivo, busque y copie el valor de la clave de configuración yarn.application.classpath.  
  
4. En el nodo de Control, en el **archivo yarn.site.xml,** encontrar el **yarn.application.classpath** propiedad. Pegue el valor de la máquina de Hadoop en el elemento de valor.  
  
5. Para todas las versiones 5.X de CDH, deberá agregar los parámetros de configuración mapreduce.application.classpath al final del archivo yarn.site.xml o en el archivo mapred-site.xml. HortonWorks incluye estas configuraciones dentro de las configuraciones yarn.application.classpath. Consulte [PolyBase configuration](../relational-databases/polybase/polybase-configuration.md) (Configuración de PolyBase) para obtener ejemplos.

## <a name="configure-an-external-table"></a>Configurar una tabla externa

Para consultar los datos en el origen de datos de Hadoop, debe definir una tabla externa para usar en las consultas de Transact-SQL. Los pasos siguientes describen cómo configurar la tabla externa.

1. Cree una clave maestra en la base de datos. Es necesario para cifrar el secreto de credencial.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

2. Cree una credencial de ámbito de base de datos para los clústeres de Hadoop protegidos mediante Kerberos.

   ```sql
   -- IDENTITY: the Kerberos user name.  
   -- SECRET: the Kerberos password  
   CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
   WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
   ```

3. Cree un origen de datos externo con [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md).

   ```sql
   -- LOCATION (Required) : Hadoop Name Node IP address and port.  
   -- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
   -- CREDENTIAL (Optional):  the database scoped credential, created above.  
   CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
         TYPE = HADOOP,
         LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',
         RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',
         CREDENTIAL = HadoopUser1
   );  
   ```

4. Cree un formato de archivo externo con [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md).

   ```sql
   -- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

5. Cree una tabla externa que señale a los datos almacenados en Hadoop con [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md). En este ejemplo, los datos externos contienen datos de sensor del vehículo.

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
         DATA_SOURCE = MyHadoopCluster,  
         FILE_FORMAT = TextFileFormat  
   );  
   ```

6. Cree estadísticas en una tabla externa.

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

La siguiente consulta ad hoc combinaciones relacionales con datos de Hadoop. Selecciona a los clientes que la unidad con más rapidez que 35 mph, combinar los datos estructurados del cliente almacenados los puntos de acceso con datos de sensor de vehículo almacenados en Hadoop.  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
OPTION (FORCE EXTERNALPUSHDOWN);   -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
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

La consulta siguiente exporta los datos desde puntos de acceso a Hadoop. Se puede usar para archivar los datos relacionales en Hadoop mientras todavía poder consultarlo.

```sql
-- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = HadoopHDP2,  
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

Para ver de configuración de seguridad de Hadoop [configurar la seguridad de Hadoop](polybase-configure-hadoop-security.md).<br>
Para más información sobre PolyBase, consulte [¿Qué es PolyBase?](../relational-databases/polybase/polybase-guide.md) 
 
