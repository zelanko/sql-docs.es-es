---
title: 'Paso 3: Probar el paquete del tutorial de la lección 3 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b6b446d566e7c9aa18e635799e81120d1ac73470
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965179"
---
# <a name="step-3-testing-the-lesson-3-tutorial-package"></a>Paso 3: Prueba del paquete del tutorial de la lección 3
  En esta tarea, ejecutará el paquete Lesson 3.dtsx. Al ejecutar el paquete, en la ventana Registrar eventos se mostrará una lista de las entradas del registro que se escriben en el archivo de registro. Una vez que haya finalizado la ejecución del paquete, comprobará el contenido del archivo de registro generado por el proveedor de registro.  
  
## <a name="checking-the-package-layout"></a>Comprobar el diseño del paquete  
 Antes de probar el paquete, debe comprobar que los flujos de datos y de control de la lección 3 contienen los objetos mostrados en los diagramas siguientes. El flujo de control debe ser idéntico al flujo de datos de la lección 2. El flujo de datos debe ser idéntico al flujo de datos de las lecciones 1 y 2.  
  
 **Flujo de control**  
  
 ![Flujo de control del paquete](../../2014/tutorials/media/task4lesson2control.gif "Flujo de control del paquete")  
  
 **Flujo de datos**  
  
 ![Flujo de datos del paquete](../../2014/tutorials/media/task9lesson1data.gif "Flujo de datos del paquete")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>Para ejecutar el paquete de tutorial de la lección 4  
  
1.  En el menú SSIS, haga clic en Registrar eventos.  
  
2.  En el menú **Depurar** , haga clic en **Iniciar depuración**.  
  
3.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar** , haga clic en **Detener depuración**.  
  
### <a name="to-examine-the-generated-log-file"></a>Para examinar el archivo de registro generado  
  
-   Mediante el Bloc de notas o cualquier otro editor de texto, abra el archivo TutorialLog.log.  
  
-   Aunque la semántica de la información generada para los `PipelineExecutionPlan` `PipelineExecutionTrees` eventos y está fuera del ámbito de este tutorial, puede ver que la primera línea muestra los campos de información especificados en la pestaña **detalles** del cuadro de diálogo **configurar registros de SSIS** . Además, puede comprobar que los dos eventos que ha seleccionado, PipelineExecutionPlan y PipelineExecutionTrees, se han registrado para cada iteración del bucle Foreach.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 4: Adición de redirección de flujo de errores](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
