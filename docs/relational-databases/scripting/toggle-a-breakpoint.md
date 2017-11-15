---
title: "Alternar un punto de interrupción | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c477ab89-a1cd-4f2c-aa7c-40525041100f
caps.latest.revision: "5"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1323ff3e4849a06192bd4aec71f61daf376cbb09
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="toggle-a-breakpoint"></a>Alternar un punto de interrupción
  El hecho de establecer un punto de interrupción en una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] se denomina alternar un punto de interrupción.  
  
## <a name="breakpoints"></a>Puntos de interrupción  
 Una vez establecido el punto de interrupción, se representa mediante un icono en la barra gris situada a la izquierda de la instrucción. El icono se denomina glifo de punto de interrupción. [!INCLUDE[tsql](../../includes/tsql-md.md)] se aplican a instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] completadas. Cuando se alterna un punto de interrupción, el depurador resalta la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] asociada.  
  
 Si hay varias instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] en una línea, puede alternar un punto de interrupción para cada instrucción. Al hacer clic en la barra gris de la izquierda de la ventana se alterna un punto de interrupción en la primera instrucción de la línea. Para alternar un punto de interrupción en una instrucción subsiguiente, resalte cualquier parte de la instrucción o mueva el cursor a la instrucción y, a continuación, presione F9 o haga clic en **Alternar punto de interrupción** en el menú **Depurar** . Si hay varios puntos de interrupción en una línea, solo hay un glifo de punto de interrupción en la barra gris de la izquierda.  
  
 Una vez que se ha alternado un punto de interrupción, puede realizar diversas acciones en el punto de interrupción, como editar sus propiedades o deshabilitarlo provisionalmente. Para obtener más información, vea [Utilizar puntos de interrupción de Transact-SQL](../../relational-databases/scripting/transact-sql-breakpoints.md).  
  
## <a name="toggle-a-breakpoint"></a>Alternar un punto de interrupción  
 **Para alternar un punto de interrupción en una instrucción Transact-SQL**  
  
1.  Haga clic en la barra deshabilitada situada a la izquierda de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
2.  Alternativamente, puede resaltar cualquier parte de la instrucción o mover el cursor a la instrucción y, a continuación, realizar cualquiera de las acciones siguientes:  
  
    -   Presione F9.  
  
    -   En el menú **Depurar** , haga clic en **Alternar punto de interrupción**.  
  
  
