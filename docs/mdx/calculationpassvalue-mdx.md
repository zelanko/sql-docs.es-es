---
title: CalculationPassValue (MDX) | Documentos de Microsoft
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
- CALCULATIONPASSVALUE
dev_langs:
- kbMDX
helpviewer_keywords:
- CalculationPassValue function
ms.assetid: 1b4012cb-c8c7-441a-bb9c-59430703b189
caps.latest.revision: 45
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: dd5ed7f5ef6eb60b37c5066f7535d34913572871
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="calculationpassvalue-mdx"></a>CalculationPassValue (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el valor numérico o de cadena de una expresión MDX (Expresiones multidimensionales) evaluada sobre el paso de cálculo especificado de un cubo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
      Numeric syntax  
CalculationPassValue(Numeric_Expression,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
String syntax  
CalculationPassValue(String_Expression ,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
 *String_Expression*  
 Expresión de cadena válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número expresado como una cadena.  
  
 *Pass_Value*  
 Expresión numérica válida que especifica el número de paso de cálculo.  
  
 ABSOLUTE  
 Un valor de marca de acceso que especifica que la *Pass_Value* parámetro contiene el índice basado en cero del paso de cálculo. ABSOLUTE es el valor de marca de acceso predeterminado si no se especifica un valor de marca de acceso.  
  
 RELATIVE  
 Un valor de marca de acceso que especifica que la *Pass_Value* parámetro contiene un desplazamiento relativo del paso de cálculo del cálculo desencadenador. Si el desplazamiento se resuelve en un índice de paso de cálculo menor que 0, se utiliza el paso de cálculo 0 y no se producen errores.  
  
 ALL  
 Cuando se establece esta marca, todos los valores son NULL, excepto los cargados por el motor de almacenamiento. Cuando no se establece, los valores se agregan sin aplicar cálculos.  
  
## <a name="remarks"></a>Notas  
 Si se proporciona una expresión numérica, la función devuelve un valor numérico mediante la evaluación de la expresión numérica MDX especificada en el paso de cálculo y, de manera opcional, modificada por una marca de acceso y un modificador de marca de acceso.  
  
 Si se proporciona una expresión de cadena, la función devuelve un valor de cadena mediante la evaluación de la expresión de cadena MDX especificada en el paso de cálculo especificado y modificado opcionalmente mediante una marca de acceso y un modificador de marca de acceso*.*  
  
 Con la resolución automática de recursividad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], esta función tiene muy poco uso práctico.  
  
> [!NOTE]  
>  Solo los administradores pueden usar la **CalculationPassValue** función dentro de un script MDX. Se produce un error si un script de MDX que contiene esta función se ejecuta en el contexto de un rol que no tiene privilegios de administrador.  
  
## <a name="see-also"></a>Ver también  
 [CalculationCurrentPass &#40; MDX &#41;](../mdx/calculationcurrentpass-mdx.md)   
 [IIf &#40; MDX &#41;](../mdx/iif-mdx.md)   
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
