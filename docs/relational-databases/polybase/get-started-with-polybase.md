---
title: "Introducción a PolyBase | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 5/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- PolyBase
- PolyBase, getting started
- Hadoop import
- Hadoop export
- Azure blob storage import
- Azure blob storage export
- Hadoop import, PolyBase getting started
- Hadoop export, Polybase getting started
ms.assetid: c71ddc50-b4c7-416c-9789-264671bd9ecb
caps.latest.revision: 78
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 3fc2a681f001906cf9e819084679db097bca62c7
ms.openlocfilehash: 59bf4021617603f0720c23ca192f4ddb65aa6834
ms.contentlocale: es-es
ms.lasthandoff: 05/31/2017

---
# <a name="get-started-with-polybase"></a>Introducción a PolyBase
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tema contiene los conceptos básicos acerca de cómo ejecutar PolyBase en una instancia de SQL Server.
  
 Después de realizar los pasos siguientes:  
  
-   Instalará PolyBase y podrá ejecutarlo en el servidor.  
  
-   Contará con ejemplos de instrucciones que crean objetos PolyBase.  
  
-   Sabrá cómo administrar objetos PolyBase en SQL Server Management Studio (SSMS).  
  
-   Dispondrá de ejemplos de consultas que utilizan objetos PolyBase.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Una instancia de [(64 bits) de SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) con lo siguiente:  
  
-   Microsoft .NET Framework 4.5.  
  
-   La versión de Oracle Java SE RunTime Environment (JRE) 7.51 o una superior (64 bits). (Tanto [JRE](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) como [Server JRE](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) funcionarán). Vaya a la página de [descargas de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/index.html). El programa de instalación generará un error si JRE no está presente.   
  
-   Memoria mínima: 4 GB.  
  
-   Espacio disponible en disco duro mínimo: 2 GB.    
-   La conectividad TCP/IP debe estar habilitada. (Vea [Habilitar o deshabilitar un protocolo de red de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)).  
  
 
 Un origen de datos externo, como uno de los siguientes:  
  
