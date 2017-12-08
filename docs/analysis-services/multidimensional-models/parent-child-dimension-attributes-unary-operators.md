---
title: Operadores unarios en dimensiones de elementos primarios y secundarios | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UnaryOperatorColumn property
- attributes [Analysis Services], unary operators
- unary operators
ms.assetid: b8ef549c-5458-458a-bf1a-fd743a1417fd
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4ceea7fc4a5d84d571a45c00f2e6291405544f3a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="parent-child-dimension-attributes---unary-operators"></a>Atributos de dimensión de elementos primarios y secundarios - operadores unarios
  En una dimensión que contiene una relación de elementos primarios y secundarios en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], se especifica una columna de operador unario (o de resumen personalizado) que determina el resumen personalizado para todos los miembros no calculados del atributo primario. El operador unario se aplica a los miembros siempre que los valores de los miembros primarios se evalúan. El elemento **UnaryOperatorColumn** en un atributo primario (**Uso**= Primario) especifica la columna de una tabla en la vista del origen de datos que contiene operadores unarios. Los valores para los operadores de resumen personalizado que se almacenan en esta columna se aplican a cada miembro del atributo.  
  
 Puede crear y especificar un cálculo con nombre en una tabla de dimensiones de la vista del origen de datos como una columna de operador unario. La expresión más simple, como '+', devuelve el mismo operador para todos los miembros. Pero se puede usar cualquier expresión siempre que devuelva un operador para cada miembro.  
  
 Puede cambiar el valor de la propiedad **UnaryOperatorColumn** de forma manual en un atributo primario o usar la mejora para definir agregaciones personalizadas del Asistente de Business Intelligence para reemplazar la agregación predeterminada asociada a los miembros de una dimensión. Para más información sobre el uso del Asistente de Business Intelligence para ejecutar esta configuración, vea [Agregar una agregación personalizada a una dimensión](../../analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension.md).  
  
 El valor predeterminado de la propiedad **UnaryOperatorColumn** en un atributo primario es (ninguno), que deshabilita los operadores de resumen personalizados. En la tabla siguiente se enumeran los operadores unarios disponibles y se describe su comportamiento cuando se aplican a un nivel.  
  
|Operador unario|Description|  
|--------------------|-----------------|  
|+ (signo más)|El valor del miembro se agrega al valor de agregado de los miembros iguales que ocurren antes del miembro. Éste es el operador predeterminado si no se define una columna de operador unario para un atributo.|  
|– (signo menos)|El valor del miembro se sustrae al valor de agregado de los miembros iguales que ocurren antes del miembro.|  
|* (asterisco)|El valor del miembro se multiplica por el valor de agregado de los miembros iguales que ocurren antes del miembro.|  
|/ (barra diagonal)|El valor del miembro se divide por el valor de agregado de los miembros iguales que ocurren antes del miembro.|  
|~ (tilde)|El valor del miembro se omite.|  
  
 Los valores en blanco y cualquier otro valor que no se encuentre en la tabla se tratan como el operador unario del signo más (+). Los operadores no tienen prioridad, de manera que el orden de los miembros tal como se almacenan en la columna de operadores unarios determina el orden de evaluación. Para cambiar el orden de evaluación, cree un nuevo atributo, establezca su propiedad **Type** en **Sequence**y asigne números de secuencia que correspondan al orden de evaluación en su propiedad **Source Column** . También debe ordenar miembros del atributo de acuerdo con este atributo. Para más información sobre la forma de usar el Asistente de Business Intelligence para ordenar miembros de un atributo, vea [Definir la ordenación en una dimensión](../../analysis-services/multidimensional-models/bi-wizard-define-the-ordering-for-a-dimension.md).  
  
 Puede usar la propiedad **UnaryOperatorColumn** para especificar un cálculo con nombre que devuelve un operador unario como un carácter literal para todos los miembros del atributo. Esto puede ser algo tan sencillo como escribir un carácter literal como `'*'` en el cálculo con nombre. Esto reemplaza el operador predeterminado, el signo más (+), con el operador de multiplicación, el asterisco (*), para todos los miembros del atributo. Para más información, vea [Definir cálculos con nombre en una vista del origen de datos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md).  
  
 En la pestaña **Explorador** del Diseñador de dimensiones, se pueden ver los operadores unarios junto a cada miembro en una jerarquía. También puede cambiar los operadores unarios al trabajar con una dimensión habilitada para escritura. Si la dimensión no está habilitada para escritura, debe usar una herramienta para modificar directamente el origen de datos.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de las propiedades de los atributos de dimensión](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)   
 [Operadores de resúmenes personalizados en dimensiones de elementos primarios y secundarios](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-custom-rollup-operators.md)   
 [Iniciar al Asistente de Business Intelligence en el Diseñador de dimensiones](../../analysis-services/multidimensional-models/database-dimensions-bi-wizard-in-dimension-designer.md)  
  
  
