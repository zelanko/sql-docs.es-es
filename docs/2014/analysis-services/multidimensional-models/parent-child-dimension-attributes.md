---
title: Atributos en jerarquías de elementos primarios y secundarios | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data members [Analysis Services]
- nonleaf members
- MembersWithDataCaption property
- members [Analysis Services]
- members [Analysis Services], data
- leaf members
- parent-child dimensions [Analysis Services]
- MembersWithData property
ms.assetid: 249971cc-4bcd-44f1-8241-bdacc04d3d38
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bbf5919d44a4e36e1bdddaf5c34c5e3ab6aa4315
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220287"
---
# <a name="attributes-in-parent-child-hierarchies"></a>Atributos en las jerarquías de elementos primarios y secundarios
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], se realiza normalmente una suposición general sobre el contenido de los miembros de una dimensión. Los miembros hoja contienen datos derivados directamente de los orígenes de datos subyacentes; los miembros no hoja contienen datos derivados de agregaciones realizadas en miembros secundarios.  
  
 No obstante, en una jerarquía de elementos primarios y secundarios, algunos miembros no hoja también pueden tener datos derivados de orígenes de datos subyacentes, además de los datos agregados de miembros secundarios. Para estos miembros no hoja de una jerarquía de elementos primarios y secundarios, se pueden crear miembros secundarios especiales generados por el sistema que contengan los datos de la tabla de hechos subyacente. Denominados *miembros de datos*, contienen un valor asociado directamente a un miembro no hoja que es independiente del valor de resumen calculado a partir de los descendientes del miembro no hoja.  
  
 Los miembros de datos se encuentran disponibles solo en dimensiones con jerarquías de elementos primarios y secundarios, y solo son visibles si lo tienen permitido por su atributo primario. Se puede utilizar el Diseñador de dimensiones para controlar la visibilidad de los miembros de datos. Para exponer los miembros de datos, establezca el `MembersWithData` propiedad del atributo primario para `NonLeafDataVisible.` para ocultar los miembros de datos contenidos en el atributo primario, establezca el `MembersWithData` propiedad del atributo primario en `NonLeafDataHidden`.  
  
 Este valor no reemplaza el comportamiento de agregación normal para los miembros no hoja; el miembro de datos siempre se incluye como miembro secundario para fines de agregación. Sin embargo, se puede utilizar una fórmula de resumen personalizado para reemplazar el comportamiento normal de agregación. Expresiones multidimensionales (MDX) [DataMember](/sql/mdx/datamember-mdx) función le permite tener acceso al valor del miembro de datos asociado independientemente del valor de la `MembersWithData` propiedad.  
  
 El `MembersWithDataCaption` proporciona la propiedad del atributo primario [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] con la plantilla de nomenclatura usada para generar nombres de miembro para miembros de datos.  
  
## <a name="using-data-members"></a>Usar miembros de datos  
 Los miembros de datos son de utilidad al agregar medidas a dimensiones organizativas que tienen jerarquías de elementos primarios y secundarios. Por ejemplo, en el diagrama siguiente se muestra una dimensión con tres niveles que representa el volumen de ventas brutas de productos. El primer nivel muestra el volumen de ventas brutas de todos los agentes de ventas. El segundo nivel contiene el volumen de ventas brutas de todo el personal de ventas por director de ventas y el tercer nivel contiene el volumen de ventas brutas de todo el personal de ventas por vendedor.  
  
 ![Dimensión del volumen de ventas brutas con tres niveles](../media/agdatamember1.gif "dimensión del volumen de ventas brutas con tres niveles")  
  
 Habitualmente, el valor del miembro Sales Manager 1 se deriva al agregar los valores de los miembros Salesperson 1 y Salesperson 2. Sin embargo, como Sales Manager 1 también puede vender productos, este miembro también puede contener datos derivados de la tabla de hechos, ya que puede haber ventas brutas asociadas a Sales Manager 1.  
  
 Además, la comisión individual de cada miembro del personal de ventas puede variar. En este caso, se utilizan dos escalas diferentes para calcular la comisión de las ventas brutas individuales de los directores de ventas, frente a las ventas brutas totales generadas por sus vendedores. Por lo tanto, es importante que los miembros no hoja puedan tener acceso a los datos de la tabla de hechos subyacente. El código MDX `DataMember` función puede utilizarse para recuperar el volumen ventas brutas del miembro Sales Manager 1 y una expresión de resumen personalizado puede utilizarse para excluir el miembro de datos desde el valor agregado del miembro Sales Manager 1, que proporciona el bruto volumen de ventas de los vendedores asociados a ese miembro.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de propiedades de atributos de dimensión](dimension-attribute-properties-reference.md)   
 [Jerarquía de elementos primarios y secundarios](parent-child-dimension.md)  
  
  
