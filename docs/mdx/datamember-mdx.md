---
title: DataMember (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DATAMEMBER
dev_langs: kbMDX
helpviewer_keywords: DataMember function
ms.assetid: 65bf21e8-1cb2-4ae8-bfbe-bb4d72589557
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3f002e188055f7643d75e63506a95387198e99b4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="datamember-mdx"></a>DataMember (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el miembro de datos generados por el sistema asociado a un miembro no hoja de una dimensión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 Esta función opera en los miembros no hoja en cualquier jerarquía y puede usarse en el [UPDATE CUBE (instrucción, MDX)](../mdx/mdx-data-manipulation-update-cube.md) comando para reescribir datos a un miembro no hoja directamente, en lugar de a los descendientes del miembro hoja.  
  
> [!NOTE]  
>  Devuelve el miembro especificado si es un miembro hoja o si el miembro no hoja no dispone de un miembro de datos asociado.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa el **DataMember** función en una medida calculada para mostrar la cuota de ventas para cada empleado individual:  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [Conceptos clave de MDX &#40; Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  
