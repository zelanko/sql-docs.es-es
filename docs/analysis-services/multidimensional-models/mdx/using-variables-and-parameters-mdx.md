---
title: Usar Variables y parámetros (MDX) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: deb1f7b4e641dd2347e8629e1e13ad3f4da7788c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="using-variables-and-parameters-mdx"></a>Usar variables y parámetros (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite la parametrización de las instrucciones de expresiones multidimensionales (MDX). Las instrucciones con parámetros permiten crear instrucciones genéricas que pueden personalizarse en tiempo de ejecución.  
  
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
 [Aspectos básicos de Scripting de MDX & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  
