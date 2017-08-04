---
title: "Derivado de Editor de transformación de columna | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- Derived Column Transformation Editor
ms.assetid: ff73923e-d245-43d8-bf24-af3bdc942e51
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 89b764a8ea3d4e60852092ef502eb82adcf77c91
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="derived-column-transformation-editor"></a>Columna derivada, editor de transformación
  Utilice el cuadro de diálogo **Editor de transformación Columna derivada** para crear expresiones que rellenan columnas nuevas o de reemplazo.  
  
 Para obtener más información acerca de la transformación Columna derivada, vea [Derived Column Transformation](../../../integration-services/data-flow/transformations/derived-column-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Variables y columnas**  
 Genere una expresión que utiliza una variable o una columna de entrada arrastrándolas de la lista de variables y columnas disponibles a una fila de tabla existente en el siguiente panel, o bien a una nueva fila al final de la lista.  
  
 **Funciones y operadores**  
 Genere una expresión que utiliza una función o un operador para evaluar los datos de entrada y los datos de salida directa arrastrando las funciones y operadores de la lista al siguiente panel.  
  
 **Nombre de columna derivada**  
 Especifique un nombre de columna derivada. De forma predeterminada, se muestra una lista numerada de columnas derivadas; no obstante, puede elegir un nombre único descriptivo.  
  
 **Columna derivada**  
 Seleccione una columna derivada de la lista. Elija si desea agregar la columna derivada como columna de salida nueva o reemplazar los datos de una columna existente.  
  
 **Expresión**  
 Escriba una expresión o genere una arrastrando elementos de la lista anterior de columnas, variables, funciones y operadores disponibles.  
  
 Puede especificar el valor de esta propiedad con una expresión de propiedad.  
  
 **Temas relacionados**: [Expresiones de Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Operadores &#40;expresión de SSIS&#41;](../../../integration-services/expressions/operators-ssis-expression.md) y [Funciones &#40;expresión de SSIS&#41](../../../integration-services/expressions/functions-ssis-expression.md).  
  
 **Tipo de datos**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** evalúa automáticamente la expresión y establece el tipo de datos según corresponda. El valor de esta columna es de solo lectura. Para más información, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 **Longitud**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** evalúa automáticamente la expresión y establece la longitud de columna para los datos de cadena. El valor de esta columna es de solo lectura.  
  
 **Precisión**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** establece automáticamente la precisión de los datos numéricos según el tipo de datos. El valor de esta columna es de solo lectura.  
  
 **Escala**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** establece automáticamente la escala de los datos numéricos según el tipo de datos. El valor de esta columna es de solo lectura.  
  
 **Página de códigos**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** establece automáticamente la página de códigos para el tipo de datos DT_STR. Puede actualizar la **Página de códigos**.  
  
 **Configurar la salida de errores**  
 Especifique cómo quiere controlar los errores mediante el cuadro de diálogo [Configurar la salida de errores](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) .  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Derivar valores de columna mediante la transformación Columna derivada](../../../integration-services/data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
  
