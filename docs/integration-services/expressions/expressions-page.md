---
title: Página Expresiones | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.expressionspage.f1
helpviewer_keywords:
- Expressions Page dialog box
ms.assetid: c9016ec6-11c1-4ebd-b2a7-0fa6631fd9e4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1fe673f96f3272c2f23005588f0ad49271e943fe
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917048"
---
# <a name="expressions-page"></a>Página Expresiones

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Utilice la página **Expresiones** para editar expresiones de propiedad y obtener acceso a los cuadros de diálogo **Editor de expresiones de propiedad** y **Generador de expresiones** .  
  
 Las expresiones de propiedad actualizan los valores de las propiedades cuando se ejecuta el paquete. Se pueden utilizar expresiones de propiedad con las propiedades de paquetes, tareas, contenedores, administradores de conexión y algunos componentes de flujo de datos. Las expresiones se evalúan y se usan los resultados en lugar de los valores en los que se han establecido las propiedades al configurar el paquete y los objetos de paquete. Las expresiones pueden incluir variables y las funciones y los operadores que proporciona el lenguaje de expresiones. Por ejemplo, se puede generar la línea de asunto de la tarea Enviar correo mediante la concatenación del valor de una variable que contenga la cadena "Pronóstico meteorológico para" y los resultados devueltos de la función GETDATE() para crear la cadena "Pronóstico meteorológico para 5/4/2006".  
  
 Para obtener más información sobre cómo se escriben las expresiones y cómo se usan las expresiones de propiedad, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md) y [Usar expresiones de propiedad en paquetes](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
## <a name="options"></a>Opciones  
 **Expresiones (…)**  
 Haga clic en los puntos suspensivos para abrir el cuadro de diálogo **Editor de expresiones de propiedad** . Para más información, consulte [Property Expressions Editor](../../integration-services/expressions/property-expressions-editor.md).  
  
 **\<property name>**  
 Haga clic en los puntos suspensivos para abrir el cuadro de diálogo **Generador de expresiones** . Para más información, consulte [Expression Builder](../../integration-services/expressions/expression-builder.md).  
  
## <a name="see-also"></a>Consulte también  
 [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Variables del sistema](../../integration-services/system-variables.md)   
 [Expresiones de Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
