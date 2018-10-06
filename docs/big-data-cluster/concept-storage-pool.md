---
title: ¿Qué es el bloque de almacenamiento de clústeres de macrodatos de SQL Server? | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 100ce09f7066a6df33d7b1daaf50db50bda4ed03
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48796794"
---
# <a name="what-is-the-sql-server-big-data-clusters-storage-pool"></a>¿Qué es el bloque de almacenamiento de clústeres de macrodatos de SQL Server?

En este artículo se describe el rol de la *bloque de almacenamiento de SQL Server* en un servidor de SQL 2019 previsualizar el clúster de Macrodatos. Las secciones siguientes describen la arquitectura y la funcionalidad de un grupo de almacenamiento SQL.

## <a name="storage-pool-architecture"></a>Arquitectura del grupo de almacenamiento

El grupo de almacenamiento está formado por almacenamiento consta de los nodos de SQL Server en Linux, Spark y HDFS. Todos los nodos de almacenamiento en un clúster de Macrodatos de SQL son miembros de un clúster de HDFS.

![Arquitectura del grupo de almacenamiento](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>Responsabilidades

Son responsables de los nodos de almacenamiento:

- Ingesta de datos a través de Spark.
- Almacenamiento de datos en HDFS (formato Parquet). HDFS también proporciona persistencia de datos, como datos HDFS se reparten entre todos los nodos de almacenamiento en el clúster de SQL Big Data.
- Acceso a datos a través de extremos HDFS y SQL Server.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, consulte la información general siguiente:

- [¿Qué es SQL Server 2019 macrodatos clústeres?](big-data-cluster-overview.md)
