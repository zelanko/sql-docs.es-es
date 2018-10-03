---
title: Elemento AllowedSet (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AllowedSet Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AllowedSet
helpviewer_keywords:
- AllowedSet element
ms.assetid: 4aff2e03-6e1f-4f1a-b99d-d86bba25ab9b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f011b6a3f07d71c653bd8fcb358bffb995f4bc14
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169635"
---
# <a name="allowedset-element-assl"></a>Elemento AllowedSet (ASSL)
  Contiene una expresión de conjunto que define el conjunto de permisos concedidos para un [rol](../objects/role-element-assl.md) elemento en un atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributePermission>  
      ...  
   <AllowedSet>...</AllowedSet>  
   ...  
</AttributePermission>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[AttributePermission](../objects/attributepermission-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que se corresponde con el elemento primario de `AllowedSet` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.AttributePermission>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
