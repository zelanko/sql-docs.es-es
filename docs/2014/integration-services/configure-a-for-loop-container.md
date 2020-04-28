---
title: Configurar un contenedor de bucles for | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: b9cd7ea7-b198-4a35-8b16-6acf09611ca5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 766a82c975b607687f79a696ce587422b93322bf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81487003"
---
# <a name="configure-a-for-loop-container"></a>Configurar un contenedor de bucles For
  En este procedimiento se describe cómo configurar un contenedor de bucles For mediante el cuadro de diálogo **Editor de bucles For** .  
  
### <a name="to-configure-the-for-loop-container"></a>Para configurar el contenedor de bucles For  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga doble clic en el contenedor de bucles For para abrir el **Editor de bucles For**.  
  
2.  Opcionalmente, modifique el nombre y la descripción del contenedor de bucles For.  
  
3.  También puede escribir una expresión de inicialización en el cuadro de texto **InitExpression** .  
  
4.  Escriba una expresión de evaluación en el cuadro de texto **EvalExpression** .  
  
    > [!NOTE]  
    >  La expresión debe evaluarse como un valor booleano. Cuando la expresión se evalúa como `false`, el bucle deja de ejecutarse.  
  
5.  Opcionalmente, escriba una expresión de asignación en el cuadro de texto **AssignExpression** .  
  
6.  También puede hacer clic en **Expresiones** y, en la página **Expresiones** , crear expresiones de propiedades para las propiedades del contenedor de bucles For. Para más información, vea [Agregar o cambiar una expresión de propiedad](expressions/add-or-change-a-property-expression.md).  
  
7.  Haga clic en **Aceptar** para cerrar el **Editor de bucles For**.  
  
## <a name="see-also"></a>Consulte también  
 [Contenedor de bucles for](control-flow/for-loop-container.md)   
 [Integration Services &#40;expresiones de&#41; SSIS](expressions/integration-services-ssis-expressions.md)   
 [Usar expresiones de propiedad en paquetes](expressions/use-property-expressions-in-packages.md)  
  
  
