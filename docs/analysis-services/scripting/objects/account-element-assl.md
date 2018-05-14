---
title: Cuenta de elemento (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0e9cda9f82df4f1b7a6d445d7cb85e69c635833f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="account-element-assl"></a>Elemento Account (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contiene información detallada sobre un tipo de cuenta dentro de un [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
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
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cuentas](../../../analysis-services/scripting/collections/accounts-element-assl.md)|  
|Elementos secundarios|[AccountType](../../../analysis-services/scripting/properties/accounttype-element-assl.md), [AggregationFunction](../../../analysis-services/scripting/properties/aggregationfunction-element-assl.md), [alias](../../../analysis-services/scripting/collections/aliases-element-assl.md), [anotaciones](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Dimensiones, cuyo [tipo](../../../analysis-services/scripting/properties/type-element-dimension-assl.md) elemento está establecido en *cuentas,* puede tener un atributo que especifica el tipo de cuenta, como Income, Expense, etc., representado por miembros de la dimensión. El tipo de cuenta, a continuación, se usa por [medida](../../../analysis-services/scripting/objects/measure-element-assl.md) elementos, cuyo [AggregationFunction](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md) elemento está establecido en *ByAccount*, para determinar la función de agregación que se utiliza al Agregar a los miembros de esa dimensión. El elemento **Account** representa un tipo de cuenta único y la función de agregado que tales medidas deben utilizar.  
  
 Un tipo de cuenta debe aparecer si la función de agregado es diferente del valor predeterminado utilizado por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para cada tipo de cuenta.  
  
 El conjunto de tipos de cuentas válidos es fijo.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Account>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de la base de datos &#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
