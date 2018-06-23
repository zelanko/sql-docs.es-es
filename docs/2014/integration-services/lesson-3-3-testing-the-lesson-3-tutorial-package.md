---
title: 'Paso 3: Probar el paquete del tutorial de la lección 3 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
caps.latest.revision: 27
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 03a681cf4ab018d82d991b91c463dfbef3fe8d73
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197206"
---
# <a name="step-3-testing-the-lesson-3-tutorial-package"></a>Paso 3: Probar el paquete del tutorial de la lección 3
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
  
-   Aunque la semántica de la información generada para la `PipelineExecutionPlan` y `PipelineExecutionTrees` eventos están fuera del ámbito de este tutorial, puede ver que la primera línea enumera los campos de información especificados en el **detalles** ficha de el **configurar registros de SSIS** cuadro de diálogo. Además, puede comprobar que los dos eventos que ha seleccionado, PipelineExecutionPlan y PipelineExecutionTrees, se han registrado para cada iteración del bucle Foreach.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 4: Agregar redirección de flujo de Error](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  