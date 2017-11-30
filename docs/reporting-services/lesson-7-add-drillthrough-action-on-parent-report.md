---
title: "Lección 7: Agregar una acción de obtención de detalles en el informe primario | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: aad2da1a-d7b1-4afa-a66a-1ff102e8306f
caps.latest.revision: "13"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 977cc53de149275d6eb9e6a80c0687cce9fea3d8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-7-add-drillthrough-action-on-parent-report"></a>Lección 7: Agregar una acción de obtención de detalles en el informe primario
Después de agregar un control ReportViewer a la aplicación de sitio Web, el paso siguiente consiste en agregar una acción de obtención de detalles en el informe primario.  
  
### <a name="to-add-drillthrough-action-on-the-parent-report"></a>Para agregar una acción de obtención de detalles en el informe primario  
  
1.  Vaya al informe primario.  
  
2.  Seleccione el cuadro de texto que contiene el valor **Nombre**.  
  
3.  Haga clic con el botón derecho en el cuadro de texto y, después, haga clic en **Propiedades de cuadro de texto**.  
  
4.  Vaya a la pestaña **Acción** y seleccione la opción **Ir a informe** .  
  
5.  Escriba el nombre del informe secundario en la sección **Especificar un informe** .  
  
    > [!NOTE]
    > No incluya la extensión de archivo en el nombre del informe.  
  
6.  Seleccione **Agregar** en la sección **Usar estos parámetros para ejecutar el informe** .  
  
7.  Escriba **productid** en el cuadro **Nombre** y luego seleccione **ProductID** en la lista desplegable **Valor** .  
  
8.  Seleccione **Aceptar** para finalizar.  
  
## <a name="next-task"></a>Tarea siguiente  
Ha agregado correctamente una acción de obtención de detalles en el informe primario. A continuación, creará un filtro de los datos para la tabla de datos que definió para el informe secundario. Consulte [Lección 8: Crear un filtro de datos](../reporting-services/lesson-8-create-a-data-filter.md).  
  
  
  

