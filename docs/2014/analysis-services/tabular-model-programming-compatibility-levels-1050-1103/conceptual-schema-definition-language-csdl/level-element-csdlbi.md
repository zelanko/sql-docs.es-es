---
title: Nivel de elemento (CSDLBI) | Microsoft Docs
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
ms.assetid: fdf75c47-77dc-4bdb-9931-8eca198fdb88
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3fd89aaa69e8dc2b29b80ca82f89d1453dc44017
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37211485"
---
# <a name="level-element-csdlbi"></a>Level, elemento (CSDLBI)
  El elemento Level es un tipo complejo que define un solo nivel de una jerarquía  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento Level.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|Source|Sí|Contenedor para la referencia de propiedad.|  
|PropertyRef|Sí|Referencia a una propiedad de instancia. Otros atributos del nivel, como títulos, nombre y nombre de referencia, se pueden obtener de la propiedad de instancia a la que se hace referencia. En tal caso, no necesita especificarlos en el elemento Level.|  
  
## <a name="remarks"></a>Notas  
 Para más información sobre las jerarquías en los modelos tabulares, vea [Hierarchy, elemento &#40;CSDLBI&#41;](hierarchy-element-csdlbi.md).  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestra la definición de varios niveles en una jerarquía del ejemplo de modelo tabular AdventureWorks.  
  
```  
  
<bi:Hierarchy Name="Category">  
   <bi:Level Name="CategoryName">  
     <bi:Source>  
       <bi:PropertyRef Name="CategoryName" />  
     </bi:Source>  
   </bi:Level>  
   <bi:Level Name="ProductName">  
     <bi:Source>  
       <bi:PropertyRef Name="ProductName" />  
     </bi:Source>  
   </bi:Level>  
</bi:Hierarchy>  
```  
  
## <a name="example"></a>Ejemplo  
 **Multidimensional**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestra una jerarquía con varios niveles del cubo de operaciones de Contoso.  
  
```  
<bi:Hierarchy   
   Name="Product_Hierarchy"   
   Caption="Product Hierarchy"   
   ReferenceName="Product Hierarchy">  
     <bi:Documentation>  
        <bi:Summary>DESCRIPTION_ProductModelCateg_Hierarchies</bi:Summary>  
     </bi:Documentation>  
  
     <bi:Level Name="ProductLine">  
        <bi:Source>  
        <bi:PropertyRef Name="ProductLine" />  
        </bi:Source>  
     </bi:Level>  
  
     <bi:Level Name="ModelName">  
        <bi:Source>  
        <bi:PropertyRef Name="ModelName" />  
        </bi:Source>  
     </bi:Level>  
</bi:Hierarchy>  
```  
  
## <a name="see-also"></a>Vea también  
 [Descripción del modelo de objetos tabulares](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [Descripción de las funciones para jerarquías de elementos primarios y secundarios en DAX](https://msdn.microsoft.com/library/gg492192(v=sql.120).aspx)   
 [Configurar la &#40;todas&#41; nivel para las jerarquías de atributo](../../multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
