---
title: Cambio del orden de las columnas en una tabla | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], change order in a table
- column order, change
ms.assetid: cd99ef56-9085-431a-a0fc-58e7add5399f
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d59f36bc315f6adf62d2ce8f09be4a1bb57bf428
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452893"
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
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-change-the-column-order"></a>Para cambiar el orden de las columnas  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en la tabla cuyas columnas quiera reordenar y seleccione **Diseñar**.  
  
2.  Seleccione la casilla que hay a la izquierda del nombre de la columna cuyo orden desea cambiar.  
  
3.  Arrastre la columna a otra ubicación en la tabla.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para cambiar el orden de las columnas**  
  
 Esta tarea no es compatible con las instrucciones Transact-SQL.  
  
###  <a name="TsqlExample"></a>  
