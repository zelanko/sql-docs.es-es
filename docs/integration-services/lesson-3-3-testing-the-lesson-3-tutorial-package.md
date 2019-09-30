---
title: 'Paso 3: Prueba del paquete del tutorial de la lección 3 | Microsoft Docs'
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9cdb19c6df46e3c24625bfb740c82771f0adcc1d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283180"
---
# <a name="lesson-3-3-test-the-lesson-3-tutorial-package"></a>Lección 3-3: Prueba del paquete del tutorial de la lección 3

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



En esta tarea, se ejecuta el paquete **Lesson 3.dtsx**. Mientras se ejecuta el paquete, en la ventana **Eventos de registro** se enumeran las entradas del registro que SSIS escribe en el archivo de registro por el proveedor de registro. Cuando finaliza la ejecución del paquete, puede ver el contenido del archivo de registro.  
  
## <a name="check-the-package-layout"></a>Comprobación del diseño del paquete  
Antes de probar el paquete, compruebe que los flujos de datos y de control del paquete de la lección 3 se parecen a los objetos mostrados en los diagramas siguientes. El flujo de control debe ser igual que en la lección 2, y el flujo de datos debe ser igual que en las lecciones 1 y 2.  
  
**Flujo de control**  
  
![Flujo de control del paquete](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**Flujo de datos**  
  
![Flujo de datos del paquete](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
## <a name="run-the-lesson-3-tutorial-package"></a>Ejecución del paquete del tutorial de la lección 3  
  
1.  En el menú SSIS, seleccione **Eventos de registro**.  
  
2.  En el menú **Depurar**, seleccione **Iniciar depuración**.  
  
3.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar**, seleccione **Detener depuración**.  
  
## <a name="examine-the-generated-log-file"></a>Examen del archivo de registro generado  
  
-   Mediante el Bloc de notas o cualquier otro editor de texto, abra el archivo TutorialLog.log.  
  
-   Una descripción completa de la información generada para los eventos **PipelineExecutionPlan** y **PipelineExecutionTrees** queda fuera del ámbito de este tutorial.  En el archivo de registro, puede ver que en la primera línea se enumeran los campos de información especificados en la pestaña **Detalles** del cuadro de diálogo **Configurar registros de SSIS**. También puede ver que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ha registrado los dos eventos que ha seleccionado, **PipelineExecutionPlan** y **PipelineExecutionTrees**,para cada iteración del bucle Foreach.  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 4: Adición de redireccionamiento de flujo de errores con SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
  
