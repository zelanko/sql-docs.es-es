---
title: DisplayKey, elemento (CSDLBI) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
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
applies_to:
- SQL Server 2016 Preview
ms.assetid: 7d881278-1e77-42e1-8cfc-f1bbd9ec2340
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 10f388c46f9d79314107eb375aa4de6dacdf4fbf
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="displaykey-element-csdlbi"></a>DisplayKey, elemento (CSDLBI)
  El elemento DisplayKey contiene una lista de los elementos siguientes que constituyen en conjunto un identificador seguro. DisplayKey se encuentra solamente como elemento secundario del elemento EntityType. Puede hacer referencia a columnas o a extremos de rol.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los atributos del elemento DisplayKey.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|IsDisplayKey|No|True o false.|  
  
## <a name="remarks"></a>Comentarios  
 Este elemento se utiliza en los informes. El elemento al que se aplica este atributo no tiene por qué ser la clave de tabla real, sino solo un elemento que se presentará como tal. Sin embargo, la columna que utilice para DisplayKey debe incluir valores únicos.  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestra una columna del modelo de datos de ejemplo AdventureWorks que se ha designado como el elemento DisplayKey de la tabla.  
  
```  
<sample in progress>  
```  
  
## <a name="example"></a>Ejemplo  
 **Multidimensional**  
  
 En el ejemplo siguiente, en la versión 1.1 de CSDLBI, se muestra un extracto de la representación del cubo de operaciones de Contoso. En este modelo, se ha marcado la columna Color como la clave para mostrar de la tabla Bikes.  
  
```  
  
<EntityType   
    Name="Bike">  
.. .. ..  
<Property   
    Name="Color"   
    Type="String"   
    MaxLength="Max"   
    Unicode="true"   
    FixedLength="false">  
<bi:Property   
    ContextualNameRule="Context"   
    Alignment="Left" Units="counts"   
    SortDirection="Descending"   
    IsRightToLeft="true"   
    DefaultAggregateFunction="Max" />  
</Property>  
.. .. ..  
<bi:EntityType>  
   <bi:DisplayKey>  
      <bi:MemberRef Name="Color" />  
   </bi:DisplayKey>>  
.. .. ..  
</bi:EntityType>  
</EntityType>  
```  
  
## <a name="see-also"></a>Vea también  
 [Descripción del modelo de objetos tabulares en compatibilidad 1050 1103 a través de niveles](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [Conceptos de CSDLBI](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdlbi-concepts.md)  
  
  

