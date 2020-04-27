---
title: Editor de transformación columna derivada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- Derived Column Transformation Editor
ms.assetid: ff73923e-d245-43d8-bf24-af3bdc942e51
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4fc2701ad53cd0071be40100d168d5d5571d2958
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059567"
---
# <a name="derived-column-transformation-editor"></a>Columna derivada, editor de transformación
  Utilice el cuadro de diálogo **Editor de transformación Columna derivada** para crear expresiones que rellenan columnas nuevas o de reemplazo.  
  
 Para obtener más información acerca de la transformación Columna derivada, vea [Derived Column Transformation](data-flow/transformations/derived-column-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Variables y columnas**  
 Genere una expresión que utiliza una variable o una columna de entrada arrastrándolas de la lista de variables y columnas disponibles a una fila de tabla existente en el siguiente panel, o bien a una nueva fila al final de la lista.  
  
 **Funciones y operadores**  
 Genere una expresión que utiliza una función o un operador para evaluar los datos de entrada y los datos de salida directa arrastrando las funciones y operadores de la lista al siguiente panel.  
  
 **Nombre de columna derivada**  
 Especifique un nombre de columna derivada. De forma predeterminada, se muestra una lista numerada de columnas derivadas; no obstante, puede elegir un nombre único descriptivo.  
  
 **Columna derivada**  
 Seleccione una columna derivada de la lista. Elija si desea agregar la columna derivada como columna de salida nueva o reemplazar los datos de una columna existente.  
  
 **Expression**  
 Escriba una expresión o genere una arrastrando elementos de la lista anterior de columnas, variables, funciones y operadores disponibles.  
  
 Puede especificar el valor de esta propiedad con una expresión de propiedad.  
  
 **Temas relacionados**: [Expresiones de Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md), [Operadores &#40;expresión de SSIS&#41;](expressions/operators-ssis-expression.md) y [Funciones &#40;expresión de SSIS&#41](expressions/functions-ssis-expression.md).  
  
 **Tipo de datos**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** evalúa automáticamente la expresión y establece el tipo de datos según corresponda. El valor de esta columna es de solo lectura. Para obtener más información, vea [Integration Services tipos de datos](data-flow/integration-services-data-types.md).  
  
 **Longitud**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** evalúa automáticamente la expresión y establece la longitud de columna para los datos de cadena. El valor de esta columna es de solo lectura.  
  
 **Precisión**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** establece automáticamente la precisión de los datos numéricos según el tipo de datos. El valor de esta columna es de solo lectura.  
  
 **Escala**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** establece automáticamente la escala de los datos numéricos según el tipo de datos. El valor de esta columna es de solo lectura.  
  
 **Página de códigos**  
 Si agrega datos a una nueva columna, el cuadro de diálogo **Editor de transformación Columna derivada** establece automáticamente la página de códigos para el tipo de datos DT_STR. Puede actualizar la **Página de códigos**.  
  
 **Configurar la salida de errores**  
 Especifique cómo quiere controlar los errores mediante el cuadro de diálogo [Configurar la salida de errores](../../2014/integration-services/configure-error-output.md) .  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Derivar valores de columna mediante la transformación Columna derivada](data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
  
