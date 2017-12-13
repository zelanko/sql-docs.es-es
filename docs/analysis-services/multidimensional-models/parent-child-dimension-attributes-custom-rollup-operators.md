---
title: "Operadores de resúmenes personalizados en dimensiones de elementos primarios y secundarios | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- child rollup operations
- UnaryOperatorColumn property
- custom rollup operators [Analysis Services]
- unary operators
- parent-child dimensions [Analysis Services]
ms.assetid: a3ddd9fc-5fa3-4227-9322-8c45a5b5c2c3
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bf4f123a7c2026fde28f9556957de20905330741
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="parent-child-dimension-attributes---custom-rollup-operators"></a>Atributos de dimensión de elementos primarios y secundarios: operadores de resúmenes personalizados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Operadores de resúmenes personalizados proporcionan una manera sencilla de controlar cómo se acumulan los valores de miembro en los valores de elemento primario en una jerarquía de elementos primarios y secundarios. En una dimensión que contiene una relación de elementos primarios y secundarios, se especifica una columna que contiene operadores unarios que especifican el resumen para todos los miembros no calculados del atributo primario. El operador unario se aplica a los miembros siempre que los valores de los miembros primarios se evalúan.  
  
 Los operadores unarios se almacenan en columnas definidas por la propiedad **UnaryOperatorColumn** del atributo primario y se aplican a cada miembro del atributo. La columna especificada por esta propiedad puede residir en la tabla de dimensiones o en una tabla relacionada con ella mediante una clave externa en la tabla de dimensiones.  
  
 Los operadores de resúmenes personalizados proporcionan una funcionalidad similar a la de fórmulas de miembro personalizado, pero simplificada. Una fórmula de miembro personalizado usa expresiones multidimensionales (MDX) para determinar la manera en que se acumulan los miembros. En comparación, un operador de resúmenes personalizados usa un operador unario simple para determinar la manera en que el valor de un miembro afecta al elemento primario. Las formulas de miembro personalizado del nivel precedente en una dimensión anulan al operador de resúmenes personalizados de un nivel.  
  
## <a name="custom-rollup-precedence"></a>Prioridad de los resúmenes personalizados  
 En términos de prioridad, los operadores de resúmenes personalizados del atributo de origen en un nivel de una jerarquía anulan las fórmulas de miembro personalizado del nivel anterior. Sin embargo, las fórmulas de miembro personalizado del nivel anterior anulan los operadores de resúmenes personalizados de un nivel.  
  
## <a name="see-also"></a>Vea también  
 [Definir fórmulas de miembro personalizado](../../analysis-services/multidimensional-models/attribute-properties-define-custom-member-formulas.md)   
 [Operadores unarios en dimensiones de elementos primarios y secundarios](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-unary-operators.md)  
  
  
