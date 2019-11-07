---
title: Conexión a clústeres maestros y HDFS de macrodatos
description: Aprenda a conectarse a la instancia maestra de SQL Server y a la puerta de enlace HDFS/Spark de un [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0717226ee785df568d4cea75511e65acb728c592
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532239"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Conexión a un clúster de macrodatos de SQL Server con Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se explica cómo conectarse a [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] desde Azure Data Studio.

## <a name="prerequisites"></a>Prerequisites

- Tener implementado un [clúster de macrodatos de SQL Server 2019](deployment-guidance.md).
- [Herramientas de macrodatos de SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
   - **kubectl**
   - **azdata**

## <a id="master"></a> Conexión al clúster

Para conectarse a un clúster de macrodatos con Azure Data Studio, cree una nueva conexión a la instancia maestra de SQL Server del clúster. En los pasos siguientes se describe cómo conectarse a la instancia maestra mediante Azure Data Studio.

1. Busque el punto de conexión de la instancia maestra de SQL Server:

   ```
   azdata bdc endpoint list -e sql-server-master
   ```

   > [!TIP]
   > Para obtener más información sobre cómo recuperar puntos de conexión, vea [Recuperación de puntos de conexión](deployment-guidance.md#endpoints).

1. En Azure Data Studio, presione **F1** > **Nueva conexión**.

1. En **Tipo de conexión**, seleccione **Microsoft SQL Server**.

1. Escriba el nombre del punto de conexión que ha encontrado para la instancia maestra de SQL Server en el cuadro de texto **Nombre del servidor** (por ejemplo: **\<IP_Address\>,31433**). 

1. Seleccione el tipo de autenticación. En una instancia maestra de SQL Server que se ejecute en clústeres de macrodatos solo se admiten **Autenticación de Windows** e **Inicio de sesión de SQL**. 

1. Escriba un **Nombre de usuario** y una **Contraseña** de inicio de sesión de SQL. Si usa Autenticación de Windows, no es necesario.

   > [!TIP]
   > De forma predeterminada, el nombre de usuario **SA** está deshabilitado durante la implementación del clúster de macrodatos. Durante la implementación se aprovisiona un nuevo usuario sysadmin con el nombre correspondiente a la variable de entorno **AZDATA_USERNAME** y la contraseña correspondiente a la variable de entorno **AZDATA_PASSWORD** empleados durante la implementación.

1. Cambie el **Nombre de la base de datos** de destino por uno de sus bases de datos relacionales.

   ![Conexión a la instancia maestra](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. Presione **Conectar **. Debería aparecer el** Panel del servidor**.

Con la versión de febrero de 2019 de Azure Data Studio, la conexión a la instancia maestra de SQL Server también le permite interactuar con la puerta de enlace HDFS/Spark. Esto significa que no es necesario usar la conexión independiente para HDFS y Spark que se describe en la siguiente sección.

- El Explorador de objetos contiene ahora un nuevo nodo **Data Services** con compatibilidad con las tareas del clúster de macrodatos que se activan con el botón derecho, como la creación de nuevos cuadernos o el envío de trabajos de Spark. 
- El nodo **Data Services** también contiene una carpeta **HDFS** para la exploración de HDFS y para realizar acciones como crear tablas externas o analizar en Notebook.
- El **Panel del servidor** de la conexión también contiene pestañas para el **clúster de macrodatos de SQL Server** y **SQL Server 2019 (versión preliminar)** cuando la extensión está instalada.

   ![Nodo Data Services de Azure Data Studio](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)?
