---
title: KPIValue (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: KPIValue function
ms.assetid: c4f8532c-4c24-4ad5-8847-4522511e0039
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4e02510740e79519c15ddee8ca3107d275c311eb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="kpivalue-mdx"></a>KPIValue (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el miembro que calcula el valor del indicador clave de rendimiento (KPI) especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
KPIValue(KPI_Name)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Nombre_kpi*  
 Expresión de cadena válida que especifica el nombre del KPI.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el valor del KPI, el objetivo del KPI, el estado del KPI y la tendencia del KPI de la medida Channel Revenue de los descendientes de tres miembros de la jerarquía de atributo Fiscal Year.  
  
```  
SELECT  
   { KPIValue("Channel Revenue"),   
     KPIGoal("Channel Revenue"),  
     KPIStatus("Channel Revenue"),   
     KPITrend("Channel Revenue")  
   } ON Columns,  
Descendants  
   ( { [Date].[Fiscal].[Fiscal Year].&[2002],  
       [Date].[Fiscal].[Fiscal Year].&[2003],  
       [Date].[Fiscal].[Fiscal Year].&[2004]   
     }, [Date].[Fiscal].[Fiscal Quarter]  
   ) ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
