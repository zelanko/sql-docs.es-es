---
title: NavigationProperty, elemento (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: a36b4d3b-6a6c-489b-8a46-2e6b925b568f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fbb0d38a4bcab7592893aaa63acb1bbb96dac5c3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157585"
---
# <a name="navigationproperty-element-csdlbi"></a>NavigationProperty, elemento (CSDLBI)
  El elemento NavigationProperty es un tipo complejo que extiende el tipo Member de CSDL para poder navegar en modelos de datos de Business Intelligence.  
  
> [!WARNING]  
>  Este elemento se utiliza en la creación de informes y no se puede modificar ni manipular.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento NavigationProperty.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|CollectionCaption|no|Nombre plural para hacer referencia a un conjunto de instancias de la propiedad de navegación.<br /><br /> Si se omite este atributo, se utiliza el atributo Caption del miembro base.|  
  
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
 [Descripción del modelo de objetos tabulares](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
