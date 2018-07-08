---
title: Referencia a ensamblados en un archivo RDL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 29e2a4698ef09627b4098ab5e28ecbe096d6af30
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153976"
---
# <a name="referencing-assemblies-in-an-rdl-file"></a>Hacer referencia a ensamblados en un archivo RDL
  Para admitir el uso de ensamblados de código personalizados en archivos de definición de informe, se incluyen dos elementos del lenguaje RDL (Report Definition Language) en la especificación RDL: **CodeModules** y **Classes**.  
  
 El elemento **CodeModules** le permite hacer referencia a los ensamblados de código administrado en las expresiones de informe. **CodeModules** es un elemento de nivel superior que contiene la referencia al ensamblado que se utiliza en los archivos de definición de informe para llamar a las funciones especializadas. Una entrada en una definición de informe que admita el uso de un ensamblado personalizado podría parecerse a la siguiente:  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 En lugar de llamar a <xref:System.Reflection.Assembly.Load%2A> desde el código personalizado, registre los ensamblados personalizados agregando manualmente los elementos **CodeModule** al archivo RDL o usando la pestaña **Referencias** del cuadro de diálogo **Propiedades del informe**. Para obtener más información, vea [Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](../report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
 El elemento **Classes** admite el uso de miembros de instancia en una definición de informe. **Classes** es un elemento de nivel superior que contiene una referencia al nombre de clase y un nombre de instancia. La entrada de una definición de informe que admita el uso de miembros de instancia podría parecerse a la siguiente:  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 Para más información, vea [Acceso a los ensamblados personalizados a través de expresiones](accessing-custom-assemblies-through-expressions.md).  
  
## <a name="see-also"></a>Vea también  
 [Usar ensamblados personalizados con informes](using-custom-assemblies-with-reports.md)  
  
  
