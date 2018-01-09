---
title: MemberRef, elemento (CSDLBI) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 399aaa34-896c-48e7-aacb-18564f31b568
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8c1bb47c2273d79e320e53b49c524112b067a2d3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="memberref-element-csdlbi"></a>MemberRef, elemento (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]El elemento MemberRef identifica el nombre de una propiedad que es el destino de una referencia.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento MemberRef.  
  
|Nombre|Es obligatorio|Description|  
|----------|-----------------|-----------------|  
|Nombre|Sí|El nombre de la propiedad contenida en un elemento MemberRef.|  
  
## <a name="memberrefs-element"></a>Elemento MemberRefs  
 MemberRefs es un tipo complejo que define una colección de miembros en la que cada miembro está incluido en un elemento MemberRef.  
  
 En la tabla siguiente se enumeran los elementos y atributos del tipo MemberRefs.  
  
|Nombre|Es obligatorio|Description|  
|----------|-----------------|-----------------|  
|MemberRef|Sí|Cadena que contiene la referencia de miembro.|  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se representa una parte del modelo de datos de ejemplo AdventureWorks que define la tabla Products. Aquí se utiliza el elemento MemberRef para cada columna incluida en el conjunto de campos predeterminado para el modelo.  
  
```  
  
<bi:EntityType>  
   <bi:DefaultDetails>  
     <bi:MemberRef Name="Color" />  
     <bi:MemberRef Name="DealerPrice" />  
     <bi:MemberRef Name="Status" />  
   </bi:DefaultDetails>  
  
```  
  
## <a name="example"></a>Ejemplo  
 **Multidimensional**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se representa una parte del cubo de operaciones de Contoso que define la tabla Bikes. En este ejemplo, se utiliza un elemento MemberRef para especificar el nombre de la columna utilizada como el conjunto de campos predeterminado en los informes, y se usa otro elemento MemberRef para hacer referencia a la columna que proporciona el criterio de ordenación.  
  
```  
  
<bi:DefaultDetails>  
   <bi:MemberRef Name="Color" />  
</bi:DefaultDetails>  
  
<bi:SortMembers>  
   <bi:MemberRef Name="Color" />  
</bi:SortMembers>  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia técnica para las anotaciones de Business Intelligence en CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
