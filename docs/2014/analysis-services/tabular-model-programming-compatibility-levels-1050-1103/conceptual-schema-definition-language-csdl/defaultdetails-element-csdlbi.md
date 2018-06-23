---
title: DefaultDetails, elemento (CSDLBI) | Documentos de Microsoft
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
ms.assetid: 05a08baa-23cc-4011-9c2e-f60a20bb87da
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 2b10c8b155cb0f06754ed6c2bc45062ae5e69898
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203740"
---
# <a name="defaultdetails-element-csdlbi"></a>DefaultDetails, elemento (CSDLBI)
  El elemento DefaultDetails representa una lista de referencias de propiedad que juntas definen el “conjunto de campos predeterminado” de columnas de la tabla. Cada propiedad solo puede hacer referencia a una medida o a una columna.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento DefaultDetails.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|DefaultDetailsPosition|no|Entero positivo que indica la presencia y la posición en la colección.|  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestra un extracto del modelo de datos de ejemplo AdventureWorks. Solo hay un conjunto de columnas predeterminado para la tabla Employees (Title). Sin embargo, se han definido tres columnas como el conjunto de campos predeterminado para la tabla Products.  
  
```  
  
<EntityType   
    Name="DimEmployee">  
....  
   <bi:DefaultDetails>  
      <bi:MemberRef Name="Title" />  
   </bi:DefaultDetails>  
.....  
<EntityType   
    Name="Products">  
.....  
   <bi:DefaultDetails>  
      <bi:MemberRef Name="Color" />  
      <bi:MemberRef Name="DealerPrice" />  
      <bi:MemberRef Name="Status" />  
   </bi:DefaultDetails>  
  
```  
  
## <a name="example"></a>Ejemplo  
 **Multidimensional**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestra un extracto de la definición de la tabla Bike en el cubo de operaciones de Contoso. Esta anotación indica que la columna Color se debe mostrar de forma predeterminada si no se especifica ninguna otra columna de visualización.  
  
```  
  
<EntityType Name="Bike">  
   <Key>  
   <PropertyRef Name="RowNumber" />  
   </Key>  
....  
<bi:EntityType>  
   <bi:DisplayKey>  
      <bi:MemberRef Name="Color" />  
   </bi:DisplayKey>  
   <bi:DefaultDetails>  
      <bi:MemberRef Name="Color" />  
   </bi:DefaultDetails>  
   <bi:SortMembers>  
      <bi:MemberRef Name="Color" />  
   </bi:SortMembers>  
....  
</bi:EntityType>  
</EntityType>  
```  
  
## <a name="see-also"></a>Vea también  
 [Descripción del modelo de objetos tabulares](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [Conceptos de CSDLBI](../csdlbi-concepts.md)  
  
  