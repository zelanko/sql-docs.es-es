---
title: Calcular el tamaño de una tabla | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 29
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8410df06898ed7c536c8a6bc8c368c1ec68d6457
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113128"
---
# <a name="estimate-the-size-of-a-table"></a>Calcular el tamaño de una tabla
  Los siguientes pasos pueden utilizarse para calcular el espacio necesario para almacenar datos en una tabla:  
  
1.  Calcular el espacio necesario para el montón o para el índice agrupado siguiendo las instrucciones indicadas en [Estimar el tamaño de un montón](estimate-the-size-of-a-heap.md) o en [Estimar el tamaño de un índice agrupado](estimate-the-size-of-a-clustered-index.md).  
  
2.  Calcular el espacio necesario para cada índice no agrupado mediante las instrucciones que se detallan en [Estimar el tamaño de un índice no agrupado](estimate-the-size-of-a-nonclustered-index.md).  
  
3.  Sumar los valores calculados en los pasos 1 y 2.  
  
## <a name="see-also"></a>Vea también  
 [Estimar el tamaño de una base de datos](estimate-the-size-of-a-database.md)   
 [Estimar el tamaño de un montón](estimate-the-size-of-a-heap.md)   
 [Estimar el tamaño de un índice agrupado](estimate-the-size-of-a-clustered-index.md)   
 [Estimar el tamaño de un índice no agrupado](estimate-the-size-of-a-nonclustered-index.md)  
  
  