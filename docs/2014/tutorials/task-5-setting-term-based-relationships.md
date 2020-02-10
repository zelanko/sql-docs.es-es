---
title: 'Tarea 5: establecer relaciones basadas en términos | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0e9a6a1a96d208077e70c0cf1835cff6e34650dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489103"
---
# <a name="task-5-setting-term-based-relationships"></a>Tarea 5: configurar relaciones basadas en términos
  En esta tarea, se definen algunas relaciones basadas en términos para los valores del dominio **nombre de proveedor** . Una relación basada en términos permite corregir un término que forma parte de un valor en un dominio. Permiten considerar como sinónimos idénticos varios valores que son idénticos salvo por la ortografía de una parte común. Por ejemplo, **Inc.** se puede corregir en **Incorporated**. DQS emplea estas relaciones en los procesos de detección de conocimiento, limpieza o coincidencia. Vea [crear relaciones basadas en términos](https://msdn.microsoft.com/library/hh510404.aspx) para obtener más detalles.  
  
1.  Seleccione **nombre de proveedor** en la **lista de dominios**.  
  
2.  Cambie a la pestaña **relaciones basadas en términos** en el panel derecho.  
  
3.  Haga clic en el botón **Agregar nueva relación** en la barra de herramientas para agregar una relación a la tabla.  
  
4.  Escriba **Co.** en el campo **valor** y **compañía** para el campo **corregir a** .  
  
5.  Repita los dos pasos anteriores para los valores siguientes:  
  
    |Value|Corregir a|  
    |-----------|----------------|  
    |Corp.|Corporation|  
    |Inc.|Incorporated|  
  
     ![Relaciones basadas en términos](../../2014/tutorials/media/et-settingtermbasedrelations.jpg "Relaciones basadas en términos")  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 6: establecer sinónimos](../../2014/tutorials/task-6-setting-synonyms.md)  
  
  
