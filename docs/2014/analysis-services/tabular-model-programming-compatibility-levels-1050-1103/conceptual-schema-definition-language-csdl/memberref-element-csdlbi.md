---
title: MemberRef, elemento (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 399aaa34-896c-48e7-aacb-18564f31b568
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bb0912afd99c7a4859ca4750a3ba1b66fdecd5f5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205725"
---
# <a name="memberref-element-csdlbi"></a>MemberRef, elemento (CSDLBI)
  El elemento MemberRef identifica el nombre de una propiedad que es el destino de una referencia.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento MemberRef.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|Nombre|Sí|El nombre de la propiedad contenida en un elemento MemberRef.|  
  
## <a name="memberrefs-element"></a>Elemento MemberRefs  
 MemberRefs es un tipo complejo que define una colección de miembros en la que cada miembro está incluido en un elemento MemberRef.  
  
 En la tabla siguiente se enumeran los elementos y atributos del tipo MemberRefs.  
  
|Nombre|Es obligatorio|Descripción|  
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
 [Referencia técnica para las anotaciones de Business Intelligence en CSDL](technical-reference-for-bi-annotations-to-csdl.md)  
  
  
