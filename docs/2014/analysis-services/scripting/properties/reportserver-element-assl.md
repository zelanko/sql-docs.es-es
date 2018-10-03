---
title: Elemento ReportServer (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ReportServer Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportServer
helpviewer_keywords:
- ReportServer element
ms.assetid: 677437aa-9d15-4dcc-a9bc-34f851d9640d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d28184ae7174689c154011f7e973f04061d865e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219405"
---
# <a name="reportserver-element-assl"></a>Elemento ReportServer (ASSL)
  Contiene el nombre de la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] instancia que está usando el [ReportAction](../data-type/action-data-type-assl.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ReportAction>  
  ...  
   <ReportServer>...</ReportServer>  
   ...  
</ReportAction>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ReportAction](../data-type/action-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que se corresponde con el elemento primario de `ReportServer` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ReportAction>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
