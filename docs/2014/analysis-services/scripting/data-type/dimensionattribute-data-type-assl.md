---
title: Tipo de datos DimensionAttribute (ASSL) | Microsoft Docs
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
- DimensionAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DimensionAttribute
helpviewer_keywords:
- DimensionAttribute data type
ms.assetid: 94349a87-b284-49d1-ac72-888f0375ceb8
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9e07d7b7c313c4d9d21e8e562f2ed6893a08b42
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194295"
---
# <a name="dimensionattribute-data-type-assl"></a>Tipo de datos DimensionAttribute (ASSL)
  Define un tipo de datos primitivo que representa un atributo de una dimensión.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <Type>...</Type>  
   <Usage>...</Usage>  
   <Source>...</Source>  
   <EstimatedCount>...</EstimatedCount>  
   <KeyColumns>...</KeyColumns>  
   <NameColumn>...</NameColumn>  
   <ValueColumn>...</ValueColumn>  
   <Translations>...</Translations>  
   <AttributeRelationships>...</AttributeRelationships>  
   <DiscretizationMethod>...</DiscretizationMethod>  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   <RootMemberIf>...</RootMemberIf>  
   <OrderBy>...</OrderBy>  
   <DefaultMember>...</DefaultMember>  
   <OrderByAttributeID>...</OrderByAttributeID>  
   <SkippedLevelsColumn>...</SkippedLevelsColumn>  
   <NamingTemplate>...</NamingTemplate>  
   <MembersWithData>...</MembersWithData>  
   <MembersWithDataCaption>...</MembersWithDataCaption>  
   <NamingTemplateTranslations>...</NamingTemplateTranslations>  
   <CustomRollupColumn>...</CustomRollupColumn>  
   <CustomRollupPropertiesColumn>...</CustomRollupPropertiesColumn>  
   <UnaryOperatorColumn>...</UnaryOperatorColumn>  
   <AttributeHierarchyOrdered>...</AttributeHierarchyOrdered>  
   <MemberNamesUnique>...</MemberNamesUnique>  
   <IsAggregatable>...</IsAggregatable>  
   <AttributeHierarchyEnabled>...</AttributeHierarchyEnabled>  
   <AttributeHierarchyOptimizedState>...</AttributeHierarchyOptimizedState>  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   <AttributeHierarchyDisplayFolder>...</AttributeHierarchyDisplayFolder>  
   <KeyUniquenessGuarantee>...<KeyUniquenessGuarantee>  
   <InstanceSelection>...</InstanceSelection>  
   <Annotations>...</Annotations>  
</DimensionAttribute>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Annotations](../collections/annotations-element-assl.md), [AttributeHierarchyDisplayFolder](../properties/displayfolder-element-assl.md), [AttributeHierarchyEnabled](../properties/enabled-element-assl.md), [AttributeHierarchyOptimizedState](../properties/state-element-assl.md), [AttributeHierarchyOrdered](../properties/attributehierarchyordered-element-assl.md), [AttributeHierarchyVisible](../properties/visible-element-assl.md), [AttributeRelationships](../collections/relationships-element-assl.md), [CustomRollupColumn](../objects/column-element-assl.md), [CustomRollupPropertiesColumn](../objects/customrolluppropertiescolumn-element-assl.md), [DefaultMember](../objects/member-element-assl.md), [Description](../properties/description-element-assl.md), [DiscretizationBucketCount](../properties/discretizationbucketcount-element-assl.md), [DiscretizationMethod](../properties/discretizationmethod-element-assl.md), [EstimatedCount](../properties/estimatedcount-element-assl.md), [ID](../properties/id-element-assl.md), [InstanceSelection](../properties/instanceselection-element-assl.md), [IsAggregatable](../properties/isaggregatable-element-assl.md), [KeyColumns](../collections/columns-element-assl.md), [KeyUniquenessGuarantee](../properties/keyuniquenessguarantee-element-assl.md), [MemberNamesUnique](../properties/membernamesunique-element-assl.md), [MembersWithData](../objects/data-element-assl.md), [MembersWithDataCaption](../properties/caption-element-assl.md), [Name](../properties/name-element-assl.md), [NameColumn](../objects/namecolumn-element-assl.md), [NamingTemplate](../properties/namingtemplate-element-assl.md), [NamingTemplateTranslations](../collections/translations-element-assl.md), [OrderBy](../properties/orderby-element-assl.md), [OrderByAttributeID](../properties/attributeid-element-assl.md), [RootMemberIf](../properties/rootmemberif-element-assl.md), [SkippedLevelsColumn](../objects/skippedlevelscolumn-element-assl.md), [Source](../properties/source-element-binding-assl.md), [Translations](../collections/translations-element-assl.md), [Type](../properties/type-element-dimensionattribute-assl.md), [UnaryOperatorColumn](../objects/unaryoperatorcolumn-element-assl.md), [Usage](../properties/usage-element-dimensionattribute-assl.md), [ValueColumn](../objects/valuecolumn-element-assl.md)|  
|Elementos derivados|[Attribute](../objects/attribute-element-assl.md) (colección[Attributes](../collections/attributes-element-assl.md) de [Dimension](../objects/dimension-element-assl.md))|  
  
## <a name="remarks"></a>Notas  
 Las restricciones siguientes se aplican al ejecutar el servicio en los valores de la propiedad de configuración DeploymentMode 1 y 2 (modos SharePoint y tabular, que se usan para ejecutar las bases de datos de modelo tabular y PowerPivot):  
  
-   El elemento Usage solo acepta los valores KEY o REGULAR.  
  
-   El elemento IsAggregatable no puede ser false.  
  
-   El elemento OrderBy solo acepta los valores KEY o PROPERTYKEY.  
  
-   Una columna calculada no puede ser una clave principal de la tabla.  
  
-   Una columna calculada no puede contener DataSize en el enlace.  
  
-   Para cada columna calculada se realiza una validación de la sintaxis antes de guardar la definición de los atributos.  
  
-   Para AttributeRelationships, RelationshipType debe establecerse en el valor Flexible.  
  
-   El atributo ‘RowNumber’, identificado por ‘RowNumber’, debe ser de tipo entero.  
  
-   Solo el atributo ‘RowNumber’ puede tener un KeyBinding de tipo RowNumberBinding.  
  
-   Todos los atributos distintos de ‘RowNumber’ deben tener una cardinalidad de uno en relación con la clave, a menos que el propio atributo sea la clave.  
  
-   Cuando la columna especificada por OrderBy también sea PropertyKey, OrderByAttributeId no podrá apuntar a la columna del número de fila.  
  
-   Los atributos utilizados como claves deben estar relacionados con todos los demás atributos; no se admiten otros tipos de relaciones.  
  
-   El elemento NullProcessing no puede establecerse en ‘UnknownMember’.  
  
-   Los enlaces no se pueden establecer en ‘Value’.  
  
 Los siguientes elementos no se admiten al ejecutar el servicio con los valores de la propiedad de configuración DeploymentMode 1 y 2 (modos SharePoint y tabular, que se usan para ejecutar las bases de datos de modelo tabular y PowerPivot):  
  
-   AttributeHierarchyOptimizedState  
  
-   CustomRollupColumn  
  
-   CustomRollupPropertiesColumn  
  
-   DefaultMember  
  
-   DiscretizationBucketCount  
  
-   DiscretizationMethod  
  
-   SkippedLevelsColumn  
  
-   Source  
  
-   UnaryOperatorColumn  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
