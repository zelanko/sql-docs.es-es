---
title: Cuadro de diálogo Expresión (generador de informes) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10040"
helpviewer_keywords:
- expressions
ms.assetid: e89c4d97-5d41-4b55-8695-79329edac15d
caps.latest.revision: 16
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 9625b461128b1aa9785edbe92b4defa47e85bc55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198847"
---
# <a name="expression-dialog-box-report-builder"></a>Expresión (cuadro de diálogo del Generador de informes)
  Use la **expresión** cuadro de diálogo para escribir [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] expresiones para informe de propiedades de los elementos. Puede usar expresiones para establecer muchas propiedades, como el color, la fuente y los bordes. En tiempo de ejecución, el procesador de informes evalúa las expresiones y usa el resultado como valor de la propiedad.  
  
 El cuadro de diálogo **Expresión** incluye una ventana de código, un árbol de categorías, elementos de categoría, un panel de descripción y un panel de ejemplo. El cuadro de diálogo **Expresión** depende del contexto; los elementos de categoría y las descripciones cambian en respuesta a la categoría de expresiones con la que se está trabajando. Para obtener más información, consulte [ejemplos de expresiones &#40;el generador de informes y SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md), [expresiones &#40;el generador de informes y SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
## <a name="expression-constructs"></a>Construcciones de expresiones  
 Las expresiones comienzan por un signo igual (=) y pueden incluir constantes, literales, operadores y referencias a campos integrados, colecciones integradas, funciones integradas, funciones de la biblioteca en tiempo de ejecución de [!INCLUDE[vbprvb](../includes/vbprvb-md.md)], clases de Common Language Runtime de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] y funciones personalizadas. En la lista siguiente se describen las categorías y los valores que puede agregar a una expresión.  
  
 **Establecer expresión para:***\<PropertyName >*   
 Nombre de la propiedad cuya expresión está definiendo. También puede establecer esta propiedad, por nombre, en el panel de propiedades.  
  
 **Constantes**  
 Proporciona una lista de valores predefinidos válidos para esta propiedad (para las propiedades que están basadas en constantes). Por ejemplo, una propiedad basada en colores muestra los nombres de los colores válidos. Para una propiedad que es un tipo de datos Boolean, los valores son `True` y `False`.  
  
 No todos los elementos que admiten expresiones pueden establecerse en una constante. Si una propiedad no se puede establecer en un valor constante, el panel de descripciones proporciona esta información.  
  
 **Campos integrados**  
 Proporciona una lista de los elementos de la colección global que puede utilizar en una expresión. Algunas colecciones solo se admiten una vez publicado el informe en el servidor. Para obtener más información, vea [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md).  
  
 **Parámetros**  
 Proporciona una lista de parámetros de informe.  
  
 **Campos (**  *\<conjunto de datos seleccionado >* **)**  
 Muestra la lista de campos para el conjunto de datos seleccionado en la categoría Conjuntos de datos. Haga doble clic en un campo para copiarlo en el cuadro **Expresión** .  
  
 **Conjuntos de datos**  
 Proporciona una lista de conjuntos de datos disponibles y muestra los campos miembros del conjunto de datos.  
  
 **Variables**  
 Muestra una lista de variables de informe. Para más información, vea [Referencias a las colecciones de variables de informe y de grupo &#40;Generador de informes y SSRS&#41;](report-design/built-in-collections-report-and-group-variables-references-report-builder.md).  
  
 **Operadores**  
 Muestra los operadores que puede incluir en un cálculo o manipulación de cadena. Para obtener más información, vea [Usar operadores en expresiones &#40;Generador de informes y SSRS&#41;](report-design/operators-in-expressions-report-builder-and-ssrs.md).  
  
 **Funciones comunes**  
 Muestra funciones comunes, agrupadas por tipos. Al seleccionar una función en el panel Elemento, aparecen una descripción y un ejemplo.  
  
 Entre las funciones comunes se incluyen funciones integradas de informe y de agregado, funciones de la biblioteca en tiempo de ejecución de [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] y clases de Common Language Runtime (CLR) de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] en los espacios de nombres <xref:System.Math> y <xref:System.Convert>. También puede agregar referencias a clases de CLR y ensamblados externos que no aparecen en la lista de categorías. Para obtener más información, vea [Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
## <a name="options"></a>Opciones  
 Ventana de código  
 Utilice la ventana de código del panel superior para escribir una expresión. Cuando se abre el cuadro de diálogo **Expresión** , la ventana de código contiene la expresión. Puede reemplazar o revisar la expresión. Puede agregar llamadas a funciones, operadores, constantes, campos, parámetros, elementos de las colecciones globales y referencias a código personalizado. La ventana de código muestra los cambios a medida que se realizan.  
  
 Los subrayados ondulados en rojo indican un error de sintaxis. Mantenga el mouse sobre el texto subrayado para ver el mensaje de error.  
  
 Si escribe elementos de las colecciones globales seguidos por un separador de puntuación, verá una lista desplegable de los miembros o las propiedades disponibles. En la lista desplegable, puede escribir los primeros caracteres seguidos de un tabulador para rellenar la selección automáticamente.  
  
 Al escribir un nombre de función seguido por un paréntesis izquierdo, verá una información sobre herramientas que proporciona información sobre los parámetros y valores devueltos por la función.  
  
 **Categoría**  
 Muestra categorías de expresiones. Si se elige una categoría, se establece un contexto para crear una expresión y se cambia la lista de valores válidos en el panel Elemento. Por ejemplo, para una expresión para un valor de cuadro de texto, expanda funciones comunes y seleccione funciones de agregado para mostrar `Avg`, `Count`y otras funciones en el **elemento** panel.  
  
 **Elemento**  
 Muestra la lista de valores válidos para la categoría seleccionada. Haga doble clic en un elemento para agregar el texto de la expresión para este elemento en el punto de inserción en la ventana de código.  
  
 **Valores**  
 En función de la categoría y el elemento que seleccione, el tercer panel contiene una descripción, una expresión de ejemplo o una lista de valores válidos. Arrastre el borde del cuadro de diálogo para ampliar el área de ejemplo.  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40;Generador de informes y SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [Aplicar formato a los elementos de informe &#40;Generador de informes y SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Aplicar formato a números y fechas &#40;el generador de informes SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Usar referencias a la colección de parámetros &#40;generador de informes y SSRS&#41;](report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [Ejemplos de expresión de grupo &#40;Generador de informes y SSRS&#41;](report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [Ejemplos de ecuaciones de filtro &#40;el generador de informes SSRS&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [Referencias a la colección de campos de conjunto de datos &#40;el generador de informes SSRS&#41;](report-design/built-in-collections-dataset-fields-collection-references-report-builder.md)   
 [Referencia a las funciones de agregado &#40;el generador de informes SSRS&#41;](report-design/report-builder-functions-aggregate-functions-reference.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Seleccione el cuadro de diálogo Color &#40;el generador de informes SSRS&#41;](../../2014/reporting-services/select-color-dialog-box-report-builder-and-ssrs.md)  
  
  