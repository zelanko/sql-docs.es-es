---
title: Función Previous (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 403a9384-6ca4-42e8-97ca-ac3f6fe4316b
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 65f8f0bdc7db2e58efd27522a93e4edf6c4e0bf3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198618"
---
# <a name="previous-function-report-builder-and-ssrs"></a>Función Previous (Generador de informes y SSRS)
  Devuelve el valor o el valor agregado especificado para la instancia anterior de un elemento dentro del ámbito especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Previous(expression, scope)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *expression*  
 (`Variant` o `Binary`) la expresión que se usará para identificar los datos y para el que se va a recuperar el valor anterior, por ejemplo, `Fields!Fieldname.Value` o `Sum(Fields!Fieldname.Value)`.  
  
 *ámbito*  
 (`String`) Opcional. El nombre de un grupo o región de datos o null (`Nothing` en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), que especifica el ámbito de la que se va a recuperar el valor anterior especificado por *expresión*.  
  
## <a name="return-type"></a>Tipo devuelto  
 Devuelve un `Variant` o `Binary`.  
  
## <a name="remarks"></a>Notas  
 La función `Previous` devuelve el valor anterior para la expresión evaluada en el ámbito especificado después de aplicar todos los filtros y la configuración de ordenación.  
  
 Si *expresión* no contiene un agregado, el `Previous` función tiene como valor predeterminado el ámbito actual del elemento de informe.  
  
 En un grupo de detalles, utilice `Previous` para especificar el valor de una referencia de campo en la instancia anterior de la fila de detalles.  
  
> [!NOTE]  
>  El `Previous` función solo admite referencias de campo en el grupo de detalles. Por ejemplo, en un cuadro de texto del grupo de detalles, `=Previous(Fields!Quantity.Value)` devuelve los datos para el campo `Quantity` de la fila anterior. En la primera fila, esta expresión devuelve NULL (`Nothing` en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]).  
  
 Si *expresión* contiene una función de agregado que utiliza un ámbito predeterminado, `Previous` agrega los datos dentro de la instancia anterior del ámbito especificado en la función llamada agregado.  
  
 Si *expresión* contiene una función de agregado que especifica un ámbito distinto del predeterminado, el *ámbito* parámetro para el `Previous` función debe ser un ámbito contenedor para el ámbito especificado en la llamada de función de agregado.  
  
 Las funciones `Level`, `InScope`, `Aggregate` y `Previous` no se puede usar en el *expresión*parámetro. No se admite especificar el parámetro *recursive* para ninguna función de agregado.  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="description"></a>Descripción  
 Cuando se coloca en la fila de datos predeterminada de una región de datos, el ejemplo de código siguiente proporciona el valor para el campo `LineTotal` de la fila anterior.  
  
### <a name="code"></a>código  
  
```  
=Previous(Fields!LineTotal.Value)  
```  
  
### <a name="description"></a>Descripción  
 En el ejemplo siguiente se muestra una expresión que calcula la suma de las ventas en un día concreto del mes y el valor anterior para ese día del mes del año anterior. La expresión se agrega a una celda de una fila que pertenece al grupo secundario `GroupbyDay`. Su grupo primario es `GroupbyMonth`, cuyo grupo primario es `GroupbyYear`. La expresión muestra los resultados para GroupbyDay (el ámbito predeterminado) y, a continuación, para `GroupbyYear` (el ámbito primario del grupo primario `GroupbyMonth`).  
  
 Por ejemplo, para una región de datos con un grupo primario denominado `Year`, su grupo secundario se denomina `Month`y su grupo secundario se denomina `Day` (3 niveles anidados). Si se sitúa la expresión `=Previous(Sum(Fields!Sales.Value,"Day"),"Year")` en una fila asociada al grupo `Day` , devuelve el valor de las ventas correspondiente al mismo día y mes del año anterior.  
  
### <a name="code"></a>código  
  
```  
=Sum(Fields!Sales.Value) & " " & Previous(Sum(Fields!Sales.Value,"GroupbyDay"),"GroupbyYear")  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresión que se utiliza en los informes &#40;el generador de informes SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para totales, agregados y colecciones integradas &#40;el generador de informes SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  