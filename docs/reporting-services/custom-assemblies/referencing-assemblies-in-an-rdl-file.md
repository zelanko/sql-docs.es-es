---
title: Referencia a ensamblados en un archivo RDL | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 87285bffd5136c4ac2a66ae17755edcecd35f065
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "63193974"
---
# <a name="referencing-assemblies-in-an-rdl-file"></a>Hacer referencia a ensamblados en un archivo RDL
  Para admitir el uso de ensamblados de código personalizados en archivos de definición de informe, se incluyen dos elementos del lenguaje RDL (Report Definition Language) en la especificación RDL: **CodeModules** y **Classes**.  
  
 El elemento **CodeModules** le permite hacer referencia a los ensamblados de código administrado en las expresiones de informe. **CodeModules** es un elemento de nivel superior que contiene la referencia al ensamblado que se utiliza en los archivos de definición de informe para llamar a las funciones especializadas. Una entrada en una definición de informe que admita el uso de un ensamblado personalizado podría parecerse a la siguiente:  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 En lugar de llamar a <xref:System.Reflection.Assembly.Load%2A> desde el código personalizado, registre los ensamblados personalizados agregando manualmente los elementos **CodeModule** al archivo RDL o usando la pestaña **Referencias** del cuadro de diálogo **Propiedades del informe**. Para obtener más información, vea [Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)subyacente.  
  
 El elemento **Classes** admite el uso de miembros de instancia en una definición de informe. **Classes** es un elemento de nivel superior que contiene una referencia al nombre de clase y un nombre de instancia. La entrada de una definición de informe que admita el uso de miembros de instancia podría parecerse a la siguiente:  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 Para más información, vea [Acceso a los ensamblados personalizados a través de expresiones](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md).  
  
## <a name="see-also"></a>Consulte también  
 [Uso de ensamblados personalizados con informes](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
