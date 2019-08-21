---
title: Conexión a los clústeres de macrodatos maestros y HDFS
description: Obtenga información sobre cómo conectarse al SQL Server instancia maestra y la puerta de enlace HDFS/Spark [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]para un.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fb6e1f684a277740c06fbd0a2fdc23dbd77f8e5c
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652423"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Conexión a un clúster de macrodatos de SQL Server con Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo conectarse a [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] desde Azure Data Studio.

## <a name="prerequisites"></a>Requisitos previos

- Tener implementado un [clúster de macrodatos de SQL Server 2019](deployment-guidance.md).
- [Herramientas de macrodatos de SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
   - **kubectl**

## <a id="master"></a> Conexión al clúster

Para conectarse a un clúster de macrodatos con Azure Data Studio, cree una nueva conexión a la instancia maestra de SQL Server del clúster. En los pasos siguientes se describe cómo conectarse a la instancia maestra mediante Azure Data Studio.

1. Desde la línea de comandos, busque la dirección IP de la instancia maestra con el siguiente comando:

   ```
   kubectl get svc master-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > De forma predeterminada, el nombre del clúster de macrodatos es **mssql-cluster**, a menos que haya personalizado el nombre en un archivo de configuración de implementación. Para obtener más información, vea [Configuración de opciones de implementación para clústeres de macrodatos](deployment-custom-configuration.md#clustername).

1. En Azure Data Studio, presione **F1** > **Nueva conexión**.

1. En **Tipo de conexión**, seleccione **Microsoft SQL Server**.

1. Escriba la dirección IP de la instancia maestra de SQL Server en **Nombre del servidor** (por ejemplo: **\<Dirección IP\>,31433**).

1. Escriba un **Nombre de usuario** y una **Contraseña** de inicio de sesión de SQL.

   > [!TIP]
   > De forma predeterminada, el nombre de usuario es **SA** y, a menos que se cambie, la contraseña corresponde a la variable de entorno **MSSQL_SA_PASSWORD** que se usa durante la implementación.

1. Cambie el **Nombre de la base de datos** de destino por uno de sus bases de datos relacionales.

   ![Conexión a la instancia maestra](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. Presione **Conectar **. Debería aparecer el** Panel del servidor**.

Con la versión de febrero de 2019 de Azure Data Studio, la conexión a la instancia maestra de SQL Server también le permite interactuar con la puerta de enlace HDFS/Spark. Esto significa que no es necesario usar la conexión independiente para HDFS y Spark que se describe en la siguiente sección.

- El Explorador de objetos contiene ahora un nuevo nodo **Data Services** con compatibilidad con las tareas del clúster de macrodatos que se activan con el botón derecho, como la creación de nuevos cuadernos o el envío de trabajos de Spark. 
- El nodo **Data Services** también contiene una carpeta **HDFS** para la exploración de HDFS y para realizar acciones como crear tablas externas o analizar en Notebook.
- El **Panel del servidor** de la conexión también contiene pestañas para el **clúster de macrodatos de SQL Server** y **SQL Server 2019 (versión preliminar)** cuando la extensión está instalada.

   ![Nodo Data Services de Azure Data Studio](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]acerca de, vea [Qué son [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] ](big-data-cluster-overview.md).