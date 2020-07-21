---
title: Mover elementos en una solución | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- moving items
- solutions [SQL Server Management Studio], item relocation
- relocating items
ms.assetid: b40a24eb-f528-4e70-b26e-5eaf6e0ed1ed
author: stevestein
ms.author: sstein
ms.openlocfilehash: fd0a8a89686c62b4d4d00aea5479bb956fe3011f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061146"
---
# <a name="move-items-in-a-solution"></a>Mover elementos en una solución
  Los elementos de proyecto en los proyectos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] son las consultas, las conexiones y los archivos varios. Puede mover consultas y archivos varios entre proyectos en el Explorador de soluciones. Sin embargo, las conexiones no se pueden mover.  
  
### <a name="to-move-items-in-solution-explorer"></a>Para mover elementos en el Explorador de soluciones  
  
1.  En el Explorador de soluciones, seleccione el elemento que desea mover.  
  
2.  En el menú **Editar** , haga clic en **Cortar**.  
  
3.  En el Explorador de soluciones, seleccione el destino.  
  
4.  En el menú **Editar** , haga clic en **Pegar**.  
  
 Puede mover elementos si arrastra consultas y archivos varios dentro del Explorador de soluciones. La acción de arrastrarlos permite ver el resultado de la operación. El mover consultas de un tipo de proyecto a otro puede dar lugar a que éstas se consideren del tipo archivos varios en el proyecto de destino.  
  
> [!NOTE]  
>  El mover una consulta conectada no mueve la conexión al proyecto de destino. La consulta perderá su conexión si se mueve al proyecto de destino.  
  
## <a name="see-also"></a>Consulte también  
 [Explorador de soluciones](solution-explorer.md)   
 [Copiar elementos de una solución](copy-items-in-a-solution.md)  
  
  
