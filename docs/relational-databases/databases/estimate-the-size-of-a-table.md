---
title: Calcular el tamaño de una tabla | Microsoft Docs
description: Siga este procedimiento para estimar la cantidad de espacio necesario para almacenar datos en una tabla en SQL Server.
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
ms.openlocfilehash: d2cec3c9f67a07cb36c6ba7f4a11225b5544b252
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002191"
---
# <a name="estimate-the-size-of-a-table"></a>Calcular el tamaño de una tabla
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Los siguientes pasos pueden utilizarse para calcular el espacio necesario para almacenar datos en una tabla:  
  
1.  Calcular el espacio necesario para el montón o para el índice agrupado siguiendo las instrucciones indicadas en [Estimar el tamaño de un montón](../../relational-databases/databases/estimate-the-size-of-a-heap.md) o en [Estimar el tamaño de un índice agrupado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md).  
  
2.  Calcular el espacio necesario para cada índice no agrupado mediante las instrucciones que se detallan en [Estimar el tamaño de un índice no agrupado](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md).  
  
3.  Sumar los valores calculados en los pasos 1 y 2.  

## <a name="see-also"></a>Consulte también  
 [Estimar el tamaño de una base de datos](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [Estimar el tamaño de un montón](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Estimar el tamaño de un índice agrupado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Estimar el tamaño de un índice no clúster](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  
