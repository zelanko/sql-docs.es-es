---
title: MSSQLSERVER_32040 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32040 (Database Engine error)
ms.assetid: 709219b1-f8b2-4696-8923-dd2e91492eb8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d2b92d959afa9dc38e9aad4a15ecd5eb3c44e87e
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551760"
---
# <a name="mssqlserver_32040"></a>MSSQLSERVER_32040
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|32040|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum32040|  
|Texto del mensaje|Se ha producido la alerta para 'transacción sin enviar más antigua'. El valor actual de '%d' sobrepasa el umbral '%d'.|  
  
## <a name="explanation"></a>Explicación  
 Este evento de creación de reflejo de la base de datos se genera en la instancia del servidor principal para indicar que la edad de la transacción sin enviar más antigua ha alcanzado el valor umbral especificado por el usuario. Normalmente, este evento se produce al cambiar el rendimiento del sistema. El ancho de banda entre los dos sistemas ha disminuido, o bien la carga ha aumentado.  
  
 La edad de la transacción sin enviar más antigua es una medida del rendimiento que le puede ayudar a evaluar el potencial de pérdida de datos como medida del número de minutos de transacciones sin enviar. Esta medida es especialmente relevante en sesiones de modo de alto rendimiento. No obstante, esta medida también es importante para la sesión de modo de alta seguridad cuando la creación de reflejo se detiene o suspende debido a que los asociados se han desconectado.  
  
## <a name="user-action"></a>Acción del usuario  
 Compruebe las cargas en las instancias del servidor principal y reflejado y su conexión de red para localizar la causa.  
  
## <a name="see-also"></a>Consulte también  
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Usar alertas y umbrales de advertencia de las métricas de rendimiento de la creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
