---
title: 'Tarea 9: Adición de unión de todo transformar para combinar registros correctos y corregidos | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 24ba466d-a7d3-49e7-9111-b348399c9e58
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 2a3861e7de24e4fdf43ea11cf447b448c9d17b48
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62866438"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>Tarea 9: Adición de la transformación Unión de todo para combinar los registros correctos y corregidos
  En esta tarea, agregará la transformación Unión de todo al flujo de datos. La transformación Unión de todo combina varias entradas en una salida. En su escenario, combina los registros Correctos y Corregidos en un flujo.  
  
1.  Arrastrar y colocar **unión de todo** transformar de **común** sección de la **cuadro de herramientas de SSIS** a la **de flujo de datos** pestaña y colóquelo bajo **Elegir registros correctos y corregidos**.  
  
2.  Haga clic en **Union All** transformar en el **de flujo de datos** ficha y haga clic en **cambiar el nombre**. Tipo **combinar registros correctos y corregidos**y presione **ENTRAR**.  
  
     ![Combinar correctos y corregidos Reocrds](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "combinar Reocrds correctos y corregidos")  
  
3.  Conectar **elegir registros correctos y corregidos** a **combinar registros correctos y corregidos** en el **de flujo de datos** ficha mediante el conector azul. Debería ver el **selección de entrada y salida** cuadro de diálogo.  
  
4.  En el **entrada salida** cuadro de diálogo, seleccione **correcto** para **salida** y haga clic en **Aceptar**.  
  
     ![Cuadro de diálogo de selección de salida de entrada](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "salida cuadro de diálogo de selección de entrada")  
  
5.  Mueva el conector denominado **correcto** a la izquierda arrastrando y colocando el punto al final del conector a la izquierda.  
  
     ![Conexión-corrección para combinar correctos y corregidos](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "conexión-corrección para combinar correctos y corregidos")  
  
6.  Si selecciona **elegir registros correctos y corregidos** transformar, debería ver otro conector azul. Arrastre el conector azul hasta **combinar registros correctos y corregidos**.  
  
     ![Conexión-corregidos para combinar correctos y corregidos](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "conexión-corregidos para combinar correctos y corregidos")  
  
7.  Esto **conector** debe tener el título **corregido**. Puesto que tiene solo dos condiciones **correcto** y **corregido**, y ya se ha utilizado una condición, el **selección de entrada y salida** cuadro de diálogo no se muestra en este momento. Si los conectores se superponen, mueva uno hacia la izquierda y el otro hacia la derecha arrastrando el conector hacia la izquierda o hacia la derecha.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 10: Agregar la transformación Agrupación aproximada para identificar duplicados](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  
