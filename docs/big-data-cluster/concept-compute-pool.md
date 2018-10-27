---
title: ¿Qué es un grupo de proceso de clústeres de macrodatos SQL? | Microsoft Docs
description: En este artículo se describe el grupo de proceso en un clúster de macrodatos de SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 67f13687bf55a9e267582a0749043c51d2e2b3bf
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050803"
---
# <a name="what-is-a-sql-big-data-clusters-compute-pool"></a>¿Qué es un grupo de proceso de clústeres de macrodatos SQL?

En este artículo se describe el rol de *grupos de proceso de SQL Server* en un clúster de macrodatos de vista previa de 2019 de SQL Server. Grupos de proceso proporcionan recursos de cálculo de escalabilidad horizontal para un clúster de macrodatos. Las secciones siguientes describen la arquitectura y la funcionalidad de un grupo de proceso.

## <a name="compute-pool-architecture"></a>Arquitectura del grupo de proceso

Un grupo de proceso está formado por uno o más pods que se ejecutan en Kubernetes de proceso. La creación automatizada y la administración de estos pods se coordinan mediante el [instancia principal de SQL Server](concept-master-instance.md). Cada pod contiene un conjunto de servicios de bases y una instancia del motor de base de datos de SQL Server.

> [!NOTE]
> CTP 2.0 solo admite un grupo de proceso único por clúster.

## <a name="scale-out-groups"></a>Grupos de escalado horizontal

Un grupo de proceso puede actuar como un grupo de escalabilidad horizontal de PolyBase para las consultas distribuidas a través de orígenes de datos diferentes, como HDFS, Oracle, MongoDB o Teradata. Mediante el uso de compute pods de Kubernetes, clústeres de datos de gran tamaño pueden automatizar la creación y configuración de pods de proceso para grupos de escalado horizontal de PolyBase.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, consulte la información general siguiente:

- [¿Qué son los clústeres de macrodatos de 2019 de SQL Server?](big-data-cluster-overview.md)
