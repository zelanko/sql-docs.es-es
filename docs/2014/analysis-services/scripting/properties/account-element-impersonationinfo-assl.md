---
title: Cuenta de elemento (ImpersonationInfo) (ASSL) | Documentos de Microsoft
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
- Account Element (ImpersonationInfo)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Account element
ms.assetid: aa3a1281-e42a-4926-875b-e6b81f4599c3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 454e46b3515ebd6b5ad8e8193edbc2a9aea14562
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108429"
---
# <a name="account-element-impersonationinfo-assl"></a>Elemento Account (ImpersonationInfo) (ASSL)
  Contiene el nombre de la cuenta de usuario para la [ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md) tipo de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Account>...</Account>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de la `Account` elemento, así como el valor de la [contraseña](password-element-assl.md) , se utiliza por motivos de suplantación si el valor de la [ImpersonationMode](impersonationmode-element-assl.md) (elemento) para cualquier elemento derivado de la `ImpersonationInfo` tipo de datos está establecido en *ImpersonateAccount*.  
  
## <a name="see-also"></a>Vea también  
 [Elemento DataSourceImpersonationInfo &#40;ASSL&#41;](impersonationinfo-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  