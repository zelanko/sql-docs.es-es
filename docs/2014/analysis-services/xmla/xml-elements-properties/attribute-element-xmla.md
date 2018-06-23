---
title: Atributo de elemento (XMLA) | Documentos de Microsoft
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
- Attribute Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Attribute
- microsoft.xml.analysis.attribute
- urn:schemas-microsoft-com:xml-analysis#Attribute
helpviewer_keywords:
- Attribute element
ms.assetid: 0df9cf44-dc5f-4234-8a5a-daac8aabc0d6
caps.latest.revision: 17
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 665626323e435eeed50b73f4d94de4506dba4f19
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106195"
---
# <a name="attribute-element-xmla"></a>Elemento Attribute (XMLA)
  Define o filtra un miembro en un atributo en el que un elemento primario [insertar](../xml-elements-commands/insert-element-xmla.md), [actualización](../xml-elements-commands/update-element-xmla.md), o [Drop](../xml-elements-commands/drop-element-xmla.md) ejecuta un comando.  
  
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Atributos](attributes-element-xmla.md)|  
  
 **Elementos secundarios**  
  
|||  
|-|-|  
|**Antecesor o elemento primario**|**Elemento secundario**|  
|[Quitar](../xml-elements-commands/drop-element-xmla.md), [donde](name-element-xmla.md), [claves](keys-element-xmla.md)|  
|[Insertar](../xml-elements-commands/insert-element-xmla.md), [actualización](../xml-elements-commands/update-element-xmla.md)|[AttributeName](name-element-xmla.md), [CustomRollup](customrollup-element-xmla.md), [CustomRollupProperties](properties-element-xmla.md), [claves](keys-element-xmla.md), [nombre](name-element-xmla.md), [ SkippedLevels](skippedlevels-element-xmla.md), [traducciones](translations-element-xmla.md), [UnaryOperator](unaryoperator-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 El `Attribute` elemento define el miembro de atributo que se inserta, actualiza o elimina, respectivamente, la `Insert`, `Update`, o `Drop` comando. Como estos comandos solo pueden funcionar en un miembro de atributo a la vez, el [atributos](attributes-element-xmla.md) colección de la `Insert`, `Update`, y `Drop` comandos solo pueden contener un `Attribute` elemento. Sin embargo, la colección `Attributes` del elemento `Where` para los comandos `Drop` y `Update` puede contener más de un elemento `Attribute`, para que pueda filtrar los atributos que se van a quitar o actualizar en una dimensión con permiso de escritura.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)   
 [Dimensiones habilitadas para escritura](../../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  