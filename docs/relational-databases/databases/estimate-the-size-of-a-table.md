---
title: Calcular el tamaño de una tabla | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 49e63511a23b670575f517640bb0b9f0eb06870a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "72909030"
---
# <a name="estimate-the-size-of-a-table"></a>Calcular el tamaño de una tabla
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Los siguientes pasos pueden utilizarse para calcular el espacio necesario para almacenar datos en una tabla:  
  
1.  Calcular el espacio necesario para el montón o para el índice agrupado siguiendo las instrucciones indicadas en [Estimar el tamaño de un montón](../../relational-databases/databases/estimate-the-size-of-a-heap.md) o en [Estimar el tamaño de un índice agrupado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md).  
  
2.  Calcular el espacio necesario para cada índice no agrupado mediante las instrucciones que se detallan en [Estimar el tamaño de un índice no agrupado](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md).  
  
3.  Sumar los valores calculados en los pasos 1 y 2.  

## <a name="see-also"></a>Consulte también  
 [Estimar el tamaño de una base de datos](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [Estimar el tamaño de un montón](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Estimar el tamaño de un índice agrupado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Estimar el tamaño de un índice no clúster](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  
