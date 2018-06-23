---
title: MSSQLSERVER_32042 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 32042 (Database Engine error)
ms.assetid: 53a51c7a-dcd4-4c15-b4d2-6aaa9dce76da
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2dc82f65ed2044ac5edc324e78d743dd6b6e9622
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111573"
---
# <a name="mssqlserver32042"></a>MSSQLSERVER_32042
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|32042|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum32042|  
|Texto del mensaje|Se ha producido la alerta para 'registro sin enviar'. El valor actual de '%d' sobrepasa el umbral '%d'.|  
  
## <a name="explanation"></a>Explicación  
 Este evento de creación de reflejo de la base de datos se genera en la instancia del servidor principal para indicar que la cantidad de registro sin enviar ha alcanzado el valor umbral especificado por el usuario. Normalmente, este evento se produce al cambiar el rendimiento del sistema. El ancho de banda entre los dos sistemas ha disminuido, o bien la carga ha aumentado.  
  
 La cantidad de registro sin enviar es una medida de rendimiento que le puede ayudar a evaluar el potencial de pérdida de datos en número de kilobytes (KB) de registro sin enviar. Esta medida es especialmente pertinente en sesiones de modo de alto rendimiento. No obstante, esta medida también es importante para la sesión de modo de alta seguridad cuando la creación de reflejo se detiene o suspende debido a que los asociados se han desconectado.  
  
## <a name="user-action"></a>Acción del usuario  
 Compruebe las cargas en las instancias del servidor principal y reflejado y su conexión de red para localizar la causa.  
  
## <a name="see-also"></a>Vea también  
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Usar alertas y umbrales de advertencia de las métricas de rendimiento de la creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  