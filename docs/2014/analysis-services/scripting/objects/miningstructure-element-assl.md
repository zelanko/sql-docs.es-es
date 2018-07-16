---
title: Elemento MiningStructure (ASSL) | Microsoft Docs
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
- MiningStructure Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningStructure
helpviewer_keywords:
- MiningStructure element
ms.assetid: b943cd92-0ed8-4bd8-8fbc-7dab0534aede
caps.latest.revision: 48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ed39aafbe937c637abd7a6ec67fbd7343b62b116
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271831"
---
# <a name="miningstructure-element-assl"></a>Elemento MiningStructure (ASSL)
  Define la estructura de un conjunto de modelos de minería de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructures>  
   <MiningStructure>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</<Description>  
      <Source>...</Source>  
      <CreatedTimestamp>...</<CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastProcessed>...</LastProcessed>  
      <Translations>...</Translations>  
      <Language>...</Language>  
            <Collation>...</Collation>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <CacheMode>...</CacheMode>  
            <Columns>...</Columns>  
      <State>...</State>  
      <HoldoutActualSize>...</HoldoutActualSize>  
      <HoldoutMaxCases>...</HoldoutMaxCases>  
      <HoldoutMaxPercent>...</HoldoutMaxPercent>  
      <HoldoutSeed>...</HoldoutSeed>        
            <MiningStructurePermissions>...</<MiningStructurePermissions>  
            <MiningModels>...</MiningModels>  
            <Annotations>...</Annotations>  
   </MiningStructure>  
</MiningStructures>  
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
|Elementos primarios|[MiningStructures](../collections/miningstructures-element-assl.md)|  
|Elementos secundarios|[Las anotaciones](../collections/annotations-element-assl.md), [CacheMode](../properties/cachemode-element-assl.md), [intercalación](../properties/collation-element-assl.md), [columnas](../collections/columns-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [descripción ](../properties/description-element-assl.md), [ErrorConfiguration](errorconfiguration-element-assl.md),<br /><br /> [HoldoutActualSize](../properties/holdoutactualsize-element.md),<br /><br /> [HoldoutMaxCases](../properties/holdoutmaxcases-element.md),<br /><br /> [HoldoutMaxPercent](../properties/holdoutmaxpercent-element.md),<br /><br /> [HoldoutSeed](../properties/holdoutseed-element.md),<br /><br /> [Id. de](../properties/id-element-assl.md), [lenguaje](../properties/language-element-assl.md), [LastProcessed](../properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [MiningModels](../collections/miningmodels-element-assl.md), [ MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md), [nombre](../properties/name-element-assl.md), [origen](../properties/source-element-binding-assl.md), [estado](../properties/state-element-assl.md), [traducciones](../collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 La estructura de minería de datos define las columnas y los enlaces. Después de definir una estructura de minería, puede utilizarla para definir muchos modelos de minería. La estructura de minería y cada modelo de minería que contiene se pueden procesar independientemente.  
  
> [!NOTE]  
>  Las propiedades de exclusión, `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed` y `HoldoutActualSize`, se introdujeron en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Le permiten definir una partición en una estructura de minería que actúa como el conjunto de pruebas para todos los modelos de minería que están asociados a la estructura. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] no admite estas propiedades. Por consiguiente, si intenta utilizar estas propiedades en una instancia de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devolverá un error.  
  
## <a name="drillthrough-to-structure-columns"></a>Obtener detalles para las columnas de una estructura  
 En [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], se ha agregado un nuevo elemento de permiso a la [elemento MiningStructurePermissions &#40;ASSL&#41; ](../collections/miningstructurepermissions-element-assl.md) colección. Si agrega `AllowDrillthrough` permiso a ambos el [MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md) y [MiningModelPermission](miningmodelpermission-element-assl.md) colecciones, obtención de detalles está habilitada en el modelo de minería de datos a la estructura, de manera que los miembros de un rol que tenga `AllowDrillthrough` pueden consultar el modelo de minería de datos y devolver columnas de estructura que no se incluyeron en el modelo de permisos en el modelo.  
  
 Por consiguiente, para proteger información confidencial o datos personales, debería crear la vista del origen de datos de forma que enmascare los datos confidenciales y conceder permiso `AllowDrillthrough` en la estructura de minería solo cuando sea necesario. Para obtener más información, consulte [elemento AllowDrillThrough &#40;ASSL&#41;](../properties/allowdrillthrough-element-assl.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento MiningModel &#40;ASSL&#41;](miningmodel-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)   
 [SELECCIONE &AMP;#40;DMX&AMP;#41;](/sql/dmx/select-dmx)  
  
  
