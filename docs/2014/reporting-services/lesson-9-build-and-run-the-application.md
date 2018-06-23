---
title: 'Lección 9: Compilar y ejecutar la aplicación | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f52d3f3a-0b09-4b34-9112-0b3655271587
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: fdb619e98fe28742ac6b96acc6419513addfae25
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106049"
---
# <a name="lesson-9-build-and-run-the-application"></a>Lesson 9: Build and Run the Application
  Después de crear un filtro para los datos de la tabla de datos, el paso siguiente consiste en generar y ejecutar la aplicación del sitio Web.  
  
### <a name="to-build-and-run-the-application"></a>Para generar y ejecutar la aplicación  
  
1.  Pulse **CTRL+F5** para ejecutar la página Default.aspx sin depurar o pulse F5 para ejecutar la página con la depuración.  
  
     Como parte del proceso de compilación, se compila el informe y los errores detectados (por ejemplo, un error de sintaxis en una expresión usada en el informe) se agregan a la **Lista de tareas** que se encuentra en la parte inferior de la ventana de Visual Studio.  
  
     La página Web aparece en el explorador. El control ReportViewer muestra el informe. Puede utilizar la barra de herramientas para navegar por el informe, ampliarlo y exportarlo a Excel.  
  
2.  Mantenga el mouse sobre alguna de las filas bajo la columna **Nombre** . El cursor del mouse mostrará un símbolo de mano.  
  
3.  Haga clic en un valor de la columna **Nombre** . El informe secundario se muestra con los datos filtrados correspondientes.  
  
4.  Haga clic en el icono, **Volver al informe primario**, en la barra de herramientas de **ReportViewer** para navegar de nuevo al informe **Primario** .  
  
     ![obtención de SSRS mediante ReportViewer](../../2014/tutorials/media/ssrs-drillthrough-report.png "ssrs obtención de detalles mediante ReportViewer")  
  
5.  Cierre el explorador para salir.  
  
  