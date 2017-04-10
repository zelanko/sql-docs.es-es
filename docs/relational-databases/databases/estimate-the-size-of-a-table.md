---
title: "Calcular el tama&#241;o de una tabla | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "páginas [SQL Server], espacio"
  - "espacio [SQL Server], tablas"
  - "tamaño de fila [SQL Server]"
  - "tamaño [SQL Server], tablas"
  - "tamaño de columna [SQL Server]"
  - "predecir tamaño de tabla [SQL Server]"
  - "tamaño de índice [SQL Server]"
  - "estimar tamaño de tabla"
  - "índices agrupados, tamaño de tabla"
  - "espacio en disco [SQL Server], tablas"
  - "asignación de espacio [SQL Server], tamaño de la tabla"
  - "diseñar bases de datos [SQL Server], estimar tamaño"
  - "filas libres reservadas por página [SQL Server]"
  - "calcular tamaño de tabla"
ms.assetid: 15c17c92-616f-402e-894b-907a296efe5f
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# Calcular el tama&#241;o de una tabla
  Los siguientes pasos pueden utilizarse para calcular el espacio necesario para almacenar datos en una tabla:  
  
1.  Calcular el espacio necesario para el montón o para el índice agrupado siguiendo las instrucciones indicadas en [Estimar el tamaño de un montón](../../relational-databases/databases/estimate-the-size-of-a-heap.md) o en [Estimar el tamaño de un índice agrupado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md).  
  
2.  Calcular el espacio necesario para cada índice no agrupado mediante las instrucciones que se detallan en [Estimar el tamaño de un índice no agrupado](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md).  
  
3.  Sumar los valores calculados en los pasos 1 y 2.  
  
## Vea también  
 [Estimar el tamaño de una base de datos](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [Estimar el tamaño de un montón](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Estimar el tamaño de un índice clúster](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Estimar el tamaño de un índice no clúster](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  