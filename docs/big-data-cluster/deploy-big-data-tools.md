---
title: Conectarse a un servidor SQL en clúster de macrodatos con Azure Data Studio | Microsoft Docs
description: Obtenga información sobre cómo conectarse a un clúster de SQL Server 2019 macrodatos con Azure Data Studio.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/05/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 971fc2f8e8a77b00f3d2c5cd6390fec351ffc0f3
ms.sourcegitcommit: c7d3a903eb7f410db3a0230101d24de0af17621a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2018
ms.locfileid: "48827306"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Conectarse a un clúster de macrodatos de SQL Server con Azure Data Studio

En este artículo se describe cómo instalar Azure Data Studio, la extensión de SQL Server 2019 (versión preliminar) y, a continuación, conectarse a un clúster de macrodatos. La nueva extensión de SQL Server 2019 incluye compatibilidad con la versión preliminar de [clústeres de SQL Server 2019 macrodatos](big-data-cluster-overview.md), un enfoque integrado [experiencia de cuaderno](notebooks-guidance.md)y un PolyBase [asistente Create External Table](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-azure-data-studio"></a>Instalar datos de Azure Studio

Para instalar Azure Data Studio, consulte [descargue e instale la versión más reciente de Azure Data Studio](../azure-data-studio/download.md).

## <a name="install-the-sql-server-2019-extension-preview"></a>Instalar la extensión de SQL Server 2019 (versión preliminar)

Para instalar la extensión, consulte [instalar la extensión de SQL Server 2019 (versión preliminar)](../azure-data-studio/sql-server-2019-extension.md).

## <a name="connect-to-the-cluster"></a>Conéctese al clúster

Cuando se conecta a un clúster de macrodatos, tiene la opción para conectarse a SQL Server [instancia maestra](concept-master-instance.md) o a la puerta de enlace de Spark o HDFS. Las secciones siguientes muestran cómo conectarse a cada uno.

## <a name="master-instance"></a>Instancia principal

1. En Azure Data Studio, presione **F1** > **nueva conexión**.
1. En **tipo de conexión**, seleccione **Microsoft SQL Server**.
1. Escriba la dirección IP de la instancia principal de SQL Server en **nombre del servidor** (por ejemplo:  **\<dirección IP\>, 31433**).
1. Cambiar el **nombre de base de datos** a la **high_value_data** base de datos.

   ![Conéctese a la instancia maestra](./media/deploy-big-data-tools/connect-to-cluster.png)

1. Presione **Connect**y el **panel Server** debería aparecer.

## <a name="hdfsspark-gateway"></a>Puerta de enlace de Spark o HDFS

1. En Azure Data Studio, presione **F1** > **nueva conexión**.
1. En **tipo de conexión**, seleccione **clúster grande de datos de SQL Server**.
1. Escriba la dirección IP del clúster de macrodatos en **nombre del servidor**.

   ![Conectarse a la puerta de enlace de Spark o HDFS](./media/deploy-big-data-tools/connect-to-cluster-hdfs-spark.png)

1. Presione **Connect**y el **panel Server** debería aparecer.

## <a name="next-steps"></a>Pasos siguientes

Para ejecutar los cuadernos en Azure Data Studio, vea [para usar cuadernos en versión preliminar de SQL Server 2019](notebooks-guidance.md).
