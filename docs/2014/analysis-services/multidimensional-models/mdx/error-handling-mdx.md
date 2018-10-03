---
title: (MDX) de control de errores | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57b7320e8d09a3106d29a7f4c53c14a52afaadd7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187985"
---
# <a name="error-handling-mdx"></a>Control de errores (MDX)
  Todos los cubos pueden controlar la forma en que se administran los errores de los scripts de expresiones multidimensionales (MDX). Control de errores se realiza a través de la `ScriptErrorHandlingMode` enumerador. Los valores posibles que admite este enumerador son los siguientes:  
  
 `IgnoreNone`  
 Hace que el servidor genere un error cuando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] detecta un error en el script MDX.  
  
 `IgnoreAll`  
 Hace que el servidor omita todos los comandos del script MDX que contengan un error, incluidos los errores de sintaxis, de resolución de nombres y otros.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
