---
title: Niveles (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Levels
dev_langs:
- kbMDX
helpviewer_keywords:
- Levels function
ms.assetid: 1a989cc9-8aa8-4ec3-b5e9-795d6fa84983
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2b465db3999a950c4ae78997fc66215e72215ed2
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="levels-mdx"></a>Levels (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el nivel cuya posición en una dimensión o jerarquía se especifica mediante una expresión numérica, o cuyo nombre se especifica mediante una expresión de cadena.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Numeric expression syntax  
Hierarchy_Expression.Levels( Level_Number )  
  
String expression syntax  
Hierarchy_Expression.Levels( Level_Name )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Expression*  
 Expresión MDX válida que devuelve una jerarquía.  
  
 *Level_Number*  
 Expresión numérica válida que especifica un número de nivel.  
  
 *Level_Name*  
 Expresión de cadena válida que especifica un nombre de nivel.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica un número de nivel, la **niveles** función devuelve el nivel asociado a la posición de base cero especificada.  
  
 Si se especifica un nombre de nivel, la **niveles** función devuelve el nivel especificado.  
  
> [!NOTE]  
>  Utilice la sintaxis de expresión de cadena para funciones definidas por el usuario.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran cada uno de los **niveles** sintaxis de función.  
  
### <a name="numeric"></a>Numérico  
 El ejemplo siguiente devuelve el nivel Country:  
  
```  
SELECT [Geography].[Geography].Levels(1) ON 0  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 El ejemplo siguiente devuelve el nivel Country:  
  
```  
SELECT [Geography].[Geography].Levels('Country') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

