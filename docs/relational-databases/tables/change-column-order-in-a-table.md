---
title: Cambio del orden de las columnas en una tabla | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], change order in a table
- column order, change
ms.assetid: cd99ef56-9085-431a-a0fc-58e7add5399f
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 5490f611a754e13faf436857bb0c65c0b3aad3f7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39543925"
---
# <a name="change-column-order-in-a-table"></a>Cambiar el orden de las columnas de una tabla
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Puede cambiar el orden de las columnas en el Diseñador de tablas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!CAUTION]  
>  Si cambia el orden de las columnas de una tabla, el código y las aplicaciones que dependen de un orden de columnas determinado pueden verse afectados. Los elementos afectados pueden ser consultas, vistas, procedimientos almacenados, funciones definidas por el usuario y aplicaciones cliente. Tenga en cuenta las consecuencias antes de realizar cualquier cambio en el orden de las columnas. El procedimiento recomendado es especificar el orden en que las columnas se devuelven en el nivel de aplicación y de consulta. No debe confiar en el uso de SELECT * para devolver todas las columnas en un orden esperado según el orden en que están definidos en la tabla. Especifique siempre las columnas por nombre en las consultas y aplicaciones en el orden en que desea que aparezcan.  
  
 **En este tema**  
  
-   **Para cambiar el orden de las columnas con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-change-the-column-order"></a>Para cambiar el orden de las columnas  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en la tabla cuyas columnas quiera reordenar y seleccione **Diseñar**.  
  
2.  Seleccione la casilla que hay a la izquierda del nombre de la columna cuyo orden desea cambiar.  
  
3.  Arrastre la columna a otra ubicación en la tabla.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para cambiar el orden de las columnas**  
  
 Esta tarea no se puede realizar mediante instrucciones Transact-SQL.  
  
###  <a name="TsqlExample"></a>  
