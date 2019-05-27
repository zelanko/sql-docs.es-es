---
title: Agregar una agregación personalizada a una dimensión | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], Business Intelligence enhancements
- Business Intelligence enhancements [Analysis Services], custom aggregations
- aggregations [Analysis Services], custom
- unary operators
- custom aggregations [Analysis Services]
ms.assetid: 3199a6c2-a06d-47b9-bd1c-604dbb085318
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e647b32d8f94ebd545a9d8d85d066a25dde6e77c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66076909"
---
# <a name="add-a-custom-aggregation-to-a-dimension"></a>Agregar una agregación personalizada a una dimensión
  Agregue una mejora de agregación personalizada a un cubo o dimensión para reemplazar las agregaciones predeterminadas asociadas a un miembro de dimensión con un operador unario diferente. Esta mejora especifica una columna de operador unario en la tabla de dimensión que define el resumen de los miembros de una jerarquía de elementos primarios y secundarios. El operador unario actúa sobre el atributo primario en una jerarquía de elementos primarios y secundarios.  
  
> [!NOTE]  
>  Una agregación personalizada solo está disponible en dimensiones basadas en los orígenes de datos existentes. En las dimensiones que se crearon sin utilizar un origen de datos, debe ejecutar el Asistente para generar esquemas para crear una vista del origen de datos antes de agregar la agregación personalizada.  
  
 Para agregar una agregación personalizada, debe utilizar el Asistente de Business Intelligence y seleccionar la opción **Especificar un operador unario** en la página **Elegir mejora** . Este asistente le indica los pasos necesarios para seleccionar la dimensión en la que desea aplicar una agregación personalizada e identificar la agregación personalizada.  
  
> [!NOTE]  
>  Antes de ejecutar el Asistente de Business Intelligence para agregar una agregación personalizada, compruebe que la dimensión que desea mejorar contiene una jerarquía de atributos primarios y secundarios. Para obtener más información, consulte [jerarquía de elementos primarios y secundarios](parent-child-dimension.md).  
  
## <a name="selecting-a-dimension"></a>Seleccionar una dimensión  
 En la primera página **Especificar un operador unario** del asistente, debe especificar la dimensión en la que desea aplicar una agregación personalizada. La agregación personalizada agregada a la dimensión seleccionada provocará cambios en la dimensión. Estos cambios son heredados por todos los cubos que incluyan la dimensión seleccionada.  
  
## <a name="adding-custom-aggregation-unary-operator"></a>Agregar agregación personalizada (operador unario)  
 En la segunda página de **Especificar un operador unario** , debe especificar el atributo primario que desea para la agregación personalizada y la columna de origen en la tabla de dimensión para el operador unario. **Atributo primario** se enumeran los atributos que tienen sus `Usage` propiedad establecida en `Parent`. Si hay más de un atributo primario, debe elegir el atributo primario que corresponda a la relación de elementos primarios y secundarios que desee utilizar. Si no se muestran atributos primarios, la dimensión no contiene una jerarquía de elementos primarios y secundarios válida.  
  
 En **Columna de origen**, debe seleccionar la columna de cadenas que contiene los operadores unarios. (Esta selección establece la `UnaryOperatorColumn` propiedad del atributo primario.) La tabla de dimensión también debe presentar una columna de cadenas que especifique el operador unario de resumen. Los valores de cadenas de esta columna deben contener operadores de agregación válidos. Si una fila está vacía, el miembro correspondiente se calcula de la forma habitual. Si la fórmula de una columna no es válida, se producirá un error en tiempo de ejecución al recuperar un valor de celda que utiliza el miembro. Para obtener más información, vea [Operadores unarios en dimensiones de elementos primarios y secundarios](parent-child-dimension-attributes-unary-operators.md).  
  
  
