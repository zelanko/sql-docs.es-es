---
title: Origen de elemento (ComAssembly) (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Source Element (ComAssembly)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Source
helpviewer_keywords: Source element
ms.assetid: 5c9209e8-ace6-4688-a64d-4987a7648ab9
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f9982e379b56374da92a5b672da24e591603a0a9
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="source-element-comassembly-assl"></a>Elemento Source (ComAssembly) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contiene el nombre de archivo o el identificador de programación (ProgID) para un componente del modelo de objetos componentes (COM).  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ComAssembly>  
   ...  
   <Source>...</Source>  
   ...  
</ComAssembly>  
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
|Elemento primario|[ComAssembly](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que corresponde al elemento primario de **origen** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ComAssembly>.  
  
## <a name="see-also"></a>Vea también  
 [Assembly (elemento) &#40; ASSL &#41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [Tipo de datos ClrAssembly &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [Assemblies, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [Elemento de la base de datos &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Elemento Server &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
