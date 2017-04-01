---
title: "Funci&#243;n Previous (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 403a9384-6ca4-42e8-97ca-ac3f6fe4316b
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Funci&#243;n Previous (Generador de informes y SSRS)
  Devuelve el valor o el valor agregado especificado para la instancia anterior de un elemento dentro del ámbito especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Sintaxis  
  
```  
  
Previous(expression, scope)  
```  
  
#### Parámetros  
 *expression*  
 (**Variant** o **Binary**). Expresión que se usa para identificar los datos cuyo valor anterior se quiere recuperar (por ejemplo, `Fields!Fieldname.Value` o `Sum(Fields!Fieldname.Value)`).  
  
 *ámbito*  
 (**String**) Opcional. Nombre de un grupo o una región de datos, o bien un valor NULL (**Nothing** en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), que especifica el ámbito para el que se recuperará el valor anterior especificado con *expression*.  
  
## Tipo devuelto  
 Devuelve un valor **Variant** o **Binary**.  
  
## Comentarios  
 La función **Previous** devuelve el valor anterior para la expresión evaluada en el ámbito especificado después de aplicar todos los filtros y la configuración de ordenación.  
  
 Si *expression* no contiene un agregado, la función **Previous** tiene como valor predeterminado el ámbito actual del elemento de informe.  
  
 En un grupo de detalles, utilice **Previous** para especificar el valor de una referencia de campo en la instancia anterior de la fila de detalles.  
  
> [!NOTE]  
>  La función **Previous** solo admite referencias de campo en el grupo de detalles. Por ejemplo, en un cuadro de texto del grupo de detalles, `=Previous(Fields!Quantity.Value)` devuelve los datos para el campo `Quantity` de la fila anterior. En la primera fila, esta expresión devuelve un valor NULL (**Nothing** en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]).  
  
 Si *expression* contiene una función de agregado que utiliza un ámbito predeterminado, **Previous** agrega los datos contenidos dentro de la instancia anterior del ámbito especificado en la llamada de la función de agregado.  
  
 Si *expression* contiene una función de agregado que especifica un ámbito distinto del predeterminado, el parámetro *scope* para la función **Previous** debe ser un ámbito contenedor para el ámbito especificado en la llamada a la función de agregado.  
  
 Las funciones **Level**, **InScope**, **Aggregate** y **Previous** no se pueden usar en el parámetro *expression*. No se admite especificar el parámetro *recursive* para ninguna función de agregado.  
  
 Para más información, vea [Referencia a las funciones de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md).  
  
## Ejemplos  
  
### Description  
 Cuando se coloca en la fila de datos predeterminada de una región de datos, el ejemplo de código siguiente proporciona el valor para el campo `LineTotal` de la fila anterior.  
  
### código  
  
```  
=Previous(Fields!LineTotal.Value)  
```  
  
### Description  
 En el ejemplo siguiente se muestra una expresión que calcula la suma de las ventas en un día concreto del mes y el valor anterior para ese día del mes del año anterior. La expresión se agrega a una celda de una fila que pertenece al grupo secundario `GroupbyDay`. Su grupo primario es `GroupbyMonth`, cuyo grupo primario es `GroupbyYear`. La expresión muestra los resultados para GroupbyDay (el ámbito predeterminado) y, a continuación, para `GroupbyYear` (el ámbito primario del grupo primario `GroupbyMonth`).  
  
 Por ejemplo, para una región de datos con un grupo primario denominado `Year`, su grupo secundario se denomina `Month` y su grupo secundario se denomina `Day` (3 niveles anidados). Si se sitúa la expresión `=Previous(Sum(Fields!Sales.Value,"Day"),"Year")` en una fila asociada al grupo `Day` , devuelve el valor de las ventas correspondiente al mismo día y mes del año anterior.  
  
### código  
  
```  
=Sum(Fields!Sales.Value) & " " & Previous(Sum(Fields!Sales.Value,"GroupbyDay"),"GroupbyYear")  
```  
  
## Vea también  
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md)  
  
  