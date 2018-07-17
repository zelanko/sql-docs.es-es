---
title: Programar las directivas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 59417a54-55f1-4468-ba41-368aa852c2d4
caps.latest.revision: 5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: c328073f25c27ff05b8b6edbd79a56ad1fda85ab
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37315135"
---
# <a name="schedule-the-policies"></a>Programar las directivas
  En esta tarea, programará las directivas de prácticas recomendadas que importó en la tarea anterior.  
  
### <a name="to-schedule-the-best-practices-policies"></a>Para programar las directivas de prácticas recomendadas  
  
1.  En el Explorador de objetos, expanda **administración**, expanda **administración de directivas**, expanda **directivas**, haga clic en una directiva de prácticas recomendadas y, a continuación, haga clic en  **Propiedades**.  
  
    > [!NOTE]  
    >  Como alternativa, para ver fácilmente qué directivas están asociadas con los procedimientos recomendados y ordenar las mejores prácticas categorías, expanda **administración**, expanda **administración de directivas**y, a continuación, haga clic en **Directivas**. En el menú **Ver** , haga clic en **Detalles del Explorador de objetos**. En el **detalles del explorador de objetos** panel, haga clic en el **categoría** encabezado para ordenar las directivas por categoría. Las directivas de prácticas recomendadas tienen el prefijo **prácticas recomendadas de Microsoft**. Haga clic en la directiva que desea configurar y, a continuación, haga clic en **propiedades**.  
  
2.  En el **General** página de la **Abrir directiva** cuadro de diálogo el **modo de evaluación** lista, haga clic en **según programación**.  
  
3.  Junto a la **programación** cuadro, haga clic en **elegir** para especificar una programación existente o haga clic en **New** para crear una nueva programación.  
  
4.  Después de haber configurado una programación, puede seleccionar la **habilitado** casilla de verificación junto a la parte superior de la página para habilitar la directiva programada.  
  
5.  Repita los pasos 1 a 4 con cada directiva que desee programar.  
  
    > [!NOTE]  
    >  Para ver los resultados de la evaluación después de la ejecución de una directiva programada, abra el registro de historial de directivas en la instancia de destino. Para abrir el registro, haga clic en **administración de directivas**y, a continuación, haga clic en **Ver historial**.  
  
## <a name="summary"></a>Resumen  
 Configuró las directivas programadas para ejecutarse en una instancia única de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Si desea implementarlas en varias instancias, continúe con la siguiente tarea de este tutorial.  
  
## <a name="next-steps"></a>Pasos siguientes  
 [Implementar directivas programadas en varias instancias](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
  
