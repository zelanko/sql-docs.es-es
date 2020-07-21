---
title: 'Lección 9: Compilar y ejecutar la aplicación | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f52d3f3a-0b09-4b34-9112-0b3655271587
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b21ee398eade4878d4f2273f17314dd184af2310
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176871"
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

     ![obtención de detalles de SSRS mediante ReportViewer](../../2014/tutorials/media/ssrs-drillthrough-report.png "obtención de detalles de SSRS mediante ReportViewer")

5.  Cierre el explorador para salir.


