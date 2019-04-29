---
title: 'Paso 3: Probar el paquete del Tutorial lección 3 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ac1aa0c45e8201d50ead862dd1631bbb3324c8e3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62891593"
---
# <a name="step-3-testing-the-lesson-3-tutorial-package"></a>Paso 3: Prueba del paquete del tutorial de la lección 3
  En esta tarea, ejecutará el paquete Lesson 3.dtsx. Al ejecutar el paquete, en la ventana Registrar eventos se mostrará una lista de las entradas del registro que se escriben en el archivo de registro. Una vez que haya finalizado la ejecución del paquete, comprobará el contenido del archivo de registro generado por el proveedor de registro.  
  
## <a name="checking-the-package-layout"></a>Comprobar el diseño del paquete  
 Antes de probar el paquete, debe comprobar que los flujos de datos y de control de la lección 3 contienen los objetos mostrados en los diagramas siguientes. El flujo de control debe ser idéntico al flujo de datos de la lección 2. El flujo de datos debe ser idéntico al flujo de datos de las lecciones 1 y 2.  
  
 **Flujo de control**  
  
 ![Flujo de control del paquete](../../2014/tutorials/media/task4lesson2control.gif "Control flow in package")  
  
 **Flujo de datos**  
  
 ![Flujo de datos del paquete](../../2014/tutorials/media/task9lesson1data.gif "Data flow in package")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>Para ejecutar el paquete de tutorial de la lección 4  
  
1.  En el menú SSIS, haga clic en Registrar eventos.  
  
2.  En el menú **Depurar** , haga clic en **Iniciar depuración**.  
  
3.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar** , haga clic en **Detener depuración**.  
  
### <a name="to-examine-the-generated-log-file"></a>Para examinar el archivo de registro generado  
  
-   Mediante el Bloc de notas o cualquier otro editor de texto, abra el archivo TutorialLog.log.  
  
-   Aunque la semántica de la información generada para el `PipelineExecutionPlan` y `PipelineExecutionTrees` eventos están fuera del ámbito de este tutorial, puede ver que la primera línea enumera los campos de información especificados en el **detalles** ficha de el **configurar registros de SSIS** cuadro de diálogo. Además, puede comprobar que los dos eventos que ha seleccionado, PipelineExecutionPlan y PipelineExecutionTrees, se han registrado para cada iteración del bucle Foreach.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 4: Agregar redirección de flujo de Error](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
