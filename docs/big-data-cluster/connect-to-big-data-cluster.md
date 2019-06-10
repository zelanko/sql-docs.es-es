---
title: Conectarse al maestro y HDFS
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo conectarse a la instancia principal de SQL Server y la puerta de enlace de Spark o HDFS para un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 245e88034194a01908b69d545deb9fa717c19a4a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782979"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Conectarse a un clúster de macrodatos de SQL Server con Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo conectarse a un clúster de macrodatos de 2019 de SQL Server (versión preliminar) desde Azure Data Studio.

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
   kubectl get svc master-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Los datos de gran tamaño de clúster nombre predeterminado es **mssql-cluster** a menos que personalice el nombre de un archivo de configuración de implementación. Para obtener más información, consulte [configurar opciones de implementación para los clústeres de macrodatos](deployment-custom-configuration.md#clustername).

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
- El **panel del servidor** para la conexión también contiene las pestañas **clúster grande de datos de SQL Server** y **(versión preliminar) de SQL Server 2019** cuando se instala la extensión.

   ![Nodo de servicios de datos de Azure Studio datos](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de 2019 de SQL Server, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos](big-data-cluster-overview.md).