---
title: Elemento (ASSL) de la cuenta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Account Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Account
helpviewer_keywords:
- Account element
ms.assetid: 0bb7d06c-0158-4ab2-b2b1-cb50ba24f7c0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 262ba3be01879770a734ab7334782e26aa04b364
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48109055"
---
# <a name="account-element-assl"></a>Elemento Account (ASSL)
  Contiene información detallada sobre un tipo de cuenta dentro de un [base de datos](database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Accounts>  
   <Account>  
      <AccountType>...</AccountType>  
      <AggregationFunction>...</AggregationFunction>  
            <Aliases>...</Aliases>  
            <Annotations>...</Annotations>  
   </Account>  
</Accounts>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cuentas](../collections/accounts-element-assl.md)|  
|Elementos secundarios|[AccountType](../properties/accounttype-element-assl.md), [AggregationFunction](../properties/aggregationfunction-element-assl.md), [alias](../collections/aliases-element-assl.md), [anotaciones](../collections/annotations-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Las dimensiones, cuyo [tipo](../properties/type-element-dimension-assl.md) elemento está establecido en *cuentas,* puede tener un atributo que especifica el tipo de cuenta, como Income, Expense, etc., representado por miembros de la dimensión. El tipo de cuenta, a continuación, se usa por [medida](measure-element-assl.md) elementos, cuyo [AggregationFunction](../properties/aggregatefunction-element-assl.md) elemento está establecido en *ByAccount*, para determinar la función de agregación que se utiliza al Agregar a los miembros de esa dimensión. El elemento `Account` representa un tipo de cuenta único y la función de agregado que tales medidas deben utilizar.  
  
 Un tipo de cuenta debe aparecer si la función de agregado es diferente del valor predeterminado utilizado por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para cada tipo de cuenta.  
  
 El conjunto de tipos de cuentas válidos es fijo.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Account>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de la base de datos &#40;ASSL&#41;](database-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
