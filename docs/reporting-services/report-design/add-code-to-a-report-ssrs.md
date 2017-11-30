---
title: "Agregar código a un informe (SSRS) | Microsoft Docs"
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
helpviewer_keywords:
- code [Reporting Services]
- custom code [Reporting Services]
- expressions [Reporting Services], code
- adding code
- reports [Reporting Services], code
ms.assetid: 00ef8fc6-99fe-49b2-8a22-7eb475881dc4
caps.latest.revision: "41"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: dad6a1b0a3be940cd3f0d6ecf9a5e62193ee9960
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="add-code-to-a-report-ssrs"></a>Agregar código a un informe (SSRS)
  Si lo desea, puede llamar a su propio código personalizado en cualquier expresión. Puede proporcionar el código de estas dos formas:  
  
-   Incrustando el código escrito en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] directamente en el informe. Si el código hace referencia a un ensamblado de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que no es <xref:System.Math> ni <xref:System.Convert>, debe agregar la referencia al informe. Para más información, vea [Agregar una referencia de ensamblado a un informe &#40;SSRS&#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md). Para más información sobre otras referencias que puede usar desde el código, vea [Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
-   Proporcionando un ensamblado de código personalizado usando [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Si proporciona un ensamblado personalizado, debe instalarlo tanto en el equipo donde crea el informe como en el servidor de informes donde ve el informe. Para más información, consulte [Using Custom Assemblies with Reports](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md).  
  
### <a name="to-add-embedded-code-to-a-report"></a>Para agregar código incrustado a un informe  
  
1.  En la vista **Diseño** , haga clic con el botón derecho en la superficie de diseño fuera del borde del informe y, después, haga clic en **Propiedades del informe**.  
  
2.  Haga clic en **Código**.  
  
3.  En **Código personalizado**, escriba el código. Los errores en el código generan advertencias al ejecutar el informe. En el ejemplo siguiente se crea una función personalizada denominada `ChangeWord` que reemplaza la palabra "`Bike`" por "`Bicycle`".  
  
    ```  
    Public Function ChangeWord(ByVal s As String) As String  
       Dim strBuilder As New System.Text.StringBuilder(s)  
       If s.Contains("Bike") Then  
          strBuilder.Replace("Bike", "Bicycle")  
          Return strBuilder.ToString()  
          Else : Return s  
       End If  
    End Function  
    ```  
  
4.  En el ejemplo siguiente se muestra cómo pasar un campo de conjunto de datos denominado Category a esta función en una expresión:  
  
    ```  
    =Code.ChangeWord(Fields!Category.Value)  
    ```  
  
     Si agrega esta expresión a una celda de tabla que muestre valores de categoría, cada vez que la palabra "Bike" aparezca en el campo de conjunto de datos para esa fila, el valor de la celda de tabla muestra en su lugar la palabra "Bicycle".  
  
## <a name="see-also"></a>Vea también  
 [Propiedades del informe (cuadro de diálogo), Código](http://msdn.microsoft.com/library/955d4b11-17b4-4f1c-9690-6e7af54caea7)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Usar referencias a la colección de parámetros &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
