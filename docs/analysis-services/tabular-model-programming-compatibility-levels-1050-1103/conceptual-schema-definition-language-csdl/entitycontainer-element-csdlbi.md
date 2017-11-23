---
title: EntityContainer, elemento (CSDLBI) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: e328558e-16b0-4d4a-a79a-fdd3c9493595
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e5328a9c360fa4465e0bcf53bd0f017447c7c113
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="entitycontainer-element-csdlbi"></a>EntityContainer, elemento (CSDLBI)
  El elemento EntityContainer es un tipo complejo, basado en el tipo EntityContainer de CSDL, que define una colección de entidades en un único modelo de datos. En una aplicación de Business Intelligence, un EntityContainer representa un modelo de datos que puede contener varias tablas con columnas vinculadas mediante relaciones, así como cálculos, medidas y KPI. Conceptualmente, es similar a una base de datos o un origen de datos.  
  
 El elemento EntityContainer debe especificar cada uno de los tipos de entidad que se incluyen en el modelo de datos, incluidas las tablas y las relaciones. La información sobre estas entidades del modelo se especifica enumerando las entidades secundarias del tipo, elemento Entity. Para más información, vea [EntityType, elemento &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md).  
  
 Las propiedades como la intercalación y el idioma se definen en el nivel del EntityContainer, no en los objetos individuales. Sin embargo, las columnas y los atributos de texto dentro del modelo pueden tener títulos o traducciones en otros idiomas.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se describen los elementos y atributos que definen el elemento EntityContainer.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|Nombre|Sí|El nombre del modelo de datos.|  
|Caption|No|Descripción de la base de datos o del modelo de datos.|  
|Culture|Sí|Cadena que contiene el LCID de la solicitud.|  
|CompareOptions|Sí|Opciones de comparación de cadenas y de ordenación para el modelo específicas del idioma.|  
|DirectQueryMode|No|Enumeración que indica el modo de consulta cuando el modelo utiliza el modo DirectQuery.|  
|Elemento EntitySet|Sí|[EntitySet, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entityset-element-csdlbi.md)|  
|Elemento AssociationSet|No|[AssociationSet, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/associationset-element-csdlbi.md)|  
  
## <a name="compareoptions-element"></a>Elemento CompareOptions  
 El atributo CompareOptions define las propiedades de intercalación que se aplican al modelo de datos. Las propiedades definidas por este atributo se derivan de la configuración del criterio de ordenación, de la distinción de kana y de la distinción entre mayúsculas y minúsculas establecida en la base de datos de Analysis Services en tiempo de diseño del modelo. En la tabla siguiente se describen los valores que se incluyen como parte del atributo CompareOptions.  
  
|Valor|Description|  
|-----------|-----------------|  
|IgnoreCase|Valor booleano que indica si las comparaciones de cadenas deben distinguir entre mayúsculas y minúsculas.|  
|IgnoreNonSpace|Valor booleano que indica si las comparaciones de cadenas deben omitir los caracteres de combinación sin espacio, como los signos diacríticos.|  
|IgnoreKanaType|Valor booleano que indica si las comparaciones de cadenas deben omitir el tipo de kana.|  
|IgnoreWidth|Valor booleano que indica si las comparaciones de cadenas deben omitir el ancho de caracteres.|  
  
## <a name="directquerymode"></a>DirectQueryMode  
 **DirectQueryMode**  
  
 El tipo simple, DirectQueryMode, define el tipo de consulta que se utiliza de forma predeterminada cuando el modelo está habilitado para recuperar datos directamente desde un origen de datos relacional. Esta propiedad solo se aplica a los modelos tabulares que se ejecutan en el modo DirectQuery. En la siguiente tabla se muestran los posibles valores para la enumeración del modo DirectQuery.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|InMemory|Indica que las consultas que se realicen en el modelo utilizarán datos de la memoria caché.|  
|InMemoryWithDirectQuery|Indica que, de forma predeterminada, las consultas que se realicen en el modelo utilizarán datos del origen de datos relacional.|  
|DirectQueryWithInMemory|Indica que, de forma predeterminada, las consultas que se realicen en el modelo utilizarán datos de la memoria caché.|  
|DirectQuery|Indica que las consultas que se realicen en el modelo solo utilizarán datos del origen de datos relacional.|  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se representa una parte del modelo de datos tabular AdventureWorks.  
  
```  
  
<EntityContainer   
     Name="Sandbox">  
   <EntitySet   
       Name="DimEmployee"   
       EntityType="Sandbox.DimEmployee">  
   <bi:EntitySet />  
   </EntitySet>  
  
   <EntitySet   
     Name="DimProduct"   
       EntityType="Sandbox.DimProduct">  
    <bi:EntitySet />  
    </EntitySet>  
  
<bi:EntityContainer Caption="AWSimple" Culture="en-US">  
  
```  
  
## <a name="example"></a>Ejemplo  
 **Multidimensional**  
  
 El ejemplo siguiente, en la versión 1.1 de CSDLBI, es un extracto del cubo de operaciones de Contoso.  
  
```  
  
<EntityContainer   
     Name="Sandbox">  
   <EntitySet   
      Name="Bike"   
      EntityType="Sandbox.Bike">  
    <bi:EntitySet Hidden="true" />  
   </EntitySet>  
…  
<bi:EntityContainer   
   Caption="CSDLTest"   
   Culture="en-US">  
<bi:CompareOptions   
   IgnoreCase="true" />  
</bi:EntityContainer>  
</EntityContainer>  
  
```  
  
## <a name="see-also"></a>Vea también  
 [EntitySet, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entityset-element-csdlbi.md)  
  
  
