---
title: Programar las directivas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 59417a54-55f1-4468-ba41-368aa852c2d4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6b098f7929f762992f55995836dc03f95001e33d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063941"
---
# <a name="schedule-the-policies"></a>Programar las directivas
  En esta tarea, programará las directivas de prácticas recomendadas que importó en la tarea anterior.  
  
### <a name="to-schedule-the-best-practices-policies"></a>Para programar las directivas de prácticas recomendadas  
  
1.  En Explorador de objetos, expanda **Administración**, expanda **Administración de directivas**, expanda **directivas**, haga clic con el botón secundario en una directiva de prácticas recomendadas y, a continuación, haga clic en **propiedades**.  
  
    > [!NOTE]  
    >  Como alternativa, para ver fácilmente qué directivas están asociadas a los procedimientos recomendados y ordenar las categorías de prácticas recomendadas, expanda **Administración**, expanda **Administración de directivas**y, a continuación, haga clic en **directivas**. En el menú **Ver** , haga clic en **Detalles del Explorador de objetos**. En el panel de **detalles del explorador de objetos** , haga clic en el encabezado **categoría** para ordenar las directivas por categoría. Las directivas de prácticas recomendadas tienen el prefijo **prácticas recomendadas de Microsoft**. Haga clic con el botón secundario en la Directiva que desea configurar y, a continuación, haga clic en **propiedades**.  
  
2.  En la página **General** del cuadro de diálogo **abrir Directiva** , en la lista **modo de evaluación** , haga clic **en programación**.  
  
3.  Junto al cuadro **programación** , haga clic en **elegir** para especificar una programación existente o haga clic en **nuevo** para crear una nueva programación.  
  
4.  Después de configurar una programación, puede activar la casilla **habilitada** situada cerca de la parte superior de la página para habilitar la Directiva programada.  
  
5.  Repita los pasos 1 a 4 con cada directiva que desee programar.  
  
    > [!NOTE]  
    >  Para ver los resultados de la evaluación después de la ejecución de una directiva programada, abra el registro de historial de directivas en la instancia de destino. Para abrir el registro, haga clic con el botón secundario en **Administración de directivas**y, a continuación, haga clic en **Ver historial**.  
  
## <a name="summary"></a>Resumen  
 Configuró las directivas programadas para ejecutarse en una instancia única de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Si desea implementarlas en varias instancias, continúe con la siguiente tarea de este tutorial.  
  
## <a name="next-steps"></a>Pasos siguientes  
 [Implementar directivas programadas en varias instancias](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
  
