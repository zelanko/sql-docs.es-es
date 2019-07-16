---
title: Predecir (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 165d03b886ad8e9beeb09bf5a835c879cc23a2a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055586"
---
# <a name="predict-mdx"></a>Predict (MDX)


    
> [!CAUTION]  
>  Esta función está en proceso de eliminación debido a incoherencias internas.  
>   
>  Revise la sección de ejemplo para encontrar una solución alternativa mediante una expresión DMX.  
  
 Devuelve un valor de una expresión numérica evaluada sobre un modelo de minería de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Predict(Mining_Model_Name,String_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Mining_Model_Name*  
 Expresión de cadena válida que representa el nombre de un modelo de minería de datos.  
  
 *String_Expression*  
 Expresión de cadena válida que se evalúa como una expresión DMX válida para el modelo de minería de datos especificado.  
  
## <a name="remarks"></a>Comentarios  
 El **Predict** función evalúa la expresión de cadena especificada dentro del contexto del modelo de minería de datos especificado.  
  
 La sintaxis y las funciones de minería de datos se documentan en la referencia de Expresiones de minería de datos (DMX).  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se predice nombre del clúster y la distancia desde él de un cliente determinado utilizando el modelo de minería de datos Customer Clusters:  
  
```  
WITH MEMBER MEASURES.CLNAME AS   
PREDICT("Customer Clusters", "Cluster()")  
MEMBER MEASURES.CLDISTANCE AS   
PREDICT("Customer Clusters", "ClusterDistance(Cluster())")  
SELECT {MEASURES.CLNAME, MEASURES.CLDISTANCE} ON 0   
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Customer].&[12012])  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
