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
ms.openlocfilehash: ae667d2cecb65f2525aaf855d3d1b70d40a59b21
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68016875"
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
 Un valor de marca de acceso que especifica que el parámetro *Pass_Value* contiene el índice de base cero del paso de cálculo. ABSOLUTE es el valor de marca de acceso predeterminado si no se especifica un valor de marca de acceso.  
  
 RELATIVE  
 Un valor de marca de acceso que especifica que el parámetro *Pass_Value* contiene un desplazamiento relativo desde el paso de cálculo del cálculo desencadenador. Si el desplazamiento se resuelve en un índice de paso de cálculo menor que 0, se utiliza el paso de cálculo 0 y no se producen errores.  
  
 ALL  
 Cuando se establece esta marca, todos los valores son NULL, excepto los cargados por el motor de almacenamiento. Cuando no se establece, los valores se agregan sin aplicar cálculos.  
  
## <a name="remarks"></a>Observaciones  
 Si se proporciona una expresión numérica, la función devuelve un valor numérico mediante la evaluación de la expresión numérica MDX especificada en el paso de cálculo y, de manera opcional, modificada por una marca de acceso y un modificador de marca de acceso.  
  
 Si se proporciona una expresión de cadena, la función devuelve un valor de cadena evaluando la expresión de cadena MDX especificada en el paso de cálculo especificado y modificada opcionalmente mediante una marca de acceso y un modificador de marca de acceso *.*  
  
 Con la resolución automática de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]recursividad en, esta función tiene poco uso práctico.  
  
> [!NOTE]  
>  Solo los administradores pueden usar la función **CalculationPassValue** en un script MDX. Se produce un error si un script de MDX que contiene esta función se ejecuta en el contexto de un rol que no tiene privilegios de administrador.  
  
## <a name="see-also"></a>Consulte también  
 [&#41;CalculationCurrentPass &#40;MDX](../mdx/calculationcurrentpass-mdx.md)   
 [IIf &#40;&#41;MDX](../mdx/iif-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
