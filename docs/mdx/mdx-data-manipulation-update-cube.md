---
description: 'Manipulación de datos de MDX: UPDATE CUBE'
title: UPDATE CUBE (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 142783612b495d7968fec1574e182654ac83fb64
ms.sourcegitcommit: 827ad02375793090fa8fee63cc372d130f11393f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2020
ms.locfileid: "89480675"
---
# <a name="mdx-data-manipulation---update-cube"></a>Manipulación de datos de MDX: UPDATE CUBE


  La instrucción UPDATE CUBE se emplea para reescribir datos en cualquier celda de un cubo que se agrega a su primario mediante la agregación SUM. Para obtener más información y un ejemplo, vea "Descripción de las asignaciones" en esta entrada de blog: [compilar una aplicación de reescritura con Analysis Services (blog)](https://docs.microsoft.com/archive/blogs/data_otaku/building-a-writeback-application-with-analysis-services).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
UPDATE [ CUBE ] Cube_Name   
   SET   
            <update clause>   
           [, <update clause> ...n ]  
  
<update clause> ::=   
      Tuple_Expression[.VALUE]= New_Value  
      [   
        USE_EQUAL_ALLOCATION   
        | USE_EQUAL_INCREMENT   
        | USE_WEIGHTED_ALLOCATION [ BY Weight_Expression]   
        | USE_WEIGHTED_INCREMENT [ BY Weight_Expression]  
      ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Cadena válida que proporciona el nombre de un cubo.  
  
 *Tuple_Expression*  
 Expresión MDX válida que devuelve una tupla.  
  
 *New_Value*  
 Expresión numérica válida.  
  
 *Weight_Expression*  
 Expresión numérica MDX (Expresiones multidimensionales) válida que devuelve un valor decimal entre 0 y 1.  
  
## <a name="remarks"></a>Observaciones  
 Puede actualizar el valor de una celda hoja o de una celda no hoja especificada de un cubo, asignando opcionalmente el valor de una celda no hoja especificada a través de las celdas hoja dependientes. La celda especificada por la expresión de tupla puede ser cualquier celda válida del espacio multidimensional (es decir, la celda no tiene que ser una celda hoja). Sin embargo, la celda se debe agregar con la función [SUM](../mdx/sum-mdx.md) Aggregate y no debe incluir un miembro calculado en la tupla que se usa para identificar la celda.  
  
 Puede ser útil pensar en la instrucción **Update Cube** como una subrutina que generará automáticamente una serie de operaciones de reescritura de celda individuales en celdas hoja y no hoja que se acumularán en una suma especificada.  
  
 La siguiente es una descripción de los métodos de asignación.  
  
 **USE_EQUAL_ALLOCATION:** A cada celda hoja que contribuye a la celda actualizada se le asignará un valor igual basado en la siguiente expresión.  
  
```  
<leaf cell value> =   
<New Value> / Count(leaf cells that are contained in <tuple>)  
```  
  
 **USE_EQUAL_INCREMENT:** Cada celda hoja que contribuye a la celda actualizada se cambiará de acuerdo con la siguiente expresión.  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value > - <existing value>) /  
Count(leaf cells contained in <tuple>)  
```  
  
 **USE_WEIGHTED_ALLOCATION:** A cada celda hoja que contribuye a la celda actualizada se le asignará un valor igual que se basa en la expresión siguiente.  
  
```  
<leaf cell value> = < New Value> * Weight_Expression  
```  
  
 **USE_WEIGHTED_INCREMENT:** Cada celda hoja que contribuye a la celda actualizada se cambiará de acuerdo con la siguiente expresión.  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value> - <existing value>)  * Weight_Expression  
```  
  
 Si no se especifica una expresión de peso, la instrucción **Update Cube** usa implícitamente la siguiente expresión.  
  
```  
Weight_Expression = <leaf cell value> / <existing value>  
```  
  
 Una expresión de peso debería expresarse como un valor decimal entre cero (0) y 1. Este valor especifica la proporción del valor asignado que desea asignar a las celdas hoja afectadas por la asignación. El programador de la aplicación cliente es el responsable de crear expresiones con valores agregados de resumen que sean iguales al valor asignado de la expresión.  
  
> [!CAUTION]  
>  La aplicación cliente debe considerar la asignación de todas las dimensiones de forma simultánea para evitar posibles resultados inesperados, incluidos los valores de resumen incorrectos o los datos incoherentes.  
  
 Cada asignación de **cubo de actualización** debe considerarse atómica para fines transaccionales. Eso significa que si alguna de las operaciones de asignación no tiene éxito por alguna razón, como un error en una fórmula o una infracción de seguridad, se producirá un error de toda la operación UPDATE CUBE. Antes de procesar los cálculos de las operaciones de asignación individuales, se toma una instantánea de los datos para garantizar que los cálculos resultantes sean correctos.  
  
> [!CAUTION]  
>  Cuando se utiliza en una medida que contiene enteros, el método USE_WEIGHTED_ALLOCATION puede devolver resultados imprecisos causados por cambios en el redondeo incremental.  
  
> [!IMPORTANT]  
>  Si las celdas actualizadas no se superponen, se puede utilizar la propiedad de la cadena de conexión **Update Isolation Level** para mejorar el rendimiento de UPDATE CUBE.  
  
## <a name="see-also"></a>Consulte también  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [Instrucciones de manipulación de datos de MDX &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
