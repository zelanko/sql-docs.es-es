---
title: 'Tarea 5: Configurar basadas en términos relaciones | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 322c5a5afcd7c5d82982a86cb9398e66bb248c5d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034456"
---
# <a name="task-5-setting-term-based-relationships"></a>Tarea 5: configurar relaciones basadas en términos
  En esta tarea, definirá algunas relaciones basadas en términos para los valores de la **Supplier Name** dominio. Una relación basada en términos permite realizar una corrección para un término que forma parte de un valor en un dominio. Permiten considerar como sinónimos idénticos varios valores que son idénticos salvo por la ortografía de una parte común. Por ejemplo, **Inc.** puede corregirse a **Incorporated**. DQS emplea estas relaciones en los procesos de detección de conocimiento, limpieza o coincidencia. Consulte [crear relaciones basadas en términos](https://msdn.microsoft.com/library/hh510404.aspx) para obtener más detalles.  
  
1.  Seleccione **Supplier Name** en el **lista de dominios**.  
  
2.  Cambie a la **relaciones basadas en términos** ficha en el panel derecho.  
  
3.  Haga clic en **agregar nueva relación** en la barra de herramientas para agregar una relación a la tabla.  
  
4.  Tipo **Co.** para el **valor** campo y **empresa** para el **corregir a** campo.  
  
5.  Repita los dos pasos anteriores para los valores siguientes:  
  
    |Valor|Corregir a|  
    |-----------|----------------|  
    |Corp.|Corporation|  
    |Inc.|Incorporated|  
  
     ![Relaciones basadas en términos](../../2014/tutorials/media/et-settingtermbasedrelations.jpg "relaciones basadas en términos")  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 6: Establecer sinónimos](../../2014/tutorials/task-6-setting-synonyms.md)  
  
  
