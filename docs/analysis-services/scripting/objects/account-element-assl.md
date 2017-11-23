---
title: Cuenta de elemento (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Account Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Account
helpviewer_keywords: Account element
ms.assetid: 0bb7d06c-0158-4ab2-b2b1-cb50ba24f7c0
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: efe72ade8623910c34a1aff1d5439ee707c27f7b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="account-element-assl"></a>Elemento Account (ASSL)
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
 [Elemento de la base de datos &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
