---
title: Carga de datos de muestra
titleSuffix: SQL Server big data clusters
description: Este tutorial muestra cómo cargar datos de ejemplo en un clúster de macrodatos de SQL Server. Los datos de ejemplo incluyen datos relacionales en la instancia principal de SQL Server. También incluye datos de HDFS en el bloque de almacenamiento. Estos datos es compatible con otros tutoriales de esta sección.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 04/23/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f4ea5540c0188ec9a57ad8b6780cf3ab6af5dfc2
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727346"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>Tutorial: Cargar datos de ejemplo en un clúster de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este tutorial explica cómo usar un script para cargar datos de ejemplo en un clúster de macrodatos de 2019 de SQL Server (versión preliminar). Muchos de los otros tutoriales en la documentación de usan estos datos de ejemplo.

> [!TIP]
> Puede encontrar ejemplos adicionales para el clúster de macrodatos de 2019 de SQL Server (versión preliminar) en el [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) repositorio de GitHub. Se encuentran en el **sql-server-samples/samples/features/sql-big-data-cluster/** ruta de acceso.

## <a name="prerequisites"></a>Requisitos previos

- [Un clúster implementado macrodatos](deployment-guidance.md)
- [Herramientas de datos de gran tamaño](deploy-big-data-tools.md)
   - **mssqlctl**
   - **kubectl**
   - **sqlcmd**
   - **curl**

## <a id="sampledata"></a> Cargar datos de ejemplo

Los pasos siguientes usan un script de arranque para descargar una copia de seguridad de base de datos de SQL Server y cargar los datos en el clúster de macrodatos. Para facilitar su uso, estos pasos se ha desglosado en [Windows](#windows) y [Linux](#linux) secciones.

## <a id="windows"></a> Windows

Los pasos siguientes describen cómo usar a un cliente de Windows para cargar los datos de ejemplo en el clúster de macrodatos.

1. Abra un nuevo símbolo de Windows.

   > [!IMPORTANT]
   > No use Windows PowerShell para realizar estos pasos. En PowerShell, la secuencia de comandos se producirá un error como utilizarán la versión de PowerShell de **curl**.

1. Use **curl** para descargar el script de arranque para los datos de ejemplo.

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. Descargue el **bootstrap-ejemplo-db.sql** script Transact-SQL. Este script se llama por el script de arranque.

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. La secuencia de comandos bootstrap requiere los siguientes parámetros posicionales para el clúster de macrodatos:

   | Parámetro | Descripción |
   |---|---|
   | <CLUSTER_NAMESPACE> | El nombre que asignó a su clúster de macrodatos. |
   | <SQL_MASTER_IP> | La dirección IP de la instancia maestra. |
   | <SQL_MASTER_SA_PASSWORD> | La contraseña de SA para la instancia maestra. |
   | <KNOX_IP> | La dirección IP de la puerta de enlace de Spark o HDFS. |
   | <KNOX_PASSWORD> | La contraseña de la puerta de enlace de Spark o HDFS. |

   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) para buscar las direcciones IP para la instancia principal de SQL Server y Knox. Ejecute `kubectl get svc -n <your-big-data-cluster-name>` y examine las direcciones IP externa para la instancia maestra (**master-svc-external**) y Knox (**puerta de enlace-svc-external**). El nombre predeterminado de un clúster es **mssql-cluster**.

1. Ejecute el script de arranque.

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

Los pasos siguientes describen cómo usar a un cliente Linux para cargar los datos de ejemplo en el clúster de macrodatos.

1. Descargue el script de arranque y asignarle permisos ejecutable.

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. Descargue el **bootstrap-ejemplo-db.sql** script Transact-SQL. Este script se llama por el script de arranque.

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. La secuencia de comandos bootstrap requiere los siguientes parámetros posicionales para el clúster de macrodatos:

   | Parámetro | Descripción |
   |---|---|
   | <CLUSTER_NAMESPACE> | El nombre que asignó a su clúster de macrodatos. |
   | <SQL_MASTER_IP> | La dirección IP de la instancia maestra. |
   | <SQL_MASTER_SA_PASSWORD> | La contraseña de SA para la instancia maestra. |
   | <KNOX_IP> | La dirección IP de la puerta de enlace de Spark o HDFS. |
   | <KNOX_PASSWORD> | La contraseña de la puerta de enlace de Spark o HDFS. |

   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) para buscar las direcciones IP para la instancia principal de SQL Server y Knox. Ejecute `kubectl get svc -n <your-big-data-cluster-name>` y examine las direcciones IP externa para la instancia maestra (**master-svc-external**) y Knox (**puerta de enlace-svc-external**). El nombre predeterminado de un clúster es **mssql-cluster**.

1. Ejecute el script de arranque.

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>Pasos siguientes

Después de ejecutar el script de arranque, el clúster de macrodatos tiene bases de datos de ejemplo y datos de HDFS. Los tutoriales siguientes usan los datos de ejemplo para demostrar las capacidades de clúster de macrodatos:

Virtualización de datos:

- [Tutorial: Consulta de HDFS en un clúster de macrodatos de SQL Server](tutorial-query-hdfs-storage-pool.md)
- [Tutorial: Consultas de Oracle desde un clúster de macrodatos de SQL Server](tutorial-query-oracle.md)

Ingesta de datos:

- [Tutorial: Introducir datos en un grupo de datos de SQL Server con Transact-SQL](tutorial-data-pool-ingest-sql.md)
- [Tutorial: Introducir datos en un grupo de datos de SQL Server con trabajos de Spark](tutorial-data-pool-ingest-spark.md)

Blocs de notas:

- [Tutorial: Ejecutar un cuaderno de ejemplo en un clúster de macrodatos de SQL Server 2019](tutorial-notebook-spark.md)