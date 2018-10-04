---
title: Elemento PendingValue (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PendingValue Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PendingValue
helpviewer_keywords:
- PendingValue element
ms.assetid: 386b2ec6-3d83-42d2-b83a-83e375fbdcbd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0f78f1916f9d6b4cd266848d5b5c5943fb17cc9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117431"
---
# <a name="pendingvalue-element-assl"></a>Elemento PendingValue (ASSL)
  Contiene la lectura-valor pendiente de solo asociado [ServerProperty](../objects/serverproperty-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ServerProperty>  
   ...  
   <PendingValue>...</PendingValue>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cualquier simpleType|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ServerProperty](../objects/serverproperty-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 Este elemento contiene el valor de la `ServerProperty` que se usará la próxima vez que la instancia actual de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se inicia. Este valor se recupera normalmente de dondequiera que esté almacenado el valor para la propiedad del servidor: en un archivo de inicialización, el Registro de Windows [!INCLUDE[msCoName](../../../includes/msconame-md.md)] u otro mecanismo de almacenamiento.  
  
 El elemento que se corresponde con el elemento primario de `PendingValue` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ServerProperty>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento ServerProperties &#40;ASSL&#41;](../collections/serverproperties-element-assl.md)   
 [Elemento Server &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
