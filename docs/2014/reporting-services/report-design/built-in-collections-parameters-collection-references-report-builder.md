---
title: Referencias a la colección de parámetros (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c4b47e15-0484-4c13-9182-898db825f01f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c3c9452a9be55c71431a0ed3012769b1f5f6d8eb
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106412"
---
# <a name="parameters-collection-references-report-builder-and-ssrs"></a>Usar referencias a la colección de parámetros (Generador de informes y SSRS)
  Los parámetros de informe son una de las colecciones integradas a las que se puede hacer referencia desde una expresión. Al incluir parámetros en una expresión, puede personalizar los datos y el aspecto de los informes basándose en las opciones seleccionadas por el usuario. Se pueden usar expresiones para cualquier propiedad de elemento de informe o de cuadro de texto que proporcione la opción (*Fx*) o \<**Expresión**>. Las expresiones también se usan para controlar el contenido y el aspecto de los informes de otras maneras. Para más información, vea [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md).  
  
 Cuando se comparan los valores de los parámetros en tiempo de ejecución con los valores de los campos del conjunto de datos, los tipos de datos de los dos elementos que se comparan deben coincidir. Los parámetros de informe pueden tener uno de los siguientes tipos: Boolean, DateTime, Integer, Float o Text, que representa el tipo de datos subyacente String. Es posible que tenga que convertir el tipo de datos del valor del parámetro para que coincida con el valor del conjunto de datos. Para obtener más información, vea [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
 Para incluir una referencia de parámetro en una expresión, debe entender cómo especificar la sintaxis correcta para la referencia de parámetro, que varía dependiendo de si el parámetro es de un solo valor o de varios valores.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Single"></a> Usar un parámetro de un solo valor en una expresión  
 En la tabla siguiente se muestran ejemplos de la sintaxis que se debe usar cuando se incluye una referencia a un parámetro de un solo valor de cualquier tipo de datos en una expresión.  
  
|Ejemplo|Descripción|  
|-------------|-----------------|  
|`=Parameters!` *\<NombreDeParámetro>* `.IsMultiValue`|Devuelve `False`.<br /><br /> Comprueba si un parámetro es de varios valores. Si `True`, el parámetro es de varios valores y es una colección de objetos. Si `False`, el parámetro es de valor único y es un objeto único.|  
|`=Parameters!` *\<NombreDeParámetro>* `.Count`|Devuelve el valor entero 1. Para un parámetro de un solo valor, el recuento es siempre 1.|  
|`=Parameters!` *\<NombreDeParámetro>* `.Label`|Devuelve la etiqueta del parámetro, se suele utilizar como nombre para mostrar de una lista desplegable de valores disponibles.|  
|`=Parameters!` *\<NombreDeParámetro>* `.Value`|Devuelve el valor del parámetro. Si no se ha establecido la propiedad Label, este valor aparece en la lista desplegable de valores disponibles.|  
|`=CStr(Parameters!`  *\<NombreDeParámetro>* `.Value)`|Devuelve el valor del parámetro como una cadena.|  
|`=Fields(Parameters!` *\<NombreDeParámetro>* `.Value).Value`|Devuelve el valor del campo que tiene el mismo nombre que el parámetro.|  
  
 Para obtener más información sobre cómo usar parámetros en los filtros, vea [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md).  
  
##  <a name="Multi"></a> Usar un parámetro de varios valores en una expresión  
 En la tabla siguiente se muestran ejemplos de la sintaxis que se debe usar cuando se incluye una referencia a un parámetro de varios valores de cualquier tipo de datos en una expresión.  
  
|Ejemplo|Descripción|  
|-------------|-----------------|  
|`=Parameters!` *\<NombreDeParámetroConVariosValores>* `.IsMultiValue`|Devuelve `True` o `False`.<br /><br /> Comprueba si un parámetro es de varios valores. Si el valor es `True`, el parámetro es de varios valores y es una colección de objetos. Si el valor es `False`, el parámetro es de un solo valor y es un solo objeto.|  
|`=Parameters!` *\<NombreDeParámetroConVariosValores>* `.Count`|Devuelve un valor entero.<br /><br /> Se refiere al número de valores. Para un parámetro de un solo valor, el recuento es siempre 1. Para un parámetro de varios valores, el recuento es 0 o más.|  
|`=Parameters!` *\<NombreDeParámetroConVariosValores>* `.Value(0)`|Devuelve el primer valor de un parámetro de varios valores.|  
|`=Parameters!` *\<NombreDeParámetroConVariosValores>* `.Value(Parameters!` *\<NombreDeParámetroConVariosValores>* `.Count-1)`|Devuelve el último valor de un parámetro de varios valores.|  
|`=Split("Value1,Value2,Value3",",")`|Devuelve una matriz de valores.<br /><br /> Cree una matriz de valores para un parámetro de varios valores de tipo `String`. Puede utilizar cualquier delimitador del segundo parámetro para Split. Esta expresión puede utilizarse para establecer valores predeterminados para un parámetro de varios valores o para crear un parámetro de varios valores que se enviará a un subinforme o a un informe detallado.|  
|`=Join(Parameters!` *\<NombreDeParámetroConVariosValores>* `.Value,", ")`|Devuelve un valor de tipo `String` formado por una lista de valores delimitada por comas en un parámetro de varios valores. Puede utilizar cualquier delimitador del segundo parámetro para Join.|  
  
 Para más información sobre cómo usar parámetros en los filtros, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](report-parameters-report-builder-and-report-designer.md).  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Filtros de uso frecuente &#40;Generador de informes y SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md)   
 [Agregar, cambiar o eliminar parámetros de informe &#40;Generador de informes y SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Tutorial: Agregar un parámetro a un informe &#40;Generador de informes&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Tutoriales &#40;generador de informes&#41;](../report-builder-tutorials.md)   
 [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](built-in-collections-in-expressions-report-builder.md)  
  
  
