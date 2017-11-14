---
title: Cuenta de elemento (ImpersonationInfo) (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
apiname:
- Account Element (ImpersonationInfo)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Account element
ms.assetid: aa3a1281-e42a-4926-875b-e6b81f4599c3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e99a3e4bd81c70fd1043465f59f76b2fab60e863
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="account-element-impersonationinfo-assl"></a>Elemento Account (ImpersonationInfo) (ASSL)
  Contiene el nombre de la cuenta de usuario para la [ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md) tipo de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Account>...</Account>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de la **cuenta** elemento, así como el valor de la [contraseña](../../../analysis-services/scripting/properties/password-element-assl.md) , se utiliza por motivos de suplantación si el valor de la [ImpersonationMode](../../../analysis-services/scripting/properties/impersonationmode-element-assl.md) (elemento) para cualquier elemento derivado de la **ImpersonationInfo** tipo de datos está establecido en *ImpersonateAccount*.  
  
## <a name="see-also"></a>Vea también  
 [Datasourceimpersonationinfo, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/properties/datasourceimpersonationinfo-element-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

