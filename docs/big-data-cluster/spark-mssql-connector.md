---
title: Conectar Spark a SQL Server
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo usar el conector de Spark MSSQL en Spark para leer y escribir en SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5b603e91e2dffae034dd9d66a1bcd3e5f812a308
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67957837"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-mssql-spark-connector"></a>Cómo leer y escribir en SQL Server de Spark mediante el conector de Spark MSSQL

Un patrón clave de uso de macrodatos es un procesamiento de datos de gran volumen en Spark, seguido de la escritura de los datos en SQL Server para acceder a las aplicaciones de línea de negocio. Estos patrones de uso se benefician de un conector que usa las optimizaciones de SQL clave y proporciona un mecanismo de escritura eficaz.

En este artículo se proporciona un ejemplo de cómo usar el conector de Spark MSSQL para leer y escribir en las siguientes ubicaciones de un clúster de macrodatos:

1. La instancia maestra de SQL Server
1. El grupo de datos de SQL Server

   ![Diagrama del conector de Spark MSSQL](./media/spark-mssql-connector/mssql-spark-connector-diagram.png)

En el ejemplo se realizan las tareas siguientes:

- Lectura de un archivo de HDFS y realización de algún procesamiento básico.
- Escritura de la trama de datos en una instancia maestra de SQL Server como tabla de SQL y, después, lectura de la tabla en una trama de datos.
- Escritura de la trama de datos en un grupo de datos de SQL Server como tabla externa de SQL y, después, lectura de la tabla externa en una trama de datos.

## <a name="mssql-spark-connector-interface"></a>Interfaz del conector de Spark MSSQL

SQL Server 2019 (versión preliminar) proporciona el **conector de Spark MSSQL** para clústeres de macrodatos, que usa las API de escritura masiva de SQL Server para escrituras de Spark a SQL. El conector de Spark MSSQL se basa en las API de origen de datos de Spark y proporciona una interfaz de conector de Spark JDBC conocida. Para los parámetros de interfaz, consulte la [documentación de Apache Spark](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html). El nombre **com.microsoft.sqlserver.jdbc.spark** hace referencia al conector de Spark MSSQL.

En la tabla siguiente se describen los parámetros de interfaz que han cambiado o son nuevos:

| Nombre de propiedad | Opcional | Descripción |
|---|---|---|
| **isolationLevel** | Sí | Describe el nivel de aislamiento de la conexión. El valor predeterminado del conector MSSQLSpark es **READ_COMMITTED** |

El conector utiliza API de escritura masiva de SQL Server. El usuario puede pasar los parámetros de escritura masiva como parámetros opcionales, y el conector los pasa tal cual a la API subyacente. Para obtener más información sobre las operaciones de escritura masiva, vea [SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions).

## <a name="prerequisites"></a>Prerequisites

- Un [clúster de macrodatos de SQL Server](deploy-get-started.md)

- [Azure Data Studio](https://aka.ms/azdata-insiders)

## <a name="create-the-target-database"></a>Creación de la base de datos de destino

1. Abra Azure Data Studio y [conéctese a la instancia maestra de SQL Server del clúster de macrodatos](connect-to-big-data-cluster.md).

1. Cree una nueva consulta y ejecute el siguiente comando para crear una base de datos de ejemplo denominada **MyTestDatabase**.

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

## <a name="load-sample-data-into-hdfs"></a>Carga de datos de muestra en HDFS

1. Descargue [AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv) en el equipo local.

1. Inicie Azure Data Studio y [conéctese a su clúster de macrodatos](connect-to-big-data-cluster.md).

1. Haga clic con el botón derecho en la carpeta HDFS en el clúster de macrodatos y seleccione **Nuevo directorio**. Asigne al directorio el nombre **spark_data**.

1. Haga clic con el botón derecho en el directorio **spark_data** y seleccione **Cargar archivos**. Cargue el archivo **AdultCensusIncome.csv**.

   ![Archivo CSV AdultCensusIncome](./media/spark-mssql-connector/spark_data.png)

## <a name="run-the-sample-notebook"></a>Ejecución del cuaderno de ejemplo

Para demostrar el uso del conector de Spark MSSQL con estos datos, puede descargar un cuaderno de ejemplo, abrirlo en Azure Data Studio y ejecutar cada bloque de código. Para obtener más información sobre el trabajo con cuadernos, vea [Uso de los cuadernos en la versión preliminar de SQL Server 2019](notebooks-guidance.md).

1. Desde una línea de comandos de PowerShell o Bash, ejecute el siguiente comando para descargar el cuaderno de ejemplo **mssql_spark_connector.ipynb**:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-virtualization/mssql_spark_connector.ipynb"
   ```

1. En Azure Data Studio, abra el archivo de cuaderno de ejemplo. Compruebe que está conectado a la puerta de enlace de HDFS/Spark para el clúster de macrodatos.

1. Ejecute cada celda de código del ejemplo para ver el uso del conector de Spark MSSQL.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos, vea [Cómo implementar clústeres de macrodatos SQL Server en Kubernetes](deployment-guidance.md).