---
title: ¿Qué son los grupos de datos?
titleSuffix: SQL Server big data clusters
description: En este artículo, se describe el grupo de datos en un clúster de macrodatos de SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f9355508e4d32dd9a6152781fba325ded2fa7425
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958736"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>¿Qué son los grupos de datos en un clúster de macrodatos de SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo, se describe la función de los *grupos de datos de SQL Server* en un clúster de macrodatos de SQL Server 2019 (versión preliminar). En las secciones siguientes, se describen la arquitectura y las funciones de un grupo de datos SQL.

## <a name="data-pool-architecture"></a>Arquitectura de un grupo de datos

Un grupo de datos está formado por una o más instancias de grupos de datos de SQL Server. Las instancias del grupo de datos SQL proporcionan un almacenamiento de SQL Server persistente para el clúster. Se usa un grupo de datos para ingerir datos a partir de consultas SQL o trabajos de Spark. Para ofrecer un mejor rendimiento en conjuntos de datos de gran tamaño, los datos de un grupo de datos se distribuyen en particiones en todas las instancias del grupo de datos SQL que sean miembros.

## <a name="scale-out-data-marts"></a>Data marts de escalado horizontal

Los grupos de datos permiten la creación de data marts de escalado horizontal, donde los datos externos de varios orígenes se ingieren en el grupo de datos. Como los datos se distribuyen en varias instancias de grupos de datos, las consultas paralelas en los datos recopilados son más eficientes.

![Data mart de escalado horizontal](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos de SQL Server, vea los recursos siguientes:

- [¿Qué son los clústeres de macrodatos de SQL Server 2019?](big-data-cluster-overview.md)
- [Taller: arquitectura de clústeres de macrodatos de Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
