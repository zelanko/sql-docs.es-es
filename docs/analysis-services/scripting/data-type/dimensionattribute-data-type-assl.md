---
title: Tipo de datos DimensionAttribute (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13264626bcfd1984260bd65b6162d02df0b267d6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="dimensionattribute-data-type-assl"></a>Tipo de datos DimensionAttribute (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|Tipos de datos base|Ninguno|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [AttributeHierarchyDisplayFolder](../../../analysis-services/scripting/properties/attributehierarchydisplayfolder-element-assl.md), [AttributeHierarchyEnabled](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md), [AttributeHierarchyOptimizedState](../../../analysis-services/scripting/properties/attributehierarchyoptimizedstate-element-assl.md), [AttributeHierarchyOrdered](../../../analysis-services/scripting/properties/attributehierarchyordered-element-assl.md), [AttributeHierarchyVisible](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md), [AttributeRelationships](../../../analysis-services/scripting/collections/attributerelationships-element-assl.md), [CustomRollupColumn](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md), [CustomRollupPropertiesColumn](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md), [DefaultMember](../../../analysis-services/scripting/properties/defaultmember-element-assl.md), [Description](../../../analysis-services/scripting/properties/description-element-assl.md), [DiscretizationBucketCount](../../../analysis-services/scripting/properties/discretizationbucketcount-element-assl.md), [DiscretizationMethod](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md), [EstimatedCount](../../../analysis-services/scripting/properties/estimatedcount-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [InstanceSelection](../../../analysis-services/scripting/properties/instanceselection-element-assl.md), [IsAggregatable](../../../analysis-services/scripting/properties/isaggregatable-element-assl.md), [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md), [KeyUniquenessGuarantee](../../../analysis-services/scripting/properties/keyuniquenessguarantee-element-assl.md), [MemberNamesUnique](../../../analysis-services/scripting/properties/membernamesunique-element-assl.md), [MembersWithData](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md), [MembersWithDataCaption](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md), [Name](../../../analysis-services/scripting/properties/name-element-assl.md), [NameColumn](../../../analysis-services/scripting/objects/namecolumn-element-assl.md), [NamingTemplate](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md), [NamingTemplateTranslations](../../../analysis-services/scripting/collections/namingtemplatetranslations-element-assl.md), [OrderBy](../../../analysis-services/scripting/properties/orderby-element-assl.md), [OrderByAttributeID](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md), [RootMemberIf](../../../analysis-services/scripting/properties/rootmemberif-element-assl.md), [SkippedLevelsColumn](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md), [Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md), [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md), [Type](../../../analysis-services/scripting/properties/type-element-dimensionattribute-assl.md), [UnaryOperatorColumn](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md), [Usage](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md), [ValueColumn](../../../analysis-services/scripting/objects/valuecolumn-element-assl.md)|  
|Elementos derivados|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) (colección[Attributes](../../../analysis-services/scripting/collections/attributes-element-assl.md) de [Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 Las restricciones siguientes se aplican cuando se ejecuta el servicio en los valores de propiedad de configuración DeploymentMode 1 y 2 (modos SharePoint y Tabular, utilizadas para ejecutar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] y bases de datos de modelo tabular):  
  
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
  
 Los elementos siguientes no son compatibles cuando se ejecuta el servicio de configuración DeploymentMode valores de propiedad de 1 y 2 (modos SharePoint y Tabular, utilizadas para ejecutar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] y bases de datos de modelo tabular):  
  
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
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
