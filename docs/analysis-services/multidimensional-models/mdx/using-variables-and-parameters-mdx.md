---
title: "Usar Variables y parámetros (MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [MDX]
- queries [MDX], variables
- queries [MDX], parameters
- variables [MDX]
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5ac634400b85e49cdaf9f57e683cc13fe781ed2b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="using-variables-and-parameters-mdx"></a>Usar variables y parámetros (MDX)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]admite la parametrización de las instrucciones de expresiones multidimensionales (MDX). Las instrucciones con parámetros permiten crear instrucciones genéricas que pueden personalizarse en tiempo de ejecución.  
  
 Al crear una instrucción con parámetros se debe identificar el nombre del parámetro mediante un prefijo con el símbolo de arroba (@). Por ejemplo, @Year sería un nombre de parámetro válido  
  
 MDX solo admite parámetros para valores literales o escalares. Para crear un parámetro que haga referencia a un miembro, conjunto o tupla debería utilizar una función como [StrToMember](../../../mdx/strtomember-mdx.md) o [StrToSet](../../../mdx/strtoset-mdx.md).  
  
 En el siguiente código XML de ejemplo de Analysis (XMLA), el @CountryName parámetro contendrá el país para el cliente que se recuperan datos:  
  
```  
<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">  
  <Body>  
    <Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <Command>  
        <Statement>  
select [Measures].members on 0,   
       Filter(Customer.[Customer Geography].Country.members,   
              Customer.[Customer Geography].CurrentMember.Name =  
              @CountryName) on 1  
from [Adventure Works]  
</Statement>  
      </Command>  
      <Properties />  
      <Parameters>  
        <Parameter>  
          <Name>CountryName</Name>  
          <Value>'United Kingdom'</Value>  
        </Parameter>  
      </Parameters>  
    </Execute>  
  </Body>  
</Envelope>  
```  
  
 Para utilizar esta funcionalidad con OLE DB, debería usarse la interfaz **ICommandWithParameters** . Para utilizar esta funcionalidad con ADOMD.Net, debería usarse la colección **AdomdCommand.Parameters** .  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de scripting MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  

