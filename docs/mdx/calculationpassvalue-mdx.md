---
title: CalculationPassValue (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ca5966492ac83599cd4a053ea526e2ce366e4b0e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181626"
---
# <a name="calculationpassvalue-mdx"></a>CalculationPassValue (MDX)


  Devuelve el valor numérico o de cadena de una expresión MDX (Expresiones multidimensionales) evaluada sobre el paso de cálculo especificado de un cubo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
      Numeric syntax  
CalculationPassValue(Numeric_Expression,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
String syntax  
CalculationPassValue(String_Expression ,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Numeric_Expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
 *String_Expression*  
 Expresión de cadena válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número expresado como una cadena.  
  
 *Pass_Value*  
 Expresión numérica válida que especifica el número de paso de cálculo.  
  
 ABSOLUTE  
 Un valor de marca de acceso que especifica que el *Pass_Value* parámetro contiene el índice de base cero del pase de cálculo. ABSOLUTE es el valor de marca de acceso predeterminado si no se especifica un valor de marca de acceso.  
  
 RELATIVE  
 Un valor de marca de acceso que especifica que el *Pass_Value* parámetro contiene un desplazamiento relativo desde el paso de cálculo del cálculo desencadenador. Si el desplazamiento se resuelve en un índice de paso de cálculo menor que 0, se utiliza el paso de cálculo 0 y no se producen errores.  
  
 ALL  
 Cuando se establece esta marca, todos los valores son NULL, excepto los cargados por el motor de almacenamiento. Cuando no se establece, los valores se agregan sin aplicar cálculos.  
  
## <a name="remarks"></a>Comentarios  
 Si se proporciona una expresión numérica, la función devuelve un valor numérico mediante la evaluación de la expresión numérica MDX especificada en el paso de cálculo y, de manera opcional, modificada por una marca de acceso y un modificador de marca de acceso.  
  
 Si se proporciona una expresión de cadena, la función devuelve un valor de cadena mediante la evaluación de la expresión de cadena MDX especificada en el paso de cálculo y modificado opcionalmente mediante una marca de acceso y un modificador de marca de acceso *.*  
  
 Con la resolución automática de recursividad de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], esta función tiene muy poco uso práctico.  
  
> [!NOTE]  
>  Solo los administradores pueden usar el **CalculationPassValue** función dentro de un script MDX. Se produce un error si un script de MDX que contiene esta función se ejecuta en el contexto de un rol que no tiene privilegios de administrador.  
  
## <a name="see-also"></a>Vea también  
 [CalculationCurrentPass &#40;MDX&#41;](../mdx/calculationcurrentpass-mdx.md)   
 [IIf &#40;MDX&#41;](../mdx/iif-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
