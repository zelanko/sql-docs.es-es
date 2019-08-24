---
title: ¿Qué es el bloque de almacenamiento?
titleSuffix: SQL Server big data clusters
description: En este artículo se describe el bloque de almacenamiento en un clúster de macrodatos de SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 114296d0bad77c3bbbb088feed13bd6a4bd5a074
ms.sourcegitcommit: 594cee116fa4ee321e1f5e5206f4a94d408f1576
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2019
ms.locfileid: "70009333"
---
# <a name="what-is-the-storage-pool-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>¿Qué es el bloque de[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]almacenamiento ()?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe el rol del *grupo de almacenamiento* de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]SQL Server en un. En las secciones siguientes se describen la arquitectura y la funcionalidad de un bloque de almacenamiento de SQL.

## <a name="storage-pool-architecture"></a>Arquitectura del bloque de almacenamiento

El bloque de almacenamiento consiste en nodos de almacenamiento que se componen de SQL Server en Linux, Spark y HDFS. Todos los nodos de almacenamiento de un clúster de macrodatos de SQL Server son miembros de un clúster de HDFS.

![Arquitectura del bloque de almacenamiento](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>Responsabilidades

Los nodos de almacenamiento se encargan de varios aspectos:

- Ingesta de datos a través de Spark.
- Almacenamiento de datos en HDFS (formato de texto delimitado y parquet). HDFS también proporciona persistencia de datos, ya que los datos de HDFS se reparten por todos los nodos de almacenamiento del clúster de macrodatos de SQL.
- Acceso a datos a través de los puntos de conexión de HDFS y SQL Server.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]de, consulte los siguientes recursos:

- [¿Qué [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]son?](big-data-cluster-overview.md)
- [Taller: Arquitectura [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] de Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
