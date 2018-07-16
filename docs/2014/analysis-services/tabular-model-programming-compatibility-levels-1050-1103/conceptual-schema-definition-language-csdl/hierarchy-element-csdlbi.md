---
title: Hierarchy, elemento (CSDLBI) | Microsoft Docs
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
ms.assetid: 9debb638-1b28-401b-9499-8f63943863e9
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: be67c3059f09beefae68d0264fd0316579344d64
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250795"
---
# <a name="hierarchy-element-csdlbi"></a>Hierarchy, elemento (CSDLBI)
  El elemento Hierarchy es un contenedor lógico para los campos de una tabla que se pueden vincular entre sí para formar una jerarquía. Este elemento se deriva del elemento Member de CSDL y se ha extendido para admitir las jerarquías creadas en los modelos de datos de Business Intelligence.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento Hierarchy.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|Documentación|no|Descripción de la jerarquía.|  
|Nivel|Sí|Uno o más elementos Level que definen las columnas utilizadas en la jerarquía.<br /><br /> Vea [Level, elemento &#40;CSDLBI&#41;](level-element-csdlbi.md).|  
  
## <a name="remarks"></a>Notas  
 En los modelos tabulares, las jerarquías se crean especificando relaciones de elementos primarios y secundarios entre las columnas de la misma tabla. Para más información, vea [Jerarquías &#40;SSAS tabular&#41;](../../tabular-models/hierarchies-ssas-tabular.md).  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente, en la versión 1.0 de CSDLBI, se muestra una jerarquía del modelo de ejemplo AdventureWorks que se ha agregado a la tabla Products.  
  
```  
  
<bi:Hierarchy Name="Categoryy">  
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
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestra una jerarquía del cubo de operaciones de Contoso Retail.  
  
```  
  
<bi:Hierarchy Name="Product_Hierarchy" Caption="Product Hierarchy" ReferenceName="Product Hierarchy">  
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
  
  
