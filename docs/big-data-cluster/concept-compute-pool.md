---
title: ¿Qué son los grupos de proceso?
titleSuffix: SQL Server big data clusters
description: En este artículo se describen los grupos de proceso en un clúster de macrodatos de SQL Server 2019 (versión preliminar).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d9ae112369ddad91bec125ec19713040a5aae915
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958806"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>¿Qué son los grupos de proceso en un clúster de macrodatos de SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe el rol de los *grupos de proceso de SQL Server* en un clúster de macrodatos de SQL Server 2019 (versión preliminar). Los grupos de proceso proporcionan recursos computacionales de escalado horizontal para un clúster de macrodatos. En las secciones siguientes se describe la arquitectura y funcionalidad de un grupo de proceso.

## <a name="compute-pool-architecture"></a>Arquitectura de grupo de proceso

Un grupo de proceso se compone de uno o varios pods de proceso que se ejecutan en Kubernetes. La creación y administración automatizadas de estos pods se coordinan mediante la [instancia maestra de SQL Server](concept-master-instance.md). Cada pod contiene un conjunto de servicios base y una instancia del motor de base de datos de SQL Server.

## <a name="scale-out-groups"></a>Grupos de escalado horizontal

Un grupo de proceso puede actuar como grupo de escalado horizontal de PolyBase para las consultas distribuidas en diferentes orígenes de datos, como HDFS, Oracle, MongoDB o Terradata. Mediante el uso de pods de proceso en Kubernetes, los clústeres de macrodatos pueden automatizar la creación y configuración de los pods de proceso para los grupos de escalado horizontal de PolyBase.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos de SQL Server, consulte los siguientes recursos:

- [¿Qué son los clústeres de macrodatos de SQL Server 2019?](big-data-cluster-overview.md)
- [Taller: Arquitectura de clústeres de macrodatos de Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