-   Un clúster de Hadoop. Para saber qué versiones son compatibles, vea [Configurar PolyBase](#supported).  

-   Almacenamiento de blobs de Azure

> [!NOTE]
>   Si va a usar la funcionalidad de aplicación de cálculos en Hadoop, deberá asegurarse de que el clúster de Hadoop de destino tiene componentes principales de HDFS, Yarn/MapReduce con el servidor de JobHistory habilitado. PolyBase envía la consulta de la aplicación a través de MapReduce y extrae el estado desde el servidor JobHistory. Sin alguno de los componentes se producirá un error en la consulta. 

## <a name="install-polybase"></a>Instalación de PolyBase  
 Si no ha instalado PolyBase, consulte [instalación de PolyBase](../../relational-databases/polybase/polybase-installation.md).  
  
### <a name="how-to-confirm-installation"></a>Cómo confirmar la instalación  
 Después de la instalación, ejecute el siguiente comando para confirmar que se ha instalado correctamente PolyBase. Si PolyBase está instalado, devuelve 1; en caso contrario, 0.  
  
```tsql  
SELECT SERVERPROPERTY ('IsPolybaseInstalled') AS IsPolybaseInstalled;  
```  
  
##  <a name="supported"></a> Configure PolyBase  
 Después de instalar, debe configurar SQL Server para utilizar la versión de Hadoop o almacenamiento de blobs de Azure. PolyBase es compatible con dos proveedores de Hadoop: Hortonworks Data Platform (HDP) y Cloudera Distributed Hadoop (CDH).  Los orígenes de datos externos admitidos son:  
  
-   Hortonworks HDP 1.3 en Linux y Windows Server  
  
-   Hortonworks HDP 2.1: 2.6 en Linux

-   Hortonworks HDP 2.1 - 2.3 en Windows Server  
  
-   Cloudera CDH 4.3 en Linux  
  
-   Cloudera CDH 5.1 – 5.5, 5.11 5.9 en Linux  
  
-   Almacenamiento de blobs de Azure  
  
>  [!NOTE]
> Solo se admite la conectividad de Azure Data Lake Store en Azure SQL Data Warehouse.
  
### <a name="external-data-source-configuration"></a>Configuración del origen de datos externo  
  
1.  Ejecute la “conectividad de hadoop” [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) y establezca un valor adecuado. De forma predeterminada, la conectividad de hadoop se establece en 7. Para hallar el valor, vea [Configuración de PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
      ```tsql  
    -- Values map to various external data sources.  
    -- Example: value 7 stands for Azure blob storage and Hortonworks HDP 2.3 on Linux.  
    sp_configure @configname = 'hadoop connectivity', @configvalue = 7;   
    GO   
  
    RECONFIGURE   
    GO   
    ```  
  
2.  Debe reiniciar SQL Server con **services.msc**. Al reiniciar SQL Server, se reinician estos servicios:  
  
    -   Servicio de movimiento de datos de SQL Server PolyBase  
  
    -   Motor de SQL Server PolyBase  
  
 ![detener e iniciar los servicios de PolyBase en services.msc](../../relational-databases/polybase/media/polybase-stop-start.png "detener e iniciar los servicios de PolyBase en services.msc")  
  
### <a name="pushdown-configuration"></a>Aplicación de la configuración  
 Para mejorar el rendimiento de las consultas, habilite el cálculo de la aplicación para un clúster de Hadoop:  
  
1.  Busque el archivo **yarn-site.xml** en la ruta de acceso de instalación de SQL Server. Normalmente, la ruta de acceso es:  
  
    ```  
  
    C:Program FilesMicrosoft SQL ServerMSSQL13.MSSQLSERVERMSSQLBinnPolybaseHadoopconf  
  
    ```  
  
2.  En el equipo de Hadoop, busque el archivo análogo en el directorio de configuración de Hadoop. En el archivo, busque y copie el valor de la clave de configuración yarn.application.classpath.  
  
3.  En el equipo de SQL Server, en el **archivo yarn.site.xml,** busque la propiedad **yarn.application.classpath** . Pegue el valor de la máquina de Hadoop en el elemento de valor.  
  
4. Para todas las versiones 5.X de CDH, deberá agregar los parámetros de configuración mapreduce.application.classpath al final del archivo yarn.site.xml o en el archivo mapred-site.xml. HortonWorks incluye estas configuraciones dentro de las configuraciones yarn.application.classpath. Consulte [PolyBase configuration](../../relational-databases/polybase/polybase-configuration.md) (Configuración de PolyBase) para obtener ejemplos.

 
## <a name="scale-out-polybase"></a>Escalado horizontal de PolyBase  
 La característica de grupos de PolyBase permite crear un clúster de instancias de SQL Server para procesar grandes conjuntos de datos a partir de orígenes de datos externos en un modo de escalado horizontal para mejorar el rendimiento de las consultas.  
  
1.  Instale SQL Server con PolyBase en varias máquinas.  
  
2.  Seleccione una instancia de SQL Server como nodo principal.  
  
3.  Ejecute [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)para agregar otras instancias como nodos de ejecución.  
  
    ```  
    -- Enter head node details:   
    -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';  
  
    ```  
  
4.  Reinicie el servicio de movimiento de datos de PolyBase en los nodos de ejecución.  
  
 Para obtener más información, vea [PolyBase scale-out groups](../../relational-databases/polybase/polybase-scale-out-groups.md)(Grupos de escalado horizontal de PolyBase).  
  
## <a name="create-t-sql-objects"></a>Creación de objetos de T-SQL  
 Crear objetos de función del origen de datos externo, Hadoop o almacenamiento de Azure.  
  
### <a name="hadoop"></a>Hadoop  
  
```sql  
-- 1: Create a database scoped credential.  
-- Create a master key on the database. This is required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- 2: Create a database scoped credential  for Kerberos-secured Hadoop clusters.  
-- IDENTITY: the Kerberos user name.  
-- SECRET: the Kerberos password  
  
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1   
WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
  
-- 3:  Create an external data source.  
-- LOCATION (Required) : Hadoop Name Node IP address and port.  
-- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
-- CREDENTIAL (Optional):  the database scoped credential, created above.  
  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
        TYPE = HADOOP,   
        LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',   
        RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',   
        CREDENTIAL = HadoopUser1        
);  
  
-- 4: Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).    
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
-- 5:  Create an external table pointing to data stored in Hadoop.  
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
  
-- 6:  Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
### <a name="azure-blob-storage"></a>Almacenamiento de blobs de Azure  
  
```sql  
--1: Create a master key on the database.  
-- Required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- Create a database scoped credential  for Azure blob storage.  
-- IDENTITY: any string (this is not used for authentication to Azure storage).  
-- SECRET: your Azure storage account key.  
  
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential   
WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';  
  
--2:  Create an external data source.  
-- LOCATION:  Azure account storage account name and blob container name.  
-- CREDENTIAL: The database scoped credential created above.  
  
CREATE EXTERNAL DATA SOURCE AzureStorage with (  
        TYPE = HADOOP,   
        LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
        CREDENTIAL = AzureStorageCredential  
);  
  
--3:  Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).  
  
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
--4: Create an external table.  
-- The external table points to data stored in Azure storage.  
-- LOCATION: path to a file or directory that contains the data (relative to the blob container).  
-- To point to all files under the blob container, use LOCATION='/'   
  
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
  
--5: Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
## <a name="polybase-queries"></a>Consultas de PolyBase  
 PolyBase es adecuado para realizar tres funciones:  
  
-   Realizar consultas ad hoc en tablas externas  
  
-   Importar datos  
  
-   Exportar datos  
  
### <a name="query-examples"></a>Ejemplos de consultas  
  
-   Consultas ad hoc  
  
    ```tsql  
    -- PolyBase Scenario 1: Ad-Hoc Query joining relational with Hadoop data   
    -- Select customers who drive faster than 35 mph: joining structured customer data stored   
    -- in SQL Server with car sensor data stored in Hadoop.  
    SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,   
            Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
    FROM Insured_Customers, CarSensor_Data  
    WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35   
    ORDER BY CarSensor_Data.Speed DESC  
    OPTION (FORCE EXTERNALPUSHDOWN);    -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
    ```  
  
-   Importar datos  
  
    ```tsql  
    -- PolyBase Scenario 2: Import external data into SQL Server.  
    -- Import data for fast drivers into SQL Server to do more in-depth analysis and  
    -- leverage Columnstore technology.  
  
    SELECT DISTINCT   
            Insured_Customers.FirstName, Insured_Customers.LastName,   
            Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
    INTO Fast_Customers from Insured_Customers INNER JOIN   
    (  
            SELECT * FROM CarSensor_Data where Speed > 35   
    ) AS SensorD  
    ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
    ORDER BY YearlyIncome  
  
    CREATE CLUSTERED COLUMNSTORE INDEX CCI_FastCustomers ON Fast_Customers;  
    ```  
  
-   Exportación de datos  
  
    ```  
    -- PolyBase Scenario 3: Export data from SQL Server to Hadoop.  
  
    -- Enable INSERT into external table  
    sp_configure ‘allow polybase export’, 1;  
    reconfigure  
  
    -- Create an external table.   
    CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
            [FirstName] char(25) NOT NULL,   
            [LastName] char(25) NOT NULL,   
            [YearlyIncome] float NULL,   
            [MaritalStatus] char(1) NOT NULL  
    )  
    WITH (  
            LOCATION='/old_data/2009/customerdata',  
            DATA_SOURCE = HadoopHDP2,  
            FILE_FORMAT = TextFileFormat,  
            REJECT_TYPE = VALUE,  
            REJECT_VALUE = 0  
    );  
  
    -- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
    INSERT INTO dbo.FastCustomer2009  
    SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
    ON (T1.CustomerKey = T2.CustomerKey)  
    WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
    ```  
  
## <a name="managing-polybase-objects-in-ssms"></a>Administración de objetos PolyBase en SSMS  
 En SSMS, las tablas externas se muestran en una carpeta independiente llamada " **Tablas externas**". Los orígenes de datos y los formatos de archivo externos se encuentran en subcarpetas de **Recursos externos**.  
  
 ![Objetos PolyBase en SSMS](../../relational-databases/polybase/media/polybase-management.png "Objetos PolyBase en SSMS")  
  
## <a name="troubleshooting"></a>Solucionar problemas  
 Use DMV para solucionar problemas de rendimiento y de consultas. Para obtener más información, vea [PolyBase troubleshooting](../../relational-databases/polybase/polybase-troubleshooting.md)(Solución de problemas de PolyBase).  
  
 Después de actualizar de SQL Server 2016 RC1 a RC2 o RC3, las consultas pueden producir errores. Para obtener más información y saber cómo solucionarlo, vea [Notas de la versión de SQL Server 2016](../../sql-server/sql-server-2016-release-notes.md) y busque "PolyBase".  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para entender la característica de escalado horizontal, vea [PolyBase scale-out groups](../../relational-databases/polybase/polybase-scale-out-groups.md)(Grupos de escalado horizontal de PolyBase).  Para supervisar PolyBase, consulte [PolyBase troubleshooting](../../relational-databases/polybase/polybase-troubleshooting.md)(Solución de problemas de PolyBase). Para solucionar problemas de rendimiento de PolyBase, consulte [PolyBase troubleshooting with dynamic management views](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80).  
  
## <a name="see-also"></a>Vea también  
 [Guía de PolyBase](../../relational-databases/polybase/polybase-guide.md)   
 [Grupos de escalado horizontal de PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md)   
 [Procedimientos almacenados de PolyBase](http://msdn.microsoft.com/library/a522b303-bd1b-410b-92d1-29c950a15ede)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  

