---
title: NavigationProperty, elemento (CSDLBI) | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9db2facd93380fa3d0e011104bb95950e43340fb
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34038751"
---
# <a name="navigationproperty-element-csdlbi"></a>NavigationProperty, elemento (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 **Multidimensionales**  
  
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
  
  
