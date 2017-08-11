---
title: "Agregar una expresión (generador de informes y SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a60ee091-b4ed-41e1-9b6a-032c316cd03f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 57cdb0a373d713741216b1cebc8d3d44ff7fceb3
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="add-an-expression-report-builder-and-ssrs"></a>Agregar una expresión (Generador de informes y SSRS)
  Las expresiones se usan en los informes para definir propiedades de elementos de informe, filtros, grupos, criterios de ordenación, cadenas de conexión y valores de parámetros. Las expresiones comienzan por un signo igual (=) y se escriben en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. El procesador de informes, que combina el resultado de la evaluación con elementos de diseño de informe, evalúa las expresiones en tiempo de ejecución.  
  
 Las expresiones pueden ser simples o complejas. Una expresión simple hace referencia a un único elemento de una colección integrada. Las expresiones complejas pueden contener constantes, operadores, elementos de recopilación globales y llamadas a funciones. Para obtener más información, vea [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-expression-to-a-text-box"></a>Para agregar una expresión a un cuadro de texto  
  
-   En la vista **Diseño** , haga clic en el cuadro de texto de la superficie de diseño al que desea agregar una expresión.  
  
    -   Si se trata de una expresión simple, escriba el texto para mostrar de la expresión en el cuadro de texto. Por ejemplo, para el campo de conjunto de datos Sales, escriba `[Sales]`.  
  
    -   Si se trata de una expresión compleja, haga clic con el botón derecho en el cuadro de texto y seleccione **Expresión**. Se abre el cuadro de diálogo **Expresión** . Escriba o cree de forma interactiva la expresión después del signo '=' en el panel de expresión y, a continuación, haga clic en Aceptar.  
  
         La expresión aparece en la superficie de diseño como `<<Expr>>`.  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a texto y marcadores de posición &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Cuadros de texto &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [Usar expresiones en informes &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de ecuaciones de filtro &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones de grupo &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [Cuadro de diálogo Expresión &#40; El generador de informes &#41;](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)   
 [Ejemplos de expresiones &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Agregar código a un informe &#40; SSRS &#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md)  
  
  
