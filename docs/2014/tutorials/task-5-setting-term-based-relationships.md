---
title: 'Tarea 5: Configurar basadas en términos relaciones | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
caps.latest.revision: 8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f3718b42bfb1eb7b2736bf936311e3b0b309e92
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37214215"
---
# <a name="task-5-setting-term-based-relationships"></a>Tarea 5: configurar relaciones basadas en términos
  En esta tarea, definirá algunas relaciones basadas en términos para los valores de la **Supplier Name** dominio. Una relación basada en términos permite realizar una corrección para un término que forma parte de un valor en un dominio. Permiten considerar como sinónimos idénticos varios valores que son idénticos salvo por la ortografía de una parte común. Por ejemplo, **Inc.** puede corregirse a **Incorporated**. DQS emplea estas relaciones en los procesos de detección de conocimiento, limpieza o coincidencia. Consulte [crear relaciones basadas en términos](http://msdn.microsoft.com/library/hh510404.aspx) para obtener más detalles.  
  
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
  
  
