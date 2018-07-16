---
title: Operadores de resúmenes personalizados en dimensiones de elementos primarios y secundarios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- child rollup operations
- UnaryOperatorColumn property
- custom rollup operators [Analysis Services]
- unary operators
- parent-child dimensions [Analysis Services]
ms.assetid: a3ddd9fc-5fa3-4227-9322-8c45a5b5c2c3
caps.latest.revision: 26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e6dcee2c6cb88e071d55c5cb1a7d6c131c31a5f9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37272011"
---
# <a name="custom-rollup-operators-in-parent-child-dimensions"></a>Operadores de resúmenes personalizados en dimensiones de elementos primarios y secundarios
  Los operadores de resúmenes personalizados constituyen una manera sencilla de controlar la forma en que los valores de los miembros se acumulan en los valores de sus elementos primarios en una jerarquía de elementos primarios y secundarios. En una dimensión que contiene una relación de elementos primarios y secundarios, se especifica una columna que contiene operadores unarios que especifican el resumen para todos los miembros no calculados del atributo primario. El operador unario se aplica a los miembros siempre que los valores de los miembros primarios se evalúan.  
  
 Los operadores unarios se almacenan en columnas definidas por la propiedad `UnaryOperatorColumn` del atributo primario y se aplican a cada miembro del atributo. La columna especificada por esta propiedad puede residir en la tabla de dimensiones o en una tabla relacionada con ella mediante una clave externa en la tabla de dimensiones.  
  
 Los operadores de resúmenes personalizados proporcionan una funcionalidad similar a la de fórmulas de miembro personalizado, pero simplificada. Una fórmula de miembro personalizado usa expresiones multidimensionales (MDX) para determinar la manera en que se acumulan los miembros. En comparación, un operador de resúmenes personalizados usa un operador unario simple para determinar la manera en que el valor de un miembro afecta al elemento primario. Las formulas de miembro personalizado del nivel precedente en una dimensión anulan al operador de resúmenes personalizados de un nivel.  
  
## <a name="custom-rollup-precedence"></a>Prioridad de los resúmenes personalizados  
 En términos de prioridad, los operadores de resúmenes personalizados del atributo de origen en un nivel de una jerarquía anulan las fórmulas de miembro personalizado del nivel anterior. Sin embargo, las fórmulas de miembro personalizado del nivel anterior anulan los operadores de resúmenes personalizados de un nivel.  
  
## <a name="see-also"></a>Vea también  
 [Definir fórmulas de miembro personalizado](attribute-properties-define-custom-member-formulas.md)   
 [Operadores unarios en dimensiones de elementos primarios y secundarios](parent-child-dimension-attributes-unary-operators.md)  
  
  
