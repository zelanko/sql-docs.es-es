---
title: Elemento StorageLocation (ASSL) | Documentos de Microsoft
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
- StorageLocation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- StorageLocation
helpviewer_keywords:
- StorageLocation element
ms.assetid: ecf8852f-56a1-4fcf-b0d8-d7eebb75e4ed
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b6f6d023731126cafaa76cf31598e0bae9fdf1cf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104781"
---
# <a name="storagelocation-element-assl"></a>Elemento StorageLocation (ASSL)
  Contiene la ubicación del sistema de almacenamiento de archivos para el contenido del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Cube><!-- or MeasureGroup, Partition -->  
      ...  
   <StorageLocation>...</StorageLocation>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
|Antecesor o elemento primario|Valor predeterminado|  
|------------------------|-------------------|  
|[Cubo](../objects/cube-element-assl.md)|None|  
|[MeasureGroup](../objects/group-element-assl.md)|Valor de `StorageLocation` del elemento primario `Cube`.|  
|[Partición](../objects/partition-element-assl.md)|Valor de `StorageLocation` del elemento primario `MeasureGroup`.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cubo](../objects/cube-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [partición](../objects/partition-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Los elementos que corresponden a los elementos primarios de `StorageLocation` en el modelo de objetos de Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.MeasureGroup> y <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  