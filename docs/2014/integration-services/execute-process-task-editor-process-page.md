---
title: Ejecutar el Editor de la tarea de proceso (página procesar) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executeprocesstask.process.f1
helpviewer_keywords:
- Execute Process Task Editor
ms.assetid: 0fc22406-e79b-47a4-a7e4-108d4ce6202f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fa799404777f8f0ef0a8a07a81c8c7961c636004
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059029"
---
# <a name="execute-process-task-editor-process-page"></a>Editor de la tarea Ejecutar proceso (página Procesar)
  Utilice la página **Proceso** del cuadro de diálogo **Editor de la tarea Ejecutar proceso** para configurar las opciones que permitirán ejecutar el proceso. Estas opciones incluyen el ejecutable que se debe instalar, su ubicación, los argumentos de línea de comandos y las variables que proporcionan información de entrada y capturan información de salida.  
  
 Para obtener información acerca de esta tarea, vea [Execute Process Task](control-flow/execute-process-task.md).  
  
## <a name="options"></a>Opciones  
 **RequireFullFileName**  
 Indica si la tarea debe generar un error en caso de que no se encuentre el ejecutable en la ubicación específica.  
  
 **Executable**  
 Escriba el nombre del ejecutable que desea instalar.  
  
 **Argumentos**  
 Proporcione los argumentos de línea de comandos.  
  
 **WorkingDirectory**  
 Escriba la ruta de acceso de la carpeta que contiene el ejecutable, o bien haga clic en el botón Examinar **(…)** y busque la carpeta.  
  
 **StandardInputVariable**  
 Seleccione una variable para proporcionar la entrada al proceso o haga clic en \<**Nueva variable…**> para crear una:  
  
 **Temas relacionados:**  [Agregar variable](../../2014/integration-services/add-variable.md)  
  
 **StandardOutputVariable**  
 Seleccione una variable para capturar la salida del proceso o haga clic en \<**Nueva variable…**> para crear una.  
  
 **StandardErrorVariable**  
 Seleccione una variable para capturar la salida de error del procesador o haga clic en \<**Nueva variable…**> para crear una.  
  
 **FailTaskIfReturnCodeIsNotSuccessValue**  
 Esta opción indica si la tarea genera un error porque el código de salida del proceso es diferente del valor especificado en **SuccessValue**.  
  
 **SuccessValue**  
 Especifique el valor que devuelve el ejecutable para indicar su instalación correcta. De forma predeterminada, este valor está establecido en **0**.  
  
 **TimeOut**  
 Especifique el número de segundos que el proceso puede ejecutarse. El valor **0** indica que no se usará ningún valor de tiempo de espera y que el proceso se ejecutará hasta su conclusión o hasta que se produzca un error.  
  
 **TerminateProcessAfterTimeOut**  
 Esta opción indica si el proceso está obligado a finalizar después del período de tiempo de espera especificado con la opción **TimeOut** . Esta opción solo está disponible si el valor de **TimeOut** es distinto de **0**.  
  
 **WindowStyle**  
 Especifique el estilo de ventana en el que ejecutará el proceso.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Página Expresiones](expressions/expressions-page.md)  
  
  
