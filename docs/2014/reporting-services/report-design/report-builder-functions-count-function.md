---
title: Función Count (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7b50b101-daf8-4fb0-ae04-57384755779f
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: e623374290e9620d048d651683a58bfcd3ddf573
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196883"
---
# <a name="count-function-report-builder-and-ssrs"></a>Función Count (Generador de informes y SSRS)
  Devuelve un recuento de los valores no NULL especificados por la expresión, que se evalúa en el contexto del ámbito indicado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Count(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *expression*  
 (`Variant` o `Binary`) expresión en la que se lleva a cabo la agregación, por ejemplo, `=Fields!FieldName.Value`.  
  
 *ámbito*  
 (`String`) El nombre de un conjunto de datos, grupo o región de datos que contiene el informe de elementos que se va a aplicar la función de agregado. Si no se especifica el parámetro *scope* , se usa el ámbito actual.  
  
 *recursivos*  
 (**Tipo enumerado**) Opcional. `Simple` (valor predeterminado) o `RdlRecursive`. Especifica si se debe realizar la agregación de forma recursiva.  
  
## <a name="return-type"></a>Tipo devuelto  
 Devuelve un `Integer`.  
  
## <a name="remarks"></a>Notas  
 El valor de *scope* debe ser una constante de cadena y no puede ser una expresión. Para los agregados exteriores o los que no especifican a otros agregados, *scope* debe hacer referencia al ámbito actual o a un ámbito de contenido. Para los agregados de agregados, los agregados anidados pueden especificar un ámbito secundario.  
  
 *Expression* puede contener las llamadas a las funciones de agregados anidados con las siguientes excepciones y condiciones:  
  
-   *Scope* , para los agregados anidados, debe ser igual que el ámbito del agregado exterior, o ser contenido por él. Para todos los ámbitos distintos de la expresión, un ámbito debe estar en una relación secundaria con respecto a todos los otros ámbitos.  
  
-   *Scope* , para los agregados anidados, no puede ser el nombre de un conjunto de datos.  
  
-   *Expresión* no debe contener `First`, `Last`, `Previous`, o `RunningValue` funciones.  
  
-   *Expression* no debe contener a los agregados anidados que especifican *recursive*.  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para más información sobre los agregados recursivos, vea [Crear un grupo de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
 Ejemplo  
  
## <a name="description"></a>Descripción  
 El ejemplo de código siguiente muestra una expresión que calcula el número de valores no NULL de `Size` para el ámbito predeterminado y para un ámbito de grupo primario. La expresión se agrega a una celda de una fila que pertenece al grupo secundario `GroupbySubcategory`. El grupo primario es `GroupbyCategory`. La expresión muestra los resultados para `GroupbySubcategory` (el ámbito predeterminado) y, después, para `GroupbyCategory` (el ámbito del grupo primario).  
  
> [!NOTE]  
>  Las expresiones no deben contener retornos de carro ni saltos de línea reales; en el ejemplo se han incluido para posibilitar la compatibilidad con los representadores de documentación. Si copia el ejemplo siguiente, quite los retornos de carro de todas las líneas.  
  
## <a name="code"></a>código  
  
```  
="Count (Subcategory): " & Count(Fields!Size.Value) &   
"Count (Category): " & Count(Fields!Size.Value,"GroupbyCategory")  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresión que se utiliza en los informes &#40;el generador de informes SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para totales, agregados y colecciones integradas &#40;el generador de informes SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  