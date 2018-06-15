---
title: Elemento StorageLocation (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 838bfa755a028b5f9a42091b7f33057bddb40204
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34042579"
---
# <a name="storagelocation-element-assl"></a>Elemento StorageLocation (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contiene la ubicación del sistema de almacenamiento de archivos para el contenido del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Cube><!-- or MeasureGroup, Partition -->  
      ...  
   <StorageLocation>...</StorageLocation>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Vea la tabla siguiente.|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
|Antecesor o elemento primario|Valor predeterminado|  
|------------------------|-------------------|  
|[Cubo](../../../analysis-services/scripting/objects/cube-element-assl.md)|Ninguno|  
|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|Valor de **StorageLocation** del elemento primario **Cube** .|  
|[Partición](../../../analysis-services/scripting/objects/partition-element-assl.md)|Valor de **StorageLocation** del elemento primario **MeasureGroup** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [Partition](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Los elementos que corresponden a los elementos primarios de **StorageLocation** en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.MeasureGroup>, y <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
