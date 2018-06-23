---
title: Control de errores (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d04c59c1af5a942fa53bf2fd2fe47369a15c29f5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201032"
---
# <a name="error-handling-mdx"></a>Control de errores (MDX)
  Todos los cubos pueden controlar la forma en que se administran los errores de los scripts de expresiones multidimensionales (MDX). Control de errores se realiza a través de la `ScriptErrorHandlingMode` enumerador. Los valores posibles que admite este enumerador son los siguientes:  
  
 `IgnoreNone`  
 Hace que el servidor genere un error cuando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] detecta un error en el script MDX.  
  
 `IgnoreAll`  
 Hace que el servidor omita todos los comandos del script MDX que contengan un error, incluidos los errores de sintaxis, de resolución de nombres y otros.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  