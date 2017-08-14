---
title: Hacer referencia a ensamblados en un archivo RDL | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 9fd80c818f13972434b72a72ce306e2f494cf56f
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="referencing-assemblies-in-an-rdl-file"></a>Hacer referencia a ensamblados en un archivo RDL
  Para admitir el uso de ensamblados de código personalizados en archivos de definición de informe, los dos elementos de lenguaje RDL (Report Definition) se incluyen en la especificación RDL: el **CodeModules** elemento y el **clases** elemento.  
  
 El **CodeModules** elemento le permite hacer referencia a los ensamblados de código administrado en las expresiones de informe. **CodeModules** es un elemento de nivel superior que contiene la referencia al ensamblado que se utiliza en los archivos de definición de informe para llamar funciones especializadas. Una entrada en una definición de informe que admita el uso de un ensamblado personalizado podría parecerse a la siguiente:  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 En lugar de llamar <xref:System.Reflection.Assembly.Load%2A> desde el código personalizado, registre los ensamblados personalizados agregando manualmente **CodeModule** elementos al archivo RDL o utilizando el **referencias** pestaña de la **propiedades del informe** cuadro de diálogo. Para más información, vea [Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
 El **clases** elemento admite el uso de miembros de instancia en una definición de informe. **Clases de** es un elemento de nivel superior que contiene una referencia al nombre de la clase y un nombre de instancia. La entrada de una definición de informe que admita el uso de miembros de instancia podría parecerse a la siguiente:  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 Para obtener más información, consulte [acceso a Custom Assemblies Through Expressions](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md).  
  
## <a name="see-also"></a>Vea también  
 [Usar ensamblados personalizados con informes](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
