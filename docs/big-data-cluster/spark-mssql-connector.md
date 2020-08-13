---
title: Conectar Spark a SQL Server
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo usar el conector de Apache Spark para SQL Server y Azure SQL a fin de leer y escribir en SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-bdc
ms.openlocfilehash: 3cb36c4bdddfaa97b9b6c08015308799d54cb0dc
ms.sourcegitcommit: 56f6892b3795da308d226d4b3c5c859ead2e830a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2020
ms.locfileid: "86438077"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-apache-spark-connector-for-sql-server-and-azure-sql"></a>Procedimientos para leer y escribir en SQL Server desde Spark mediante el conector de Apache Spark para SQL Server y Azure SQL

Un patrón clave de uso de macrodatos es un procesamiento de datos de gran volumen en Spark, seguido de la escritura de los datos en SQL Server para acceder a las aplicaciones de línea de negocio. Estos patrones de uso se benefician de un conector que usa las optimizaciones de SQL clave y proporciona un mecanismo de escritura eficaz.

En este artículo se proporciona información general sobre la interfaz del conector de Apache Spark para SQL Server y Azure SQL y la creación de instancias a fin de usarlas con el modo sin AD y el modo con AD. Después, se proporciona un ejemplo de cómo usar el conector de Apache Spark para SQL Server y Azure SQL a fin de leer y escribir en las siguientes ubicaciones de un clúster de macrodatos:
1. La instancia maestra de SQL Server
1. El grupo de datos de SQL Server

   ![Diagrama del conector de Apache Spark para SQL Server y Azure SQL](./media/spark-mssql-connector/mssql-spark-connector-diagram.png)

## <a name="apache-spark-connector-for-sql-server-and-azure-sql-interface"></a>Interfaz del conector de Apache Spark para SQL Server y Azure SQL

