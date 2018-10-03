---
title: Elemento Version (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Version Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Version
helpviewer_keywords:
- Version element
ms.assetid: fb26fe5d-de40-443b-a8bc-031c950552e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e8c8cde757b0de5fb4076c395ac915650a12d4a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091315"
---
# <a name="version-element-assl"></a>Elemento Version (ASSL)
  Contiene el número de versión de solo lectura de la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] representado por la [Server](../objects/server-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Server>  
      ...  
      <Version>...</Version>  
   ...  
</Server>  
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
|Elemento primario|[Server](../objects/server-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento `Version` describe qué versión de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] está instalada.  
  
 El elemento que se corresponde con el elemento primario de `Version` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Server>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Edition &#40;ASSL&#41;](edition-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
