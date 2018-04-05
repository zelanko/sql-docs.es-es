---
title: Instrucción UPDATE CUBE (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Cube
- UPDATE CUBE
- UPDATE_CUBE
- UPDATE
dev_langs:
- kbMDX
helpviewer_keywords:
- updating cubes
- cubes [Analysis Services], modifying
- modifying cubes
- UPDATE CUBE statement
ms.assetid: 6c8f23bb-401b-49de-843a-5324ac977239
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 77ca2c4e3a63db80ff21a91309f5fc531e5ba3ca
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-manipulation---update-cube"></a>Manipulación de datos MDX - UPDATE CUBE
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  La instrucción UPDATE CUBE se emplea para reescribir datos en cualquier celda de un cubo que se agrega a su primario mediante la agregación SUM. Para obtener más información y un ejemplo, vea "Descripción de las asignaciones" en esta entrada de blog: [compilar una aplicación de reescritura con Analysis Services (blog)](http://go.microsoft.com/fwlink/?LinkId=394977).  
  
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
 *Restricciones obligatorias Cube_Name*  
 Cadena válida que proporciona el nombre de un cubo.  
  
 *Tuple_Expression*  
 Expresión MDX válida que devuelve una tupla.  
  
 *Archivo_ini*  
 Expresión numérica válida.  
  
 *Weight_Expression*  
 Expresión numérica MDX (Expresiones multidimensionales) válida que devuelve un valor decimal entre 0 y 1.  
  
## <a name="remarks"></a>Comentarios  
 Puede actualizar el valor de una celda hoja o de una celda no hoja especificada de un cubo, asignando opcionalmente el valor de una celda no hoja especificada a través de las celdas hoja dependientes. La celda especificada por la expresión de tupla puede ser cualquier celda válida del espacio multidimensional (es decir, la celda no tiene que ser una celda hoja). Sin embargo, debe agregarse la celda con el [suma](../mdx/sum-mdx.md) función de agregado y no se debe incluir un miembro calculado en la tupla que se usa para identificar la celda.  
  
 Puede resultar útil pensar en el **UPDATE CUBE** instrucción como una subrutina que generará automáticamente una serie de operaciones de reescritura de celda individual a las celdas hoja y no hoja que se acumularán en la suma especificada.  
  
 La siguiente es una descripción de los métodos de asignación.  
  
 **USE_EQUAL_ALLOCATION:** cada celda hoja que contribuye a la celda actualizada se asignará un valor igual basado en la siguiente expresión.  
  
```  
<leaf cell value> =   
<New Value> / Count(leaf cells that are contained in <tuple>)  
```  
  
 **USE_EQUAL_INCREMENT:**cada celda hoja que contribuye a la celda actualizada se cambiará según la siguiente expresión.  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value > - <existing value>) /  
Count(leaf cells contained in <tuple>)  
```  
  
 **USE_WEIGHTED_ALLOCATION:** cada celda hoja que contribuye a la celda actualizada se asignará un valor igual a la que se basa en la siguiente expresión.  
  
```  
<leaf cell value> = < New Value> * Weight_Expression  
```  
  
 **USE_WEIGHTED_INCREMENT:** cada celda hoja que contribuye a la celda actualizada se cambiará según la siguiente expresión.  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value> - <existing value>)  * Weight_Expression  
```  
  
 Si no se especifica una expresión de peso, la **UPDATE CUBE** instrucción utiliza la siguiente expresión de forma implícita.  
  
```  
Weight_Expression = <leaf cell value> / <existing value>  
```  
  
 Una expresión de peso debería expresarse como un valor decimal entre cero (0) y 1. Este valor especifica la proporción del valor asignado que desea asignar a las celdas hoja afectadas por la asignación. El programador de la aplicación cliente es el responsable de crear expresiones con valores agregados de resumen que sean iguales al valor asignado de la expresión.  
  
> [!CAUTION]  
>  La aplicación cliente debe considerar la asignación de todas las dimensiones de forma simultánea para evitar posibles resultados inesperados, incluidos los valores de resumen incorrectos o los datos incoherentes.  
  
 Cada **UPDATE CUBE** asignación debe considerarse atómicas para fines transaccionales. Eso significa que si alguna de las operaciones de asignación no tiene éxito por alguna razón, como un error en una fórmula o una infracción de seguridad, se producirá un error de toda la operación UPDATE CUBE. Antes de procesar los cálculos de las operaciones de asignación individuales, se toma una instantánea de los datos para garantizar que los cálculos resultantes sean correctos.  
  
> [!CAUTION]  
>  Cuando se utiliza en una medida que contiene enteros, el método USE_WEIGHTED_ALLOCATION puede devolver resultados imprecisos causados por cambios en el redondeo incremental.  
  
> [!IMPORTANT]  
>  Si las celdas actualizadas no se superponen, se puede utilizar la propiedad de la cadena de conexión **Update Isolation Level** para mejorar el rendimiento de UPDATE CUBE.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [Instrucciones de manipulación de datos MDX &#40; MDX &#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
