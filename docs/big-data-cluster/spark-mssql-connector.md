---
title: Conectar Spark a SQL Server
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo usar el conector de Spark MSSQL en Spark para leer y escribir en SQL Server.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 54361f9a061169d51f11ccb130e78ba67c0a9a67
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759222"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-mssql-spark-connector"></a>Cómo leer y escribir en SQL Server de Spark mediante el conector de Spark MSSQL

Un patrón de uso de datos de gran tamaño de clave es el procesamiento de datos de gran volumen en Spark, seguido de escribir los datos en SQL Server para tener acceso a aplicaciones de línea de negocio. Estos patrones de uso de beneficiarán de un conector que utiliza la claves optimizaciones de SQL y proporciona un mecanismo eficaz de escritura.

Con los clústeres de datos grande CTP2.5 proporciona un nuevo conector de Spark MSSQL que usa SQL Server masiva escribir las API para un rendimiento de Spark a la escritura SQL. En este artículo se proporciona un ejemplo de cómo leer y escribir en SQL Server de Spark mediante el conector de Spark MSSQL. En este ejemplo, los datos se leen de HDFS en un clúster de macrodatos, procesados por Spark y, a continuación, se escriben en la instancia principal de SQL Server en el clúster con el nuevo conector de Spark MSSQL.

## <a name="mssql-spark-connector-interface"></a>Interfaz del conector de Spark MSSQL

Conector de Spark MSSQL se basa en el origen de datos de Spark API y proporciona una interfaz conocida de conector de Spark JDBC. Para los parámetros de la interfaz, consulte [documentación de Apache Spark](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html). El nombre al que hace referencia el conector de Spark MSSQL **com.microsoft.sqlserver.jdbc.spark**.

En la tabla siguiente se describe los parámetros de la interfaz que han cambiado o son nuevos:

| Nombre de propiedad | Opcional | Descripción |
|---|---|---|
| **isolationLevel** | Sí | Describe el nivel de aislamiento de la conexión. Es el valor predeterminado para el conector MSSQLSpark **READ_COMMITTED** |

El conector utiliza SQL Server masiva escribe las API. Cualquier escritura masiva parámetros pueden pasarse como parámetros opcionales por el usuario y se pasan como-es mediante el conector a la API subyacente. Para obtener más información acerca de forma masiva las operaciones de escritura, consulte [SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions).

## <a name="prerequisites"></a>Requisitos previos

- Un [clúster grande de datos de SQL Server](deploy-get-started.md).

- [Datos de Azure Studio](../azure-data-studio/download.md).

## <a name="create-the-target-database"></a>Crear la base de datos de destino

1. Abra Azure Data Studio, y [conectarse a la instancia principal de SQL Server del clúster de macrodatos](connect-to-big-data-cluster.md).

1. Cree una nueva consulta y ejecute el siguiente comando para crear una base de datos de ejemplo denominada **MyTestDatabase**.

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

## <a name="load-sample-data-into-hdfs"></a>Cargar datos de ejemplo en HDFS

1. Descargar [AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv) en el equipo local.

1. En Azure Data Studio, haga doble clic en la carpeta HDFS en el clúster de macrodatos y seleccione **nuevo directorio**. Nombre del directorio **spark_data**.

1. Haga clic con el botón derecho en el **spark_data** directorio y, a continuación, seleccione **cargar archivos**. Cargar el **AdultCensusIncome.csv** archivo.

   ![Archivo AdultCensusIncome CSV](./media/spark-mssql-connector/spark_data.png)

## <a name="run-the-sample-notebook"></a>Ejecute el cuaderno de ejemplo

Para demostrar el uso del conector de Spark MSSQL con estos datos, puede descargar un bloc de notas de ejemplo, ábralo en Azure Data Studio y ejecute cada bloque de código. Para obtener más información sobre cómo trabajar con equipos portátiles, consulte [para usar cuadernos en versión preliminar de SQL Server 2019](notebooks-guidance.md).

1. Desde una línea de comandos de PowerShell o bash, ejecute el comando siguiente para descargar el **mssql_spark_connector.ipynb** Bloc de notas de ejemplo:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/spark_to_sql/mssql_spark_connector.ipynb"
   ```

1. En Azure Data Studio, abra el archivo de Bloc de notas de ejemplo. Compruebe que está conectado a la puerta de enlace de Spark o HDFS para el clúster de macrodatos.

1. Ejecutar cada celda de código en el ejemplo para ver el uso del conector de Spark MSSQL.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de datos de gran tamaño, vea [cómo implementar grandes de datos de SQL Server a clústeres de Kubernetes](deployment-guidance.md)