---
title: Elemento (ASSL) de la base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Database Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DATABASE
helpviewer_keywords:
- Database element
ms.assetid: c3bc7eaf-ed0d-4395-a3b7-8d9cfacfe911
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 46166d77185836c65fe1d026255620dfb87c1f66
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191035"
---
# <a name="database-element-assl"></a>Elemento Database (ASSL)
  Define un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Databases>  
   <Database>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastUpdate>...</LastUpdate>  
      <Description>...</Description>  
      <State>   </State>  
      <AggregationPrefix>...</AggregationPrefix>  
      <EstimatedSize>...</EstimatedSize>  
      <LastProcessed>...</LastProcessed>  
      <Language>...</Language>  
            <Collation>...</Collation>  
      <Visible>...</Visible>  
      <MasterDatasourceID>...</MasterDataSourceID>  
      <Accounts>...</Accounts>  
      <DataSources>...</DataSources>  
      <DataSourceViews>...</DataSourceViews>  
      <Dimensions>...</Dimensions>  
      <Cubes>...</Cubes>  
      <MiningStructures>...</MiningStructures>  
            <Roles>...</Roles>  
      <Assemblies>...</Assemblies>  
      <DatabasePermissions>...</DatabasePermissions>  
            <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Database>  
</Databases>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Bases de datos](../collections/databases-element-assl.md)|  
|Elementos secundarios|[Cuentas](../collections/accounts-element-assl.md), [AggregationPrefix](../properties/aggregationprefix-element-assl.md), [anotaciones](../collections/annotations-element-assl.md), [ensamblados](../collections/assemblies-element-assl.md), [intercalación](../properties/collation-element-assl.md), [ CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [cubos](../collections/cubes-element-assl.md), [DatabasePermissions](../collections/databasepermissions-element-assl.md), [orígenes de datos](../collections/datasources-element-assl.md), [DataSourceViews](../collections/datasourceviews-element-assl.md), [Descripción](../properties/description-element-assl.md), [dimensiones](../collections/dimensions-element-assl.md), [EstimatedSize](../properties/estimatedsize-element-assl.md), [ID](../properties/id-element-assl.md), [lenguaje](../properties/language-element-assl.md), [ LastProcessed](../properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [LastUpdate](../properties/lastupdate-element-assl.md), [MasterDatasourceID](../properties/datasourceid-element-assl.md), [MiningStructures](../collections/miningstructures-element-assl.md), [Nombre](../properties/name-element-assl.md), [Roles](../collections/roles-element-assl.md), [estado](../properties/state-element-assl.md), [traducciones](../collections/translations-element-assl.md), [Visible](../properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Database>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Server &#40;ASSL&#41;](server-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
