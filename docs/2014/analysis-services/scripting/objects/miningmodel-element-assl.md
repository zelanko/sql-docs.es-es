---
title: Elemento MiningModel (ASSL) | Microsoft Docs
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
- MiningModel Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModel
helpviewer_keywords:
- MiningModel element
ms.assetid: a61d935f-c8f6-457d-ad0c-44f58bb286f5
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7ba98443b953f4107b209dd06af74349a81bb2a3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37224545"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[MiningModels](../collections/miningmodels-element-assl.md)|  
|Elementos secundarios|[Algoritmo](../properties/algorithm-element-assl.md), [AlgorithmParameters](algorithmparameter-element-assl.md), [AllowDrillThrough](../properties/allowdrillthrough-element-assl.md), [anotaciones](../collections/annotations-element-assl.md), [intercalación](../properties/collation-element-assl.md), [ Columnas](../collections/columns-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [descripción](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md), [lenguaje](../properties/language-element-assl.md), [ LastProcessed](../properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [MiningModelPermissions](../collections/miningmodelpermissions-element-assl.md), [nombre](../properties/name-element-assl.md), [estado](../properties/state-element-assl.md), [ Traducciones](../collections/translations-element-assl.md),<br /><br /> [FoldingParameters](../properties/foldingparameters-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento `FoldingParameters` del modelo de minería de datos es para el uso interno del servidor y no se puede usar en las instrucciones DDL.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MiningModel>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
