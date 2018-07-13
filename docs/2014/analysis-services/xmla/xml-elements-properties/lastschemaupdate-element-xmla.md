---
title: Elemento LastSchemaUpdate (XMLA) | Microsoft Docs
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
- LastSchemaUpdate Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#LastSchemaUpdate
- urn:schemas-microsoft-com:xml-analysis#LastSchemaUpdate
- microsoft.xml.analysis.lastschemaupdate
helpviewer_keywords:
- LastSchemaUpdate element
ms.assetid: 2109955c-2817-413e-93aa-95d9910e8b24
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ebdd4048e8e22aee422f3bee315776dbaed66873
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37152736"
---
# <a name="lastschemaupdate-element-xmla"></a>Elemento LastSchemaUpdate (XMLA)
  Contiene la fecha y hora en que se actualizaron por última vez los metadatos del cubo representados por el elemento primario [Cube](cube-element-olapinfo-xmla.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Cube>  
   ...  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|dateTime|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cubo](cube-element-olapinfo-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
