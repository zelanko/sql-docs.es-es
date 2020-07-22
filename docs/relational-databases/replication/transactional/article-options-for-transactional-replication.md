---
title: Opciones de artículos para la replicación transaccional | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], transactional replication options
- transactional replication, article options
ms.assetid: 3469b185-0ea5-4690-a71c-717230d886b6
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 61e8bad960da0ff90f77e0253f39c6257ddb9c2c
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86904111"
---
# <a name="article-options-for-transactional-replication"></a>Opciones de artículos para la replicación transaccional
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Existen varias opciones para artículos en las publicaciones transaccionales. Con la replicación transaccional puede hacer lo siguiente:  
  
-   Especificar cómo se propagan los cambios desde el publicador a los suscriptores. Para más información, vea [Especificar cómo se propagan los cambios para los artículos transaccionales](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
-   Especificar que se replique la ejecución de un procedimiento almacenado. Esto resulta de utilidad al replicar los resultados de los procedimientos almacenados orientados al mantenimiento que afectan a grandes cantidades de datos. Para más información, vea [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
-   Especificar opciones de esquema, por ejemplo si las restricciones y los desencadenadores se copian en el suscriptor. Para obtener más información, vea [Especificar opciones de esquema](../../../relational-databases/replication/publish/specify-schema-options.md).  
  
-   Utilizar filtros de fila y columna. Filtrar artículos de tabla permite crear particiones de los datos que se van a publicar. Para obtener más información, vea [Filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
## <a name="see-also"></a>Consulte también  
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
