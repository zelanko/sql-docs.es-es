---
title: Carga de datos de muestra
titleSuffix: SQL Server big data clusters
description: En este tutorial se muestra cómo cargar datos de ejemplo en un clúster de macrodatos de SQL Server. Los datos de ejemplo incluyen datos relacionales en el SQL Server instancia maestra. También incluye datos de HDFS en el grupo de almacenamiento. Estos datos admiten otros tutoriales de esta sección.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5b35eccece4df47cb483932386cf6a38e45d2dc8
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419280"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>Tutorial: Carga de datos de ejemplo en un clúster SQL Server Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este tutorial se explica cómo usar un script para cargar datos de ejemplo en un clúster de macrodatos de SQL Server 2019 (versión preliminar). Muchos de los otros tutoriales de la documentación de usan estos datos de ejemplo.

> [!TIP]
> Puede encontrar más ejemplos de SQL Server clúster de macrodatos de 2019 (versión preliminar) en el repositorio de github [SQL-Server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) . Se encuentran en **SQL-Server-samples/samples/Features/SQL-Big-Data-Cluster/** path.

## <a name="prerequisites"></a>Requisitos previos

- [Un clúster de Big Data implementado](deployment-guidance.md)
- [Herramientas de macrodatos](deploy-big-data-tools.md)
   - **azdata**
   - **kubectl**
   - **sqlcmd**
   - **curl**

## <a id="sampledata"></a>Cargar datos de ejemplo

En los pasos siguientes se usa un script de bootstrap para descargar una copia de seguridad de SQL Server Database y cargar los datos en el clúster de Big Data. Para facilitar su uso, estos pasos se han dividido en secciones de [Windows](#windows) y [Linux](#linux) .

## <a id="windows"></a>Windows

En los pasos siguientes se describe cómo usar un cliente de Windows para cargar los datos de ejemplo en el clúster de Big Data.

1. Abra un nuevo símbolo del sistema de Windows.

   > [!IMPORTANT]
   > No use Windows PowerShell para realizar estos pasos. En PowerShell, el script producirá un error ya que usará la versión de PowerShell de **rizo**.

1. Use **rizo** para descargar el script de bootstrap para los datos de ejemplo.

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. Descargue el script Transact-SQL de **bootstrap-Sample-dB. SQL** . El script de arranque llama a este script.

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. El script de arranque requiere los siguientes parámetros posicionales para el clúster de Big Data:

   | Parámetro | Descripción |
   |---|---|
   | < CLUSTER_NAMESPACE > | El nombre que asignó al clúster de Big Data. |
   | <SQL_MASTER_IP> | La dirección IP de la instancia maestra. |
   | <SQL_MASTER_SA_PASSWORD> | La contraseña de SA para la instancia maestra. |
   | <KNOX_IP> | La dirección IP de la puerta de enlace HDFS/Spark. |
   | <KNOX_PASSWORD> | La contraseña para la puerta de enlace HDFS/Spark. |

   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) para buscar las direcciones IP de la instancia maestra de SQL Server y Knox. Ejecute `kubectl get svc -n <your-big-data-cluster-name>` y examine las direcciones IP externas de la instancia maestra (**Master-SVC-external**) y Knox (**puerta de enlace-SVC-external**). El nombre predeterminado de un clúster es **MSSQL-Cluster**.

1. Ejecute el script bootstrap.

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

En los pasos siguientes se describe cómo usar un cliente Linux para cargar los datos de ejemplo en el clúster de Big Data.

1. Descargue el script de bootstrap y asigne permisos de archivo ejecutable.

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. Descargue el script Transact-SQL de **bootstrap-Sample-dB. SQL** . El script de arranque llama a este script.

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. El script de arranque requiere los siguientes parámetros posicionales para el clúster de Big Data:

   | Parámetro | Descripción |
   |---|---|
   | < CLUSTER_NAMESPACE > | El nombre que asignó al clúster de Big Data. |
   | <SQL_MASTER_IP> | La dirección IP de la instancia maestra. |
   | <SQL_MASTER_SA_PASSWORD> | La contraseña de SA para la instancia maestra. |
   | <KNOX_IP> | La dirección IP de la puerta de enlace HDFS/Spark. |
   | <KNOX_PASSWORD> | La contraseña para la puerta de enlace HDFS/Spark. |

   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) para buscar las direcciones IP de la instancia maestra de SQL Server y Knox. Ejecute `kubectl get svc -n <your-big-data-cluster-name>` y examine las direcciones IP externas de la instancia maestra (**Master-SVC-external**) y Knox (**puerta de enlace-SVC-external**). El nombre predeterminado de un clúster es **MSSQL-Cluster**.

1. Ejecute el script bootstrap.

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>Pasos siguientes

Una vez que se ejecuta el script de bootstrap, el clúster de Big Data tiene las bases de datos de ejemplo y los datos de HDFS. En los siguientes tutoriales se usan los datos de ejemplo para mostrar las capacidades de los clústeres de Big Data:

Virtualización de datos:

- [Tutorial: Consulta de HDFS en un clúster de macrodatos SQL Server](tutorial-query-hdfs-storage-pool.md)
- [Tutorial: Consulta de Oracle desde un clúster de macrodatos SQL Server](tutorial-query-oracle.md)

Ingesta de datos:

- [Tutorial: Ingerir datos en un grupo de datos de SQL Server con Transact-SQL](tutorial-data-pool-ingest-sql.md)
- [Tutorial: Ingerir datos en un grupo de datos de SQL Server con trabajos de Spark](tutorial-data-pool-ingest-spark.md)

Cuadernos

- [Tutorial: Ejecución de un cuaderno de ejemplo en un clúster de macrodatos SQL Server 2019](tutorial-notebook-spark.md)