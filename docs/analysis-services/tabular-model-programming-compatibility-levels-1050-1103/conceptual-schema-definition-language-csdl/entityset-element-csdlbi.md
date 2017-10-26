---
title: EntitySet, elemento (CSDLBI) | Documentos de Microsoft
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
applies_to:
- SQL Server 2016 Preview
ms.assetid: d4703c9e-5594-472e-a85b-0f5bd0d73d6f
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e48f4d90853e954618d770feda70c4a72d0f607a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="entityset-element-csdlbi"></a>EntitySet, elemento (CSDLBI)
  El elemento EntitySet define una colección de entidades de un tipo determinado en un modelo de datos CSDLBI.  
  
 El elemento EntitySet debe especificar cada uno de los tipos de entidad que se incluyen en el modelo de datos. La información sobre estas entidades del modelo se especifica enumerando las entidades secundarias del tipo, elemento Entity. Para más información, vea [EntityType, elemento &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md).  
  
 Las propiedades como la intercalación y el idioma se definen en el nivel del EntityContainer, no en los objetos individuales. Sin embargo, las columnas y los atributos de texto dentro del modelo pueden tener títulos o traducciones en otros idiomas.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen un elemento EntitySet.  
  
|Nombre del atributo|Es obligatorio|Descripción|  
|--------------------|-----------------|-----------------|  
|Caption|No|Descripción fácil de comprender del conjunto de entidades.|  
|CollectionCaption|No|Cadena que contiene el nombre plural de la entidad.|  
|ReferenceName|No|Contiene el nombre completo sin combinar de la entidad. En un modelo multidimensional, esto corresponde al nombre CubeDimension.|  
|Oculto|No|Indica si la entidad está oculta. De forma predeterminada, las entidades no están ocultas.|  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestran las definiciones de las tablas Date y Geography del modelo tabular AdventureWorks.  
  
```  
  
<EntitySet   
   Name="Date"   
   EntityType="Sandbox. Date">  
<bi:EntitySet />  
</EntitySet>  
  
<EntitySet   
   Name="Geography"   
   EntityType="Sandbox.Geography">  
<bi:EntitySet />  
</EntitySet>  
```  
  
## <a name="example"></a>Ejemplo  
 **Multidimensional**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestran varios elementos EntitySet del cubo de operaciones de Contoso Retail.  
  
```  
  
<EntitySet Name="Outage" EntityType="Sandbox.Outage">  
       <bi:EntitySet />  
</EntitySet>  
  
<EntitySet Name="Store" EntityType="Sandbox.Store">  
     <bi:EntitySet />  
</EntitySet>  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia técnica de anotaciones de BI para CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  

