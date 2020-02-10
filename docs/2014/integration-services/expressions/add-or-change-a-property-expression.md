---
title: Agregar o cambiar una expresión de propiedad | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], creating
- expressions [Integration Services], property expressions
ms.assetid: cb5da499-065f-4fa6-9f6d-5bc5f385241e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bd9095a11ef304c256b6c5a60560a71866e744fd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62899023"
---
# <a name="add-or-change-a-property-expression"></a>Agregar o cambiar una expresión de propiedad
  Puede crear expresiones de propiedad para paquetes, tareas, contenedores de bucles ForEach, contenedores de bucles For, contenedores de secuencias, controladores de eventos, administradores de conexión de paquetes y proyectos, y proveedores de registro.  
  
 Para crear o cambiar expresiones de propiedad, puede utilizar el **Editor de expresiones de propiedad** o el **Generador de expresiones**. Se puede tener acceso al **Editor de expresiones de propiedad** desde los editores personalizados que están disponibles para tareas y contenedores, o desde la ventana **Propiedades** . Se puede tener acceso al**Generador de expresiones** desde el **Editor de expresiones de propiedad**. Aunque puede escribir expresiones en el **Editor de expresiones de propiedad** o en el **Generador de expresiones**, el **Generador de expresiones** proporciona un conjunto gráfico de herramientas que simplifica el proceso de generar expresiones complejas.  
  
 Para obtener más información sobre la sintaxis, los operadores y las funciones que proporciona [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md) y [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md). El tema de cada operador o función incluye ejemplos de uso de ese operador o función en una expresión. Para obtener ejemplos de expresiones más complejas, vea [Usar expresiones de propiedad en paquetes](use-property-expressions-in-packages.md).  
  
### <a name="to-create-or-change-a-property-expression"></a>Para agregar o cambiar una expresión de propiedad  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto que contiene el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo y siga uno de estos procedimientos:  
  
    -   Si el elemento es una tarea o un contenedor, haga doble clic en el elemento y, después, haga clic en **Expresiones** en el editor.  
  
    -   Haga clic con el botón derecho en el elemento y, después, haga clic en **Propiedades**.  
  
3.  Haga clic en el cuadro **Expresiones** y, después, en el botón de puntos suspensivos (…).  
  
4.  En el **Editor de expresiones de propiedad**, seleccione una propiedad de la lista **Propiedades** y siga uno de estos procedimientos:  
  
    -   Escriba o cambie directamente la expresión de propiedad en la columna **Expresión** y, a continuación, haga clic en **Aceptar**.  
  
         O bien  
  
    -   Haga clic en los puntos suspensivos (…) en la fila de expresión de la propiedad para abrir el **Generador de expresiones**.  
  
5.  (Opcional) En el **Generador de expresiones**, haga una de las tareas siguientes:  
  
    -   Para tener acceso a las variables del sistema y a las definidas por el usuario, expanda **Variables**.  
  
    -   Para tener acceso a las funciones, las conversiones y los operadores que proporciona el lenguaje de expresiones de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , expanda **Funciones matemáticas**, **Funciones de cadena**, **Funciones de fecha y hora**, **Funciones NULL**, **Conversiones de tipo**y **Operadores**.  
  
    -   Para generar o cambiar una expresión en el **Generador de expresiones**, arrastre variables, columnas, funciones, operadores y conversiones hasta el cuadro **Expresión** , o escriba la expresión en el cuadro.  
  
    -   Para ver el resultado de la evaluación de la expresión, haga clic en **Evaluar expresión** en el **Generador de expresiones**.  
  
         Si la expresión no es válida, aparece una alerta que describe los errores de sintaxis de la expresión.  
  
        > [!NOTE]  
        >  Evaluar una expresión no asigna el resultado de la evaluación a la propiedad.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Expresiones de Integration Services &#40;SSIS&#41;](integration-services-ssis-expressions.md)   
 [Usar expresiones de propiedad en paquetes](use-property-expressions-in-packages.md)   
 [Paquetes de Integration Services &#40;SSIS&#41;](../integration-services-ssis-packages.md)   
 [Contenedores de Integration Services](../control-flow/integration-services-containers.md)   
 [Tareas de Integration Services](../control-flow/integration-services-tasks.md)   
 [Controladores de eventos de Integration Services &#40;SSIS&#41;](../integration-services-ssis-event-handlers.md)   
 [Conexiones de Integration Services &#40;SSIS&#41;](../connection-manager/integration-services-ssis-connections.md)   
 [Registro de Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md)  
  
  
