---
title: ¿Qué son los grupos de proceso?
titleSuffix: SQL Server big data clusters
description: En este artículo se describe el grupo de proceso en un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6da6e2b948027446623e47a58670e44cd99886de
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729157"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>¿Cuáles son los grupos de proceso en un clúster de macrodatos de SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe el rol de *grupos de proceso de SQL Server* en un clúster de macrodatos de vista previa de 2019 de SQL Server. Grupos de proceso proporcionan recursos de cálculo de escalabilidad horizontal para un clúster de macrodatos. Las secciones siguientes describen la arquitectura y la funcionalidad de un grupo de proceso.

## <a name="compute-pool-architecture"></a>Arquitectura del grupo de proceso

Un grupo de proceso está formado por uno o más pods que se ejecutan en Kubernetes de proceso. La creación automatizada y la administración de estos pods se coordinan mediante el [instancia principal de SQL Server](concept-master-instance.md). Cada pod contiene un conjunto de servicios de bases y una instancia del motor de base de datos de SQL Server.

## <a name="scale-out-groups"></a>Grupos de escalado horizontal

Un grupo de proceso puede actuar como un grupo de escalabilidad horizontal de PolyBase para las consultas distribuidas a través de orígenes de datos diferentes, como HDFS, Oracle, MongoDB o Teradata. Mediante el uso de compute pods de Kubernetes, clústeres de datos de gran tamaño pueden automatizar la creación y configuración de pods de proceso para grupos de escalado horizontal de PolyBase.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, consulte los siguientes recursos:

- [¿Qué son los clústeres de macrodatos de 2019 de SQL Server?](big-data-cluster-overview.md)
- [Taller: Arquitectura de clústeres de macrodatos de Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
