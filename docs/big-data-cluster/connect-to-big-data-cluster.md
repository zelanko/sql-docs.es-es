---
title: Conectarse al maestro y HDFS
titleSuffix: SQL Server 2019 big data clusters
description: Obtenga información sobre cómo conectarse a la instancia principal de SQL Server y la puerta de enlace de Spark o HDFS para un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/10/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9129b436f33092054a19b858fa5bcdb8aebadec2
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241826"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Conectarse a un clúster de macrodatos de SQL Server con Azure Data Studio

En este artículo se describe cómo conectarse a un clúster de macrodatos de 2019 de SQL Server (versión preliminar) desde Azure Data Studio.

## <a name="prerequisites"></a>Requisitos previos

- Una implementada [clúster de SQL Server 2019 macrodatos](deployment-guidance.md).
- [Herramientas de SQL Server 2019 macrodatos](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
   - **kubectl**

## <a name="connect-to-the-cluster"></a>Conéctese al clúster

Cuando se conecta a un clúster de macrodatos, tiene la opción de conectarse a la instancia principal de SQL Server o a la puerta de enlace de Spark o HDFS. Las secciones siguientes muestran cómo conectarse a cada uno.

## <a id="master"></a> Instancia principal

La instancia principal de SQL Server es una instancia de SQL Server tradicional que contienen bases de datos relacionales de SQL Server. Los pasos siguientes describen cómo conectarse a la instancia maestra mediante Azure Data Studio.

1. Desde la línea de comandos, busque la dirección IP de la instancia maestra con el siguiente comando:

   ```
   kubectl get svc endpoint-master-pool -n <your-cluster-name>
   ```

1. En Azure Data Studio, presione **F1** > **nueva conexión**.

1. En **tipo de conexión**, seleccione **Microsoft SQL Server**.

1. Escriba la dirección IP de la instancia principal de SQL Server en **nombre del servidor** (por ejemplo: **\<Dirección IP\>, 31433**).

1. Escriba un inicio de sesión SQL **nombre de usuario** y **contraseña**.

   > [!TIP]
   > De forma predeterminada, el nombre de usuario es **SA** y, a menos que cambie, la contraseña corresponde a la **MSSQL_SA_PASSWORD** variable de entorno que se usa durante la implementación.

1. Cambiar el destino **nombre de base de datos** a una de las bases de datos relacionales.

   ![Conéctese a la instancia maestra](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. Presione **Connect**y el **panel Server** debería aparecer.

## <a id="hdfs"></a> Puerta de enlace de Spark o HDFS

El **puerta de enlace de Spark o HDFS** le permite conectar con el fin de trabajar con el bloque de almacenamiento HDFS y para ejecutar trabajos de Spark. Los pasos siguientes describen cómo conectar con Azure Data Studio.

1. Desde la línea de comandos, busque la dirección IP de la puerta de enlace de Spark o HDFS con uno de los siguientes comandos.
   
   **Implementaciones de AKS:**

   ```
   kubectl get svc service-security-lb -n <your-cluster-name>
   ```

   **Las implementaciones que no sean AKS**:

   ```
   kubectl get svc service-security-nodeport -n <your-cluster-name>
   ```
 
1. En Azure Data Studio, presione **F1** > **nueva conexión**.

1. En **tipo de conexión**, seleccione **clúster grande de datos de SQL Server**.

   > [!TIP]
   > Si no ve el **clúster grande de datos de SQL Server** conexión escriba, asegúrese de que ha instalado el [extensión de SQL Server 2019](../azure-data-studio/sql-server-2019-extension.md) y que reinicie Azure Data Studio después de la extensión de completado instalación de.

1. Escriba la dirección IP del clúster de macrodatos en **nombre del servidor** (no especifique un puerto).

1. Escriba `root` para el **usuario** y especifique el **contraseña** a su clúster de macrodatos.

   ![Conectarse a la puerta de enlace de Spark o HDFS](./media/connect-to-big-data-cluster/connect-to-cluster-hdfs-spark.png)

   > [!TIP]
   > De forma predeterminada, el nombre de usuario es **raíz** y la contraseña corresponde a la **KNOX_PASSWORD** variable de entorno que se usa durante la implementación.

1. Presione **Connect**y el **panel Server** debería aparecer.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de 2019 de SQL Server, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos](big-data-cluster-overview.md).