---
title: "Calcular el tamaño de una tabla | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pages [SQL Server], space
- space [SQL Server], tables
- row size [SQL Server]
- size [SQL Server], tables
- column size [SQL Server]
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- clustered indexes, table size
- disk space [SQL Server], tables
- space allocation [SQL Server], table size
- designing databases [SQL Server], estimating size
- reserved free rows per page [SQL Server]
- calculating table size
ms.assetid: 15c17c92-616f-402e-894b-907a296efe5f
caps.latest.revision: "30"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8497c1279cda414e34334d9453ef4f5103a7d178
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="estimate-the-size-of-a-table"></a>Calcular el tamaño de una tabla
  Los siguientes pasos pueden utilizarse para calcular el espacio necesario para almacenar datos en una tabla:  
  
1.  Calcular el espacio necesario para el montón o para el índice agrupado siguiendo las instrucciones indicadas en [Estimar el tamaño de un montón](../../relational-databases/databases/estimate-the-size-of-a-heap.md) o en [Estimar el tamaño de un índice agrupado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md).  
  
2.  Calcular el espacio necesario para cada índice no agrupado mediante las instrucciones que se detallan en [Estimar el tamaño de un índice no agrupado](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md).  
  
3.  Sumar los valores calculados en los pasos 1 y 2.  
  
## <a name="see-also"></a>Vea también  
 [Estimar el tamaño de una base de datos](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [Estimar el tamaño de un montón](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Estimar el tamaño de un índice agrupado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Estimar el tamaño de un índice no agrupado](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  
