---
title: AssociationSet, elemento (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 93e5ac4d-d7e8-490e-b775-28263a48cfcc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7a7e165afc901b82d73f11f04fbb2c2cbb5402ac
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224895"
---
# <a name="associationset-element-csdlbi"></a>AssociationSet, elemento (CSDLBI)
  El elemento `AssociationSet` es un tipo complejo que define una asociación. En un modelo de datos CSDLBI, una asociación es una relación entre dos tablas.  
  
 Se debe especificar un elemento `AssociationSet` para cada relación única de un modelo. El elemento `AssociationSet` define los extremos mediante el elemento `Association`. El elemento `AssociationSet` también define metadatos sobre la relación y su uso en el modelo de datos.  
  
## <a name="applicable-attributes"></a>Atributos aplicables  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento `AssociationSet`.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|State|Sí|Cadena que indica si la asociación está activa o no. El valor lo define el elemento State.|  
|Hidden|no|Valor booleano que indica si la relación está visible. De forma predeterminada, el valor de Hidden es `false`, lo que significa que todas las relaciones están visibles en el modelo.|  
  
## <a name="state-element"></a>Elemento State  
 El elemento `State` es un tipo simple que indica si una asociación está activa y debe usarse en los cálculos, o si está inactiva y se debe hacer referencia explícita a ella en los cálculos.  
  
 Si hay varios conjuntos de asociaciones conectando las dos entidades, solo uno de ellos se puede marcar como activo. Es decir, si hay dos relaciones entre las mismas dos tablas, solo una relación puede estar activa.  
  
 En la tabla siguiente se enumeran los valores del elemento `State`.  
  
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
 [Referencia técnica para las anotaciones de Business Intelligence en CSDL](technical-reference-for-bi-annotations-to-csdl.md)  
  
  
