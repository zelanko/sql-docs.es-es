---
title: DataMember (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2979799686ad1d97018471111c57670383f7f4f8
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577857"
---
# <a name="datamember-mdx"></a>DataMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el miembro de datos generados por el sistema asociado a un miembro no hoja de una dimensión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Notas  
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
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Conceptos clave para MDX &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  
