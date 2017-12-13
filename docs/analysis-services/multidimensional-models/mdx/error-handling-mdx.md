---
title: Control de errores (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1eb0133bb4f6e1d4b03e83f771c6170204eeb5b8
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="error-handling-mdx"></a>Control de errores (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Cada cubo puede controlar cómo se controlan los errores dentro de un script de expresiones multidimensionales (MDX). El control de errores se realiza mediante el enumerador **ScriptErrorHandlingMode** . Los valores posibles que admite este enumerador son los siguientes:  
  
 **IgnoreNone**  
 Hace que el servidor genere un error cuando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] detecta un error en el script MDX.  
  
 **IgnoreAll**  
 Hace que el servidor omita todos los comandos del script MDX que contengan un error, incluidos los errores de sintaxis, de resolución de nombres y otros.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
