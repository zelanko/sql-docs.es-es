---
title: 'Tarea 5: Configurar basadas en términos relaciones | Documentos de Microsoft'
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
ms.topic: article
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b8450d3e77de578810bb57c35aafad6f90c8f19c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36102661"
---
# <a name="task-5-setting-term-based-relationships"></a>Tarea 5: configurar relaciones basadas en términos
  En esta tarea, definirá algunas relaciones basadas en términos para los valores de la **Supplier Name** dominio. Una relación basada en términos permite corregir términos que forman parte de un valor en un dominio. Permiten considerar como sinónimos idénticos varios valores que son idénticos salvo por la ortografía de una parte común. Por ejemplo, **Inc.** puede corregirse para **Incorporated**. DQS emplea estas relaciones en los procesos de detección de conocimiento, limpieza o coincidencia. Vea [crear relaciones basadas en Trérminos](http://msdn.microsoft.com/library/hh510404.aspx) para obtener más detalles.  
  
1.  Seleccione **Supplier Name** en el **lista de dominios**.  
  
2.  Cambie a la **relaciones basadas en términos** en el panel derecho.  
  
3.  Haga clic en **agregar nueva relación** botón en la barra de herramientas para agregar una relación a la tabla.  
  
4.  Tipo de **Co.** para el **valor** campo y **empresa** para el **corregir a** campo.  
  
5.  Repita los dos pasos anteriores para los valores siguientes:  
  
    |Valor|Corregir a|  
    |-----------|----------------|  
    |Corp.|Corporation|  
    |Inc.|Incorporated|  
  
     ![Relaciones basadas en términos](../../2014/tutorials/media/et-settingtermbasedrelations.jpg "relaciones basadas en términos")  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 6: Establecer sinónimos](../../2014/tutorials/task-6-setting-synonyms.md)  
  
  