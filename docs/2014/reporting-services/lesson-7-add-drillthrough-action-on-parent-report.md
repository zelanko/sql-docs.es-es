---
title: 'Lección 7: Agregar una acción de obtención de detalles en el informe primario | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: aad2da1a-d7b1-4afa-a66a-1ff102e8306f
caps.latest.revision: 9
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 4692e2403cbe6ced24d09fb2a554f9a85b475b95
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199614"
---
# <a name="lesson-7-add-drillthrough-action-on-parent-report"></a>Lección 7: Agregar una acción de obtención de detalles en el informe primario
  Después de agregar un control ReportViewer a la aplicación de sitio Web, el paso siguiente consiste en agregar una acción de obtención de detalles en el informe primario.  
  
### <a name="to-add-drillthrough-action-on-the-parent-report"></a>Para agregar una acción de obtención de detalles en el informe primario  
  
1.  Vaya al informe primario.  
  
2.  Haga clic en el cuadro de texto que contiene el valor de **nombre**.  
  
3.  Haga clic en el cuadro de texto y, a continuación, haga clic en **propiedades de cuadro de texto**.  
  
4.  Vaya a la pestaña **Acción** y seleccione la opción **Ir a informe** .  
  
5.  Escriba el nombre del informe secundario en la sección **Especificar un informe** .  
  
6.  Haga clic en **agregar** en **utilizar estos parámetros para ejecutar el informe** sección.  
  
7.  Tipo de **productid** en el **nombre** cuadro y, a continuación, haga clic en **ProductID** en el **valor** lista desplegable.  
  
8.  Haga clic en **Aceptar** para finalizar.  
  
## <a name="next-task"></a>Tarea siguiente  
 Ha agregado correctamente una acción de obtención de detalles en el informe primario. A continuación, creará un filtro de los datos para la tabla de datos que definió para el informe secundario.  
  
  