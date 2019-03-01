---
title: Conectarse al maestro y HDFS
titleSuffix: SQL Server 2019 big data clusters
description: Obtenga información sobre cómo conectarse a la instancia principal de SQL Server y la puerta de enlace de Spark o HDFS para un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cb205f387fb326b1717ec65512a911b2ae244495
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017711"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Conectarse a un clúster de macrodatos de SQL Server con Azure Data Studio

En este artículo se describe cómo conectarse a un clúster de macrodatos de 2019 de SQL Server (versión preliminar) desde Azure Data Studio. Hay dos puntos de conexión principales que se usan para interactuar con un clúster de macrodatos:

| Extremo | Descripción |
|---|---|
| Instancia de SQL Server Master | La instancia principal de SQL Server en el clúster que contiene bases de datos relacionales de SQL Server. |
| Puerta de enlace de Spark o HDFS | Acceso al almacenamiento HDFS en el clúster y la capacidad de ejecutar trabajos de Spark. |

> [!TIP]
> Con la versión de febrero de 2019 de Azure Data Studio, conectarse automáticamente a la instancia principal de SQL Server proporciona acceso de interfaz de usuario a la puerta de enlace de Spark o HDFS.

## <a name="prerequisites"></a>Requisitos previos

- Una implementada [clúster de SQL Server 2019 macrodatos](deployment-guidance.md).
- [Herramientas de SQL Server 2019 macrodatos](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
   - **kubectl**

## <a id="master"></a> Conéctese al clúster

Para conectarse a un clúster de macrodatos con Azure Data Studio, realice una conexión nueva a la instancia principal de SQL Server en el clúster. Los pasos siguientes describen cómo conectarse a la instancia maestra mediante Azure Data Studio.

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

Con la versión de febrero de 2019 de Azure Data Studio, conectarse a la instancia principal de SQL Server también le permite interactuar con la puerta de enlace de Spark o HDFS. Esto significa que no es necesario usar una conexión independiente para HDFS y Spark que se describe en la sección siguiente.

- El Explorador de objetos contiene ahora un nuevo **Data Services** nodo con el soporte técnico de contextual para las tareas de clúster de macrodatos, como crear nuevos cuadernos o enviar trabajos de spark. 
- El **Data Services** nodo también contiene un **HDFS** carpeta para la exploración de HDFS y realizar acciones como crear una tabla externa o analizar en el Bloc de notas.
- El **panel Server** para la conexión también contiene las pestañas **clúster grande de datos de SQL Server** y **(versión preliminar) de SQL Server 2019** cuando se instala la extensión.

   ![Nodo de servicios de datos de Azure Studio datos](./media/connect-to-big-data-cluster/connect-data-services-node.png)

> [!IMPORTANT]
> Si ve **error desconocido** en la interfaz de usuario, es posible que deba [conectarse directamente a la puerta de enlace de Spark o HDFS](#hdfs). Una causa de este error son diferentes contraseñas para la instancia principal de SQL Server y la puerta de enlace de Spark o HDFS. Azure Data Studio, se da por supuesto que se usa la misma contraseña para ambos.
  
## <a id="hdfs"></a> Conectarse a la puerta de enlace de Spark o HDFS

En la mayoría de los casos, conectarse a la instancia principal de SQL Server proporciona acceso a la HDFS y también a través de Spark la **Data Services** nodo. Sin embargo, puede crear una conexión dedicada a la **puerta de enlace de Spark o HDFS** si es necesario. Los pasos siguientes describen cómo conectar con Azure Data Studio.

1. Desde la línea de comandos, busque la dirección IP de la puerta de enlace de Spark o HDFS con uno de los siguientes comandos.

   ```
   kubectl get svc endpoint-security -n <your-cluster-name>
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