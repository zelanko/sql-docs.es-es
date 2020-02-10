---
title: 'Tarea 9: agregar una transformación Unión de todo para combinar los registros correctos y corregidos | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 24ba466d-a7d3-49e7-9111-b348399c9e58
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 93b160b6e513ad866126df8b401b82ee1270be84
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489651"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>Tarea 9: agregar la transformación Unión de todo para combinar los registros correctos y corregidos
  En esta tarea, agregará la transformación Unión de todo al flujo de datos. La transformación Unión de todo combina varias entradas en una salida. En su escenario, combina los registros Correctos y Corregidos en un flujo.  
  
1.  Arrastre y coloque **UNION ALL** Transform desde la sección **común** del **cuadro de herramientas de SSIS** hasta la pestaña **flujo de datos** y colóquela en **seleccionar registros correctos y corregidos**.  
  
2.  Haga clic con el botón secundario en transformación **Unión de todo** en la pestaña **flujo de datos** y haga clic en **cambiar nombre**. Escriba **combinar registros correctos y corregidos**y presione **entrar**.  
  
     ![Combinar registros correctos y corregidos](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "Combinar registros correctos y corregidos")  
  
3.  Conecte **Seleccione los registros correctos y corregidos** para **combinar los registros correctos y corregidos** en la pestaña **flujo de datos** mediante el conector azul. Debería ver el cuadro de diálogo **selección de entrada y salida** .  
  
4.  En el cuadro de diálogo **salida de entrada** , seleccione **correcto** en **salida** y haga clic en **Aceptar**.  
  
     ![Cuadro de diálogo Selección de entrada y salida](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "Cuadro de diálogo Selección de entrada y salida")  
  
5.  Mueva el conector con el título **correcto** a la izquierda arrastrando y soltando el punto al final del conector a la izquierda.  
  
     ![Conexión - Corrección para Combinar correctos y corregidos](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "Conexión - Corrección para Combinar correctos y corregidos")  
  
6.  Si selecciona la transformación seleccionar **los registros correctos y corregidos** , debería ver otro conector azul. Arrastre ese conector azul para **combinar los registros correctos y corregidos**.  
  
     ![Conexión - Corregidos para Combinar correctos y corregidos](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "Conexión - Corregidos para Combinar correctos y corregidos")  
  
7.  El título de este **conector** debe ser **corregido**. Puesto que solo tiene dos condiciones de **corrección** y **corrección, y**una condición ya se ha usado, el cuadro de diálogo Selección de **salida de entrada** no se muestra en este momento. Si los conectores se superponen, mueva uno hacia la izquierda y el otro hacia la derecha arrastrando el conector hacia la izquierda o hacia la derecha.  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 10: agregar la transformación Agrupación aproximada para identificar duplicados](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  
