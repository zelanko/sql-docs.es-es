---
title: Unorder, (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- UNORDER
dev_langs:
- kbMDX
helpviewer_keywords:
- Unorder function
ms.assetid: a805df2a-6320-45bc-989f-90e85faf027f
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: ff60b1efa91f68998a271acc31b3aef0376ac3d7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="unorder-mdx"></a>Unorder (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Quita cualquier orden impuesto sobre un conjunto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Unorder(Set_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Comentarios  
 El **Unorder** función quita cualquier ordenación impuesta en las tuplas contenidas en el conjunto por cualquier otra función o instrucción, como la [orden](../mdx/order-mdx.md) función. El orden de las tuplas en el conjunto devuelto por la **Unorder** función es indeterminada.  
  
 El **Unorder** función se utiliza como una sugerencia para [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para optimizar la consulta para el procesamiento del conjunto. Si el orden de las tuplas de un conjunto no es relevante para una consulta o cálculo, usando la **Unorder** función puede proporcionar una mejora del rendimiento en casos como este. Por ejemplo, el [NonEmpty (MDX)](../mdx/nonempty-mdx.md) función puede funcionar mejor cuando el conjunto especificado a esta función está ordenado que si [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tiene que conservar el orden, aunque con [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], el procesador de consultas intenta realizar esta función automáticamente para muchas funciones, como **suma** y **agregado**. La ventaja de rendimiento de usar **Unorder** es probable que sea notable en conjuntos muy grandes que consta de millones de tuplas.  
  
## <a name="example"></a>Ejemplo  
 El siguiente pseudocódigo muestra la sintaxis de esta función.  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
