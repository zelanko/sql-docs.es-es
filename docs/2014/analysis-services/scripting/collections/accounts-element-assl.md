---
title: Cuentas de elemento (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Accounts Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Accounts
helpviewer_keywords:
- Accounts element
ms.assetid: 3ec62f58-c19b-4b15-b040-8941521a389b
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 30fcd1815ac785ab71c90a935b9392ab5e85e98b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103183"
---
# <a name="accounts-element-assl"></a>Elemento Accounts (ASSL)
  Contiene la colección de tipos de cuenta que se definen en un [base de datos](../objects/database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Database>  
   ...  
   <Accounts>  
      <Account>...</Account>  
   </Accounts>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno (colección)|  
|Valor predeterminado|Ninguno (colección)|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Base de datos](../objects/database-element-assl.md)|  
|Elementos secundarios|[Cuenta](../objects/account-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 Dimensiones, cuyo [tipo](../properties/type-element-dimension-assl.md) elemento está establecido en *cuentas*, puede tener un atributo que especifica el tipo de cuenta, como Income, Expense etc., representado por miembros de la dimensión. El tipo de cuenta, a continuación, se usa por [medida](../objects/measure-element-assl.md) elementos, cuyo [AggregationFunction](../properties/aggregatefunction-element-assl.md) elemento está establecido en *ByAccount*, para determinar la función de agregación que se utiliza al Agregar a los miembros de esa dimensión. El elemento `Accounts` contiene una colección de elementos `Account` que representan los tipos de cuenta y la función de agregación que se deberían utilizar para cada tipo de cuenta.  
  
 Un tipo de cuenta debe aparecer si la función de agregado es diferente del valor predeterminado utilizado por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para cada tipo de cuenta.  
  
 El conjunto de tipos de cuentas válidos es fijo.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.AccountCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento AccountType &#40;ASSL&#41;](../properties/accounttype-element-assl.md)   
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  