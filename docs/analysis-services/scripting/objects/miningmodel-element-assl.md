---
title: Elemento MiningModel (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MiningModel Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MiningModel
helpviewer_keywords:
- MiningModel element
ms.assetid: a61d935f-c8f6-457d-ad0c-44f58bb286f5
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 691e74eb05498dd0e6a47c5d2bd602d06d299d5f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="miningmodel-element-assl"></a>Elemento MiningModel (ASSL)
  Define un único modelo de minería de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningModels>  
      <MiningModel>  
      <Name>...</Name>  
            <ID>...</ID>  
      <Description>...</<Descrip  
            <Algorithm>...</Algorithm>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastProcessed>...</LastProcessed>  
      <AlgorithmParameters>...</AlgorithmParameters>  
      <AllowDrillThrough>...</AllowDrillThrough>  
      <Translations>...</Translations>  
      <Columns>...</Columns>  
      <State>...</State>  
      <MiningModelPermissions>...</MiningModelPermissions>  
      <Language>...</Language>  
            <Collation>...</Collation>  
            <Annotations>...</Annotations>  
            <ddl100_100:FoldingParameters>   </FoldingParameters>  
   </MiningModel>  
</MiningModels>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[MiningModels](../../../analysis-services/scripting/collections/miningmodels-element-assl.md)|  
|Elementos secundarios|[Algoritmo](../../../analysis-services/scripting/properties/algorithm-element-assl.md), [AlgorithmParameters](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md), [AllowDrillThrough](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md), [anotaciones](../../../analysis-services/scripting/collections/annotations-element-assl.md), [intercalación](../../../analysis-services/scripting/properties/collation-element-assl.md), [Columnas](../../../analysis-services/scripting/collections/columns-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [descripción](../../../analysis-services/scripting/properties/description-element-assl.md), [identificador](../../../analysis-services/scripting/properties/id-element-assl.md), [lenguaje](../../../analysis-services/scripting/properties/language-element-assl.md), [ LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [MiningModelPermissions](../../../analysis-services/scripting/collections/miningmodelpermissions-element-assl.md), [nombre](../../../analysis-services/scripting/properties/name-element-assl.md), [estado](../../../analysis-services/scripting/properties/state-element-assl.md), [ Traducciones](../../../analysis-services/scripting/collections/translations-element-assl.md),<br /><br /> [FoldingParameters](../../../analysis-services/scripting/properties/foldingparameters-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento **FoldingParameters** del modelo de minería de datos es para el uso interno del servidor y no se puede usar en las instrucciones DDL.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MiningModel>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

