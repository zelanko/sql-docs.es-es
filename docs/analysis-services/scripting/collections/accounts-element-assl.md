---
title: Cuentas de elemento (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Accounts Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Accounts
helpviewer_keywords:
- Accounts element
ms.assetid: 3ec62f58-c19b-4b15-b040-8941521a389b
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3d781e32f57f9df9cc5bf180e37761c8a26c0848
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="accounts-element-assl"></a>Elemento Accounts (ASSL)
  Contiene la colección de tipos de cuenta que se definen en un [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno (colección)|  
|Valor predeterminado|Ninguno (colección)|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Base de datos](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|Elementos secundarios|[Cuenta](../../../analysis-services/scripting/objects/account-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Dimensiones, cuyo [tipo](../../../analysis-services/scripting/properties/type-element-dimension-assl.md) elemento está establecido en *cuentas*, puede tener un atributo que especifica el tipo de cuenta, como Income, Expense etc., representado por miembros de la dimensión. El tipo de cuenta, a continuación, se usa por [medida](../../../analysis-services/scripting/objects/measure-element-assl.md) elementos, cuyo [AggregationFunction](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md) elemento está establecido en *ByAccount*, para determinar la función de agregación que se utiliza al Agregar a los miembros de esa dimensión. El elemento **Accounts** contiene una colección de elementos **Account** que representan los tipos de cuenta y la función de agregación que se deberían utilizar para cada tipo de cuenta.  
  
 Un tipo de cuenta debe aparecer si la función de agregado es diferente del valor predeterminado utilizado por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para cada tipo de cuenta.  
  
 El conjunto de tipos de cuentas válidos es fijo.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.AccountCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento AccountType &#40; ASSL &#41;](../../../analysis-services/scripting/properties/accounttype-element-assl.md)   
 [Colecciones de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  

