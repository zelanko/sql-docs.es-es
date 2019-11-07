---
title: ¿Qué son los grupos de proceso?
titleSuffix: SQL Server big data clusters
description: En este artículo se describe el grupo de proceso en [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f6f2813dff5e965f61f15b947725d78bf327dde7
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532397"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>¿Qué son los grupos de proceso en un clúster de macrodatos de SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe el rol de los *grupos de proceso de SQL Server* en un clúster de macrodatos de SQL Server. Los grupos de proceso proporcionan recursos computacionales de escalado horizontal para un clúster de macrodatos. En las secciones siguientes se describe la arquitectura y funcionalidad de un grupo de proceso.

## <a name="compute-pool-architecture"></a>Arquitectura de grupo de proceso

Un grupo de proceso se compone de uno o varios pods de proceso que se ejecutan en Kubernetes. La creación y administración automatizadas de estos pods se coordinan mediante la [instancia maestra de SQL Server](concept-master-instance.md). Cada pod contiene un conjunto de servicios base y una instancia del motor de base de datos de SQL Server.

## <a name="scale-out-groups"></a>Grupos de escalado horizontal

Un grupo de proceso puede actuar como grupo de escalado horizontal de PolyBase para las consultas distribuidas en diferentes orígenes de datos, como HDFS, Oracle, MongoDB o Teradata. Mediante el uso de pods de proceso en Kubernetes, los clústeres de macrodatos pueden automatizar la creación y configuración de los pods de proceso para los grupos de escalado horizontal de PolyBase.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vea los recursos siguientes:

- [¿Qué son los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
- [Taller: Arquitectura de los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] de Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
