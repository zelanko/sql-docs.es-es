---
title: ¿Cuáles son los grupos de datos?
titleSuffix: SQL Server 2019 big data clusters
description: En este artículo se describe el grupo de datos en un clúster de macrodatos de SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 906b27c186668518702c7ab3a757e6eeb4e5b278
ms.sourcegitcommit: 715683b5fc7a8e28a86be8949a194226b72ac915
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/26/2019
ms.locfileid: "58478230"
---
# <a name="what-are-data-pools-in-a-sql-server-2019-big-data-cluster"></a>¿Cuáles son los grupos de datos en un clúster de macrodatos de 2019 de SQL Server?

En este artículo se describe el rol de *los grupos de datos de SQL Server* en un clúster de macrodatos de 2019 de SQL Server (versión preliminar). Las secciones siguientes describen la arquitectura y la funcionalidad de un grupo de datos SQL.

## <a name="data-pool-architecture"></a>Arquitectura del grupo de datos

Un grupo de datos consta de uno o más instancias de grupo de datos de SQL Server. Las instancias del grupo de datos SQL proporcionan almacenamiento persistente de SQL Server para el clúster. Un grupo de datos se usa para introducir datos desde las consultas SQL o trabajos de Spark. Para proporcionar un mejor rendimiento de grandes conjuntos de datos, los datos en un grupo de datos se distribuyen en particiones entre las instancias de grupo de datos SQL de miembro.

## <a name="scale-out-data-marts"></a>Puestos de datos de escalabilidad horizontal

Los grupos de datos permiten la creación de puestos de datos de escalabilidad horizontal, donde se recopilan los datos externos desde varios orígenes en el grupo de datos. Porque los datos se distribuyen entre las instancias del grupo de datos, las consultas en paralelo con los datos protegidos son más eficaces.

![Escalabilidad horizontal data mart.](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, consulte los siguientes recursos:

- [¿Qué son los clústeres de macrodatos de 2019 de SQL Server?](big-data-cluster-overview.md)
- [Taller: Arquitectura de clústeres de macrodatos de Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
