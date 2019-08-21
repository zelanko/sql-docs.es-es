---
title: ¿Qué son los grupos de proceso?
titleSuffix: SQL Server big data clusters
description: En este artículo se describe el grupo de proceso [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]en un.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6156d23fa55690224cd6df82e5f4bafe10e4d1ab
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653086"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>¿Qué son los grupos de proceso en un clúster de macrodatos de SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe el rol de los *grupos de proceso de SQL Server* en un clúster de macrodatos de SQL Server 2019 (versión preliminar). Los grupos de proceso proporcionan recursos computacionales de escalado horizontal para un clúster de macrodatos. En las secciones siguientes se describe la arquitectura y funcionalidad de un grupo de proceso.

## <a name="compute-pool-architecture"></a>Arquitectura de grupo de proceso

Un grupo de proceso se compone de uno o varios pods de proceso que se ejecutan en Kubernetes. La creación y administración automatizadas de estos pods se coordinan mediante la [instancia maestra de SQL Server](concept-master-instance.md). Cada pod contiene un conjunto de servicios base y una instancia del motor de base de datos de SQL Server.

## <a name="scale-out-groups"></a>Grupos de escalado horizontal

Un grupo de proceso puede actuar como grupo de escalado horizontal de PolyBase para las consultas distribuidas en diferentes orígenes de datos, como HDFS, Oracle, MongoDB o Terradata. Mediante el uso de pods de proceso en Kubernetes, los clústeres de macrodatos pueden automatizar la creación y configuración de los pods de proceso para los grupos de escalado horizontal de PolyBase.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]de, consulte los siguientes recursos:

- [¿Qué [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]son?](big-data-cluster-overview.md)
- [Taller: Arquitectura [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] de Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
