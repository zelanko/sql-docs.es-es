---
title: Totales visuales y totales no visuales | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 90925c99f281d128ff197fb7b0ef3b088faf5b7d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62984452"
---
# <a name="visual-totals-and-non-visual-totals"></a>Totales visuales y totales no visuales
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Los totales visuales son totales que se encuentran al final de una columna o fila que suman todos los elementos visibles de la columna o fila. Este es el comportamiento predeterminado de la mayoría de las tablas cuando se muestran. Sin embargo, a veces el usuario desea mostrar solo ciertas columnas de una tabla manteniendo los totales de toda la fila, incluidos los que no se muestran y que se denominan **Totales no visuales**, ya que el total proviene de los valores visibles y no visibles.  
  
 En el siguiente escenario se muestra el comportamiento de los totales no visuales. El primer paso muestra el comportamiento predeterminado de los totales visuales.  
  
 El ejemplo siguiente es una consulta de [Adventure Works] para obtener las cifras de [Reseller Sales Amount] en una tabla donde las categorías de producto son las columnas y los tipos comerciales de revendedor son las filas. Observe que esos totales se dan tanto para productos como para revendedores cuando se emite la siguiente instrucción SELECT:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Produce los siguientes resultados:  
  
|||||||  
|-|-|-|-|-|-|  
||**All Products**|**Accessories**|**Bikes**|**Clothing**|**Components**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$66,302,381.56**|**$1,777,840.84**|**$11,799,076.66**|  
|**Specialty Bike Shop**|**$6,756,166.18**|**$65,125.48**|**$6,080,117.73**|**$252,933.91**|**$357,989.07**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$30,892,354.33**|**$592,385.71**|**$3,307,774.48**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$29,329,909.50**|**$932,521.23**|**$8,133,313.11**|  
  
## <a name="non-visual-on-rows-and-columns"></a>Filas y columnas no visuales  
 Para generar una tabla con datos solo para los productos Accessories y Clothing, y los revendedores Value Added Reseller y Warehouse, manteniendo todavía los totales globales, se podría escribir de la forma siguiente usando NON VISUAL:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Produce los siguientes resultados:  
  
|||||  
|-|-|-|-|  
||**All Products**|**Accessories**|**Clothing**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$1,777,840.84**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$592,385.71**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$932,521.23**|  
  
## <a name="non-visual-on-rows"></a>Filas no visuales  
 Para generar una tabla que sume visualmente las columnas pero que tome el total real de todos [Category] para los totales de las filas, debe emitirse la consulta siguiente:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0`  
  
 `from ( Select {[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 0`  
  
 `from [Adventure Works])`  
  
 `)`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Observe cómo NON VISUAL se aplica solamente a [Category].  
  
 La consulta anterior genera los resultados siguientes:  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$73,694,430.80|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 Al comparar con los resultados anteriores, puede observar que la fila [All Resellers] suma ahora hasta los valores mostrados para [Value Added Reseller] y [Warehouse], pero que la columna [All Products] muestra el valor total de todos los productos, incluso los que no se muestran.  
  
## <a name="see-also"></a>Vea también  
 [Conceptos clave de MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Autoexists](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [Trabajar con miembros, tuplas y conjuntos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [Consulta de MDX básica &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)   
 [Restringir la consulta con ejes de consulta y segmentador &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)   
 [Establecer el contexto de cubo en una consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)  
  
  
