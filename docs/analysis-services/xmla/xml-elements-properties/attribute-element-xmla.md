---
title: Atributo de elemento (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f32b81a122fe82e2874c763bf68154f03ea75e49
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574867"
---
# <a name="attribute-element-xmla"></a>Elemento Attribute (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Define o filtra un miembro en un atributo en el que un elemento primario [insertar](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [actualización](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), o [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) ejecuta un comando.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Attributes>  
   ...  
   <Attribute>  
      <AttributeName>...</AttributeName>  
      <Keys>...</Keys>  
      <!-- The following elements are included only for attributes contained in the Attributes element of a parent Insert or Update command -->  
      <Name>...</Name>  
      <Translations>...</Translations>  
      <CustomRollup>...</CustomRollup>  
      <CustomRollupProperties>...</CustomRollupProperties>  
      <UnaryOperator>...</UnaryOperator>  
      <SkippedLevels>...</SkippedLevels>  
   </Attribute>  
   ...  
</Attributes>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Atributos](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)|  
|Elementos secundarios|Vea la tabla siguiente.|  
  
|Antecesor o elemento primario|Elemento secundario|  
|------------------------|-------------------|  
|[Quitar](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [donde](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md), [claves](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|[Insertar](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [actualización](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|[AttributeName](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md), [CustomRollup](../../../analysis-services/xmla/xml-elements-properties/customrollup-element-xmla.md), [CustomRollupProperties](../../../analysis-services/xmla/xml-elements-properties/customrollupproperties-element-xmla.md), [claves](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md), [nombre](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md), [ SkippedLevels](../../../analysis-services/xmla/xml-elements-properties/skippedlevels-element-xmla.md), [traducciones](../../../analysis-services/xmla/xml-elements-properties/translations-element-xmla.md), [UnaryOperator](../../../analysis-services/xmla/xml-elements-properties/unaryoperator-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento **Attribute** define del miembro de atributo que el comando **Insert**, **Update**o **Drop** inserta, actualiza o elimina, respectivamente. Como estos comandos solo pueden funcionar en un miembro de atributo a la vez, el [atributos](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md) colección de la **insertar**, **actualización**, y **Drop**comandos solo pueden contener una **atributo** elemento. Sin embargo, la colección **Attributes** del elemento **Where** para los comandos **Drop** y **Update** puede contener más de un elemento **Attribute** , para que pueda filtrar los atributos que se van a quitar o actualizar en una dimensión con permiso de escritura.  
  
## <a name="see-also"></a>Vea también
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)   
 [Dimensiones habilitadas para escritura](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
