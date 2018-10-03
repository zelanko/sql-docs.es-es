---
title: Página Expresiones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.expressionspage.f1
helpviewer_keywords:
- Expressions Page dialog box
ms.assetid: c9016ec6-11c1-4ebd-b2a7-0fa6631fd9e4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: eb12bb684753a5d965054e361f8b0b23ebf7802d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48150475"
---
# <a name="expressions-page"></a>Página Expresiones
  Utilice la página **Expresiones** para editar expresiones de propiedad y obtener acceso a los cuadros de diálogo **Editor de expresiones de propiedad** y **Generador de expresiones** .  
  
 Las expresiones de propiedad actualizan los valores de las propiedades cuando se ejecuta el paquete. Se pueden utilizar expresiones de propiedad con las propiedades de paquetes, tareas, contenedores, administradores de conexión y algunos componentes de flujo de datos. Las expresiones se evalúan y se usan los resultados en lugar de los valores en los que se han establecido las propiedades al configurar el paquete y los objetos de paquete. Las expresiones pueden incluir variables y las funciones y los operadores que proporciona el lenguaje de expresiones. Por ejemplo, se puede generar la línea de asunto de la tarea Enviar correo mediante la concatenación del valor de una variable que contenga la cadena "Pronóstico meteorológico para" y los resultados devueltos de la función GETDATE() para crear la cadena "Pronóstico meteorológico para 5/4/2006".  
  
 Para obtener más información sobre cómo se escriben las expresiones y cómo se usan las expresiones de propiedad, vea [Integration Services &#40;SSIS&#41; Expressions](integration-services-ssis-expressions.md) y [Usar expresiones de propiedad en paquetes](use-property-expressions-in-packages.md).  
  
## <a name="options"></a>Opciones  
 **Expresiones (...)**  
 Haga clic en los puntos suspensivos para abrir el cuadro de diálogo **Editor de expresiones de propiedad** . Para más información, consulte [Property Expressions Editor](property-expressions-editor.md).  
  
 **\<property name>**  
 Haga clic en los puntos suspensivos para abrir el cuadro de diálogo **Generador de expresiones** . Para más información, consulte [Expression Builder](expression-builder.md).  
  
## <a name="see-also"></a>Vea también  
 [Servicios de integración &#40;SSIS&#41; Variables](../integration-services-ssis-variables.md)   
 [Variables del sistema](../system-variables.md)   
 [Expresiones de Integration Services &#40;SSIS&#41;](integration-services-ssis-expressions.md)  
  
  
