---
title: ¿Qué son los grupos de proceso?
titleSuffix: SQL Server 2019 big data clusters
description: En este artículo se describe el grupo de proceso en un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 272f10cfed8f7cd1b07633b81642323a8c74b6d7
ms.sourcegitcommit: 56fb7b648adae2c7b81bd969de067af1a2b54180
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2019
ms.locfileid: "57227137"
---
# <a name="what-are-compute-pools-in-a-sql-server-2019-big-data-cluster"></a>¿Cuáles son los grupos de proceso en un clúster de macrodatos de 2019 de SQL Server?

En este artículo se describe el rol de *grupos de proceso de SQL Server* en un clúster de macrodatos de vista previa de 2019 de SQL Server. Grupos de proceso proporcionan recursos de cálculo de escalabilidad horizontal para un clúster de macrodatos. Las secciones siguientes describen la arquitectura y la funcionalidad de un grupo de proceso.

## <a name="compute-pool-architecture"></a>Arquitectura del grupo de proceso

Un grupo de proceso está formado por uno o más pods que se ejecutan en Kubernetes de proceso. La creación automatizada y la administración de estos pods se coordinan mediante el [instancia principal de SQL Server](concept-master-instance.md). Cada pod contiene un conjunto de servicios de bases y una instancia del motor de base de datos de SQL Server.

## <a name="scale-out-groups"></a>Grupos de escalado horizontal

Un grupo de proceso puede actuar como un grupo de escalabilidad horizontal de PolyBase para las consultas distribuidas a través de orígenes de datos diferentes, como HDFS, Oracle, MongoDB o Teradata. Mediante el uso de compute pods de Kubernetes, clústeres de datos de gran tamaño pueden automatizar la creación y configuración de pods de proceso para grupos de escalado horizontal de PolyBase.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, consulte la información general siguiente:

- [¿Qué son los clústeres de macrodatos de 2019 de SQL Server?](big-data-cluster-overview.md)
