---
title: "Creación de medidas en MDX | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f0347835-4983-4d26-acbb-6c8fae7992bd
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bf06631323bde8dc8c73bf716f5e0da858f19e71
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-building-measures"></a>Medidas de creación de MDX
  En las expresiones multidimensionales (MDX), una medida es una expresión DAX con nombre que se resuelve calculando la expresión para devolver un valor en un modelo tabular. Esta definición tan genérica tiene un alcance notable. La capacidad de construir y utilizar medias en una consulta MDX proporciona una gran solución para manipular datos tabulares.  
  
> [!WARNING]  
>  Las medidas solo pueden definirse en modelos tabulares; si la base de datos se establece en modo multidimensional, al crear una medida se generará un error.  
  
 Para crear una medida definida como parte de una consulta MDX, y en consecuencia con un ámbito limitado a la consulta, debe usar la palabra clave WITH. Puede usar la medida en una instrucción MDX SELECT. De esta manera, el miembro calculado creado con la palabra clave WITH se puede cambiar sin tener que tocar la instrucción SELECT. Sin embargo, en MDX se hace referencia a la medida de forma diferente que en las expresiones DAX; para hacer referencia a la medida que se denomina como miembro de la dimensión [Measures], vea el siguiente ejemplo MDX:  
  
```  
with measure  'Sales Territory'[Total Sales Amount] = SUM('Internet Sales'[Sales Amount]) + SUM('Reseller Sales'[Sales Amount])  
select measures.[Total Sales Amount] on columns  
     ,NON EMPTY [Date].[Calendar Year].children on rows  
from [Model]  
  
```  
  
 Devolverá los siguientes datos cuando se ejecute:  
  
||Total Sales Amount||  
|-|------------------------|-|  
|2001|11331808.96||  
|2002|30674773.18||  
|2003|41993729.72||  
|2004|25808962.34||  
  
## <a name="see-also"></a>Vea también  
 [CREATE MEMBER &#40;instrucción MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)   
 [Instrucción SELECT &#40; MDX &#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