SQL Server 2019 proporciona el [**conector de Apache Spark para SQL Server y Azure SQL**](https://github.com/microsoft/sql-spark-connector) para clústeres de macrodatos, que usa las API de escritura masiva de SQL Server para escrituras de Spark a SQL. El conector de Apache Spark para SQL Server y Azure SQL se basa en las API de origen de datos de Spark y proporciona una interfaz de conector de Spark JDBC conocida. Para los parámetros de interfaz, consulte la [documentación de Apache Spark](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html). El nombre **com.microsoft.sqlserver.jdbc.spark** hace referencia al conector de Apache Spark para SQL Server y Azure SQL. El conector de Apache Spark para SQL Server y Azure SQL admite dos modos de seguridad para conectarse con SQL Server, el modo sin Active Directory y el modo con Active Directory (AD):
### <a name="non-ad-mode"></a>Modo sin AD:
En la seguridad del modo sin AD, cada usuario tiene un nombre de usuario y una contraseña que se deben proporcionar como parámetros durante la creación de instancias del conector para realizar operaciones de lectura o escritura.
A continuación se muestra un ejemplo de creación de instancias de conector para el modo sin AD:
```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark" 

url = "jdbc:sqlserver://master-p-svc;databaseName=?;"
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("user", ?) \ 
   .option("password",?) 
writer.save() 
```
### <a name="ad-mode"></a>Modo de AD:
En la seguridad del modo de AD, una vez que un usuario ha generado un archivo keytab, tiene que proporcionar los valores `principal` y `keytab` como parámetros durante la creación de instancias del conector.

En este modo, el controlador carga el archivo keytab en los contenedores del ejecutor correspondiente. Después, los ejecutores usan el nombre de entidad de seguridad y el archivo keytab para generar un token que se utiliza para crear un conector JDBC para lectura y escritura.

A continuación se muestra un ejemplo de creación de instancias de conector para el modo de AD:
```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark"

url = "jdbc:sqlserver://master-p-svc;databaseName=?;integratedSecurity=true;authenticationScheme=JavaKerberos;" 
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("principal", ?) \ 
   .option("keytab", ?)   

writer.save() 
```

En la tabla siguiente se describen los parámetros de interfaz que han cambiado o son nuevos:

| Nombre de propiedad | Opcional | Descripción |
|---|---|---|
| **isolationLevel** | Sí | Describe el nivel de aislamiento de la conexión. El valor predeterminado del conector es **READ_COMMITTED**. |

El conector utiliza API de escritura masiva de SQL Server. El usuario puede pasar los parámetros de escritura masiva como parámetros opcionales, y el conector los pasa tal cual a la API subyacente. Para obtener más información sobre las operaciones de escritura masiva, vea [SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions).

## <a name="apache-spark-connector-for-sql-server-and-azure-sql-sample"></a>Ejemplo de conector de Apache Spark para SQL Server y Azure SQL
En el ejemplo se realizan las tareas siguientes:

- Lectura de un archivo de HDFS y realización de algún procesamiento básico.
- Escritura de la trama de datos en una instancia maestra de SQL Server como tabla de SQL y, después, lectura de la tabla en una trama de datos.
- Escritura de la trama de datos en un grupo de datos de SQL Server como tabla externa de SQL y, después, lectura de la tabla externa en una trama de datos.
### <a name="prerequisites"></a>Prerrequisitos

- Un [clúster de macrodatos de SQL Server](deploy-get-started.md)

- [Azure Data Studio](https://aka.ms/getazuredatastudio)

### <a name="create-the-target-database"></a>Creación de la base de datos de destino

1. Abra Azure Data Studio y [conéctese a la instancia maestra de SQL Server del clúster de macrodatos](connect-to-big-data-cluster.md).

1. Cree una nueva consulta y ejecute el siguiente comando para crear una base de datos de ejemplo denominada **MyTestDatabase**.

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

### <a name="load-sample-data-into-hdfs"></a>Carga de datos de muestra en HDFS

1. Descargue [AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv) en el equipo local.

1. Inicie Azure Data Studio y [conéctese a su clúster de macrodatos](connect-to-big-data-cluster.md).

1. Haga clic con el botón derecho en la carpeta HDFS en el clúster de macrodatos y seleccione **Nuevo directorio**. Asigne al directorio el nombre **spark_data**.

1. Haga clic con el botón derecho en el directorio **spark_data** y seleccione **Cargar archivos**. Cargue el archivo **AdultCensusIncome.csv**.

   ![Archivo CSV AdultCensusIncome](./media/spark-mssql-connector/spark_data.png)

### <a name="run-the-sample-notebook"></a>Ejecución del cuaderno de ejemplo

Para demostrar el uso del conector de Apache Spark para SQL Server y Azure SQL con estos datos en modo sin AD, puede descargar un cuaderno de ejemplo, abrirlo en Azure Data Studio y ejecutar cada bloque de código. Para obtener más información sobre el trabajo con cuadernos, vea [Procedimiento para usar cuadernos con SQL Server](../azure-data-studio/notebooks-guidance.md).

1. Desde una línea de comandos de PowerShell o Bash, ejecute el comando siguiente para descargar el cuaderno de ejemplo **mssql_spark_connector_non_ad_pyspark.ipynb**:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-virtualization/mssql_spark_connector_non_ad_pyspark.ipynb"
   ```

1. En Azure Data Studio, abra el archivo de cuaderno de ejemplo. Compruebe que está conectado a la puerta de enlace de HDFS/Spark para el clúster de macrodatos.

1. Ejecute cada celda de código en el ejemplo para ver el uso del conector de Apache Spark para SQL Server y Azure SQL.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos, vea [Cómo implementar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en Kubernetes](deployment-guidance.md).

¿Tiene comentarios o recomendaciones sobre características para los clústeres de macrodatos de SQL Server? [Deje una nota en Comentarios sobre clústeres de macrodatos de SQL Server](https://aka.ms/sql-server-bdc-feedback).
