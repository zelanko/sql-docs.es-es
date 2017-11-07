---
title: NavigationProperty, elemento (CSDLBI) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
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
ms.assetid: a36b4d3b-6a6c-489b-8a46-2e6b925b568f
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5b1af93e52bc1a2fbd95059c86f73a0481572399
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="navigationproperty-element-csdlbi"></a>NavigationProperty, elemento (CSDLBI)
  El elemento NavigationProperty es un tipo complejo que extiende el tipo Member de CSDL para poder navegar en modelos de datos de Business Intelligence.  
  
> [!WARNING]  
>  Este elemento se utiliza en la creación de informes y no se puede modificar ni manipular.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento NavigationProperty.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|CollectionCaption|No|Nombre plural para hacer referencia a un conjunto de instancias de la propiedad de navegación.<br /><br /> Si se omite este atributo, se utiliza el atributo Caption del miembro base.|  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente, se muestra una propiedad de navegación en la versión 1.1 de CSDLBI que describe el vínculo existente entre las tablas Product SubCategory y Product en un modelo tabular.  
  
```  
  
<NavigationProperty   
    Name="Product_Sub_Category_ProductSubcategoryKey"      
    Relationship="Sandbox.Product_Product_Sub_Category_Product_Sub_Category_ProductSubcategoryKey"  
     FromRole="Product_ProductSubcategoryKey"   
    ToRole="Product_Sub_Category_ProductSubcategoryKey">  
<bi:NavigationProperty   
     ReferenceName="Product Sub-Category_ProductSubcategoryKey" />  
</NavigationProperty>  
```  
  
## <a name="example"></a>Ejemplo  
 **Multidimensional**  
  
 En el ejemplo siguiente se muestra una propiedad de navegación en la versión 1.1 de CSDLBI que describe la relación entre dos tablas en el cubo de operaciones de Contoso. La relación conecta las tablas Bike Category y Product Subcategory.  
  
```  
  
<NavigationProperty   
     Name="BikeSubcategory_ProductSubcategoryKey"   
     Relationship="Sandbox.Bike_BikeSubcategory_BikeSubcategory_ProductSubcategoryKey"   
     FromRole="Bike_ProductSubcategoryKey"   
     ToRole="BikeSubcategory_ProductSubcategoryKey">  
   <bi:NavigationProperty />  
</NavigationProperty>  
```  
  
## <a name="see-also"></a>Vea también  
 [Descripción del modelo de objetos tabulares en compatibilidad 1050 1103 a través de niveles](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  

