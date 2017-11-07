---
title: AssociationSet, elemento (CSDLBI) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
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
ms.assetid: 93e5ac4d-d7e8-490e-b775-28263a48cfcc
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f8635a526095a7182c8415f571e26e6818f209a8
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="associationset-element-csdlbi"></a>AssociationSet, elemento (CSDLBI)
  El elemento **AssociationSet** es un tipo complejo que define una asociación. En un modelo de datos CSDLBI, una asociación es una relación entre dos tablas.  
  
 Se debe especificar un elemento **AssociationSet** para cada relación única de un modelo. El elemento **AssociationSet** define los extremos mediante el elemento **Association** . El elemento **AssociationSet** también define metadatos sobre la relación y su uso en el modelo de datos.  
  
## <a name="applicable-attributes"></a>Atributos aplicables  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento **AssociationSet** .  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|State|Sí|Cadena que indica si la asociación está activa o no. El valor lo define el elemento State.|  
|Oculto|No|Valor booleano que indica si la relación está visible. De forma predeterminada, el valor de Hidden es **false**, lo que significa que todas las relaciones están visibles en el modelo.|  
  
## <a name="state-element"></a>Elemento State  
 El elemento **State** es un tipo simple que indica si una asociación está activa y debe usarse en los cálculos, o si está inactiva y se debe hacer referencia explícita a ella en los cálculos.  
  
 Si hay varios conjuntos de asociaciones conectando las dos entidades, solo uno de ellos se puede marcar como activo. Es decir, si hay dos relaciones entre las mismas dos tablas, solo una relación puede estar activa.  
  
 En la tabla siguiente se enumeran los valores del elemento **State** .  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Activo|La asociación está activa.|  
|Inactivo|La asociación está activa.|  
  
## <a name="example"></a>Ejemplo  
 **Tabular**  
  
 En el ejemplo siguiente se muestra una relación en el modelo tabular AdventureWorks (en la versión 1.1 de CSDLBI). La asociación está marcada como inactiva, ya que hay una relación existente (entre OrderKey y Date).  
  
```  
<AssociationSet   
    Name="InternetSales_Date_Date_Date"  
    Association="Sandbox.InternetSales_Date_Date_Date">  
    <End EntitySet="InternetSales" />  
    <End EntitySet="DimDate" />  
<bi:AssociationSet State="Inactive" />  
</AssociationSet>  
  
```  
  
## <a name="example"></a>Ejemplo  
 **Multidimensional**  
  
 En el ejemplo siguiente se muestra la relación definida entre las tablas Sales y Currency, en el cubo de operaciones de Contoso.  
  
```  
<AssociationSet   
    Name ="Sales_Currency_Currency_Currency_Name2"  
    Association ="Sandbox.Sales_Currency_Currency_Currency_Name2">  
    <End EntitySet ="Sales" />  
    <End EntitySet ="Currency" />  
<bi:AssociationSet />  
</AssociationSet>  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia técnica de anotaciones de BI para CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  

