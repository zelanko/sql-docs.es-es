---
title: Elemento Locations (XMLA) | Microsoft Docs
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
- Locations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Locations
- urn:schemas-microsoft-com:xml-analysis#Locations
- microsoft.xml.analysis.locations
helpviewer_keywords:
- Locations element
ms.assetid: 630929cb-f0dc-472a-86bc-28b67e907c3d
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 901c2d1cccacef54462d5f8cf9df4a4c59907a11
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263321"
---
# <a name="locations-element-xmla"></a>Elemento Locations (XMLA)
  Contiene una colección de elementos [Location](query-element-xmla.md) que utiliza el comando primario [Backup](../xml-elements-commands/backup-element-xmla.md), [Restore](../xml-elements-commands/restore-element-xmla.md) o [Synchronize](../xml-elements-commands/synchronize-element-xmla.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
< Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Locations>  
      <Location>...</Location>  
   </Locations>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Backup](../xml-elements-commands/backup-element-xmla.md), [Restore](../xml-elements-commands/restore-element-xmla.md) o [Synchronize](../xml-elements-commands/synchronize-element-xmla.md)|  
|Elementos secundarios|[Ubicación](location-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
