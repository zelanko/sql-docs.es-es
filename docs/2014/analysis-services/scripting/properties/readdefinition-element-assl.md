---
title: Elemento ReadDefinition (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ReadDefinition Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReadDefinition
helpviewer_keywords:
- ReadDefinition element
ms.assetid: 1f250129-13b2-41b9-b083-b5aacddf0060
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 176f1fa1f1a9f4fca3e773d65a5fda01c2f6752d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218115"
---
# <a name="readdefinition-element-assl"></a>Elemento ReadDefinition (ASSL)
  Determina si los miembros pueden leer la definición de la base de datos o la definición de objetos de la base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Permission> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <ReadDefinition>...</ReadDefinition>  
   ...  
</Permission>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Ninguno*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[CubePermission](../objects/cubepermission-element-assl.md), [DatabasePermission](../objects/databasepermission-element-assl.md), [DimensionPermission](../objects/dimensionpermission-element-assl.md), [MiningModelPermission](../objects/miningmodelpermission-element-assl.md), [MiningStructurePermission ](../objects/miningstructurepermission-element-assl.md), [Permiso](../data-type/permission-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Ninguno*|El acceso a la definición del objeto no está permitido.|  
|*Basic*|El acceso básico a la definición del objeto está permitido. **Nota:** este permiso es necesario para crear cubos locales, vincular grupos de medidas y vincular dimensiones.|  
|*Permitido*|El acceso completo a la definición del objeto está permitido. **Nota:** este permiso se requiere para ejecutar un [Discover](../../xmla/xml-elements-methods-discover.md) XML llamada Analysis (XMLA) usando el parámetro DISCOVER_XML_METADATA.|  
  
 Los elementos que corresponden a los elementos primarios de `ReadDefinition` en el modelo de objetos de Objetos de administración de análisis (AMO) son  <xref:Microsoft.AnalysisServices.CubePermission>, <xref:Microsoft.AnalysisServices.DatabasePermission>, <xref:Microsoft.AnalysisServices.DimensionPermission>, <xref:Microsoft.AnalysisServices.MiningModelPermission>, <xref:Microsoft.AnalysisServices.MiningStructurePermission> y <xref:Microsoft.AnalysisServices.Permission>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento role &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
