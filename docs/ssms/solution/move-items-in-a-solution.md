---
title: "Mover elementos en una solución | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-solutions
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- moving items
- solutions [SQL Server Management Studio], item relocation
- relocating items
ms.assetid: b40a24eb-f528-4e70-b26e-5eaf6e0ed1ed
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e549c4943173ccf23c62c0e12f53cd8203aa064
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="move-items-in-a-solution"></a>Mover elementos en una solución
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Los elementos de proyecto en los proyectos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] son las consultas, conexiones y archivos varios. Puede mover consultas y archivos varios entre proyectos en el Explorador de soluciones. Sin embargo, las conexiones no se pueden mover.  
  
### <a name="to-move-items-in-solution-explorer"></a>Para mover elementos en el Explorador de soluciones  
  
1.  En el Explorador de soluciones, seleccione el elemento que desea mover.  
  
2.  En el menú **Editar** , haga clic en **Cortar**.  
  
3.  En el Explorador de soluciones, seleccione el destino.  
  
4.  En el menú **Editar** , haga clic en **Pegar**.  
  
Puede mover elementos si arrastra consultas y archivos varios dentro del Explorador de soluciones. La acción de arrastrarlos permite ver el resultado de la operación. El mover consultas de un tipo de proyecto a otro puede dar lugar a que éstas se consideren del tipo archivos varios en el proyecto de destino.  
  
> [!NOTE]  
> El mover una consulta conectada no mueve la conexión al proyecto de destino. La consulta perderá su conexión si se mueve al proyecto de destino.  
  
## <a name="see-also"></a>Ver también  
[Explorador de soluciones](../../ssms/solution/solution-explorer.md)  
[Copiar elementos de una solución](../../ssms/solution/copy-items-in-a-solution.md)  
  
