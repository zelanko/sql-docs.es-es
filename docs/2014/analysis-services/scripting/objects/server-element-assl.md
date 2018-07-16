---
title: Elemento Server (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Server Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- server
helpviewer_keywords:
- Server element
ms.assetid: 92ca67f6-817e-4a75-9244-8f8bcf412190
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d5ae1dc9c10bce01cb9b0f90da2ef25b023392f3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319235"
---
# <a name="server-element-assl"></a>Elemento Server (ASSL)
  Describe una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Server>  
   <!—These elements are common to each major object -->  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreatedTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <Description>...</Description>  
   <Annotations>...</Annotations>  
   <!-- server elements or properties -->  
   <ProductName>...</ProductName>  
   <Edition>...</Edition>  
   <EditionId>...</Edition>  
   <Version>...</Version>  
   <ServerMode>...</ServerMode>  
   <ProductLevel>...</Databases>  
   <Databases>...</Databases>  
   <Assemblies>...</Assemblies>  
   <Traces>...</Traces>  
   <Roles>...</Roles>  
   <ServerProperties>...</ServerProperties>  
</Server>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Nombre](../properties/name-element-assl.md), [ID](../properties/id-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [descripción](../properties/description-element-assl.md), [anotaciones](../collections/annotations-element-assl.md), [ProductName](../properties/productname-element-assl.md), [Edition](../properties/edition-element-assl.md), [EditionId](../../xmla/xml-elements-properties/editionid-element.md), [versión](../properties/version-element-assl.md), [ServerMode](../../xmla/xml-elements-properties/editionid-element.md), [ProductLevel](../../xmla/xml-elements-properties/productlabel-element.md), [bases de datos](../collections/databases-element-assl.md), [ensamblados](../collections/assemblies-element-assl.md), [seguimientos](../collections/traces-element-assl.md), [Roles](../collections/roles-element-assl.md), [ServerProperties](../collections/serverproperties-element-assl.md)>|  
  
## <a name="remarks"></a>Notas  
 El elemento `Server` representa una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y actúa como el nodo más alto en la jerarquía de nodos del Lenguaje de scripting de Analysis Services (ASSL).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Server>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
