---
title: Elemento ImpersonationMode (ASSL) | Microsoft Docs
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
- ImpersonationMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ImpersonateMode
helpviewer_keywords:
- ImpersonateMode element
ms.assetid: 160fdcb2-ac9f-4c5a-a0eb-a5f7669166b9
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dad131322f27cee48fa2fe1dd1ed593477afbe42
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37216235"
---
# <a name="impersonationmode-element-assl"></a>Elemento ImpersonationMode (ASSL)
  Contiene un valor que indica el método de suplantación para los elementos que se derivan de la [ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md) tipo de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ImpersonationInfo>  
   ...  
   <ImpersonationMode>...</ImpersonationMode>  
  
</ImpersonationInfo>...  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Valor de DB-Library*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Valor de DB-Library*|El elemento primario usa el método de suplantación más adecuado para el contexto en el que se usa la suplantación.|  
|*ImpersonateAccount*|El elemento primario usa las credenciales de la cuenta de usuario que se especifica en el elemento primario.|  
|*ImpersonateAnonymous*|El elemento primario usa las credenciales de un usuario anónimo.|  
|*ImpersonateCurrentUser*|El elemento primario usa las credenciales del usuario actual.|  
|*ImpersonateServiceAccount*|El elemento primario usa las credenciales de la cuenta de servicio que está asociado a la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
  
 La enumeración que corresponde a los valores permitidos para `ImpersonationMode` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ImpersonationLevel>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
