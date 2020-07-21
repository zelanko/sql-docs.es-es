---
title: MSSQLSERVER_32043 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32043 (Database Engine error)
ms.assetid: a0c48ae3-4c8c-419c-afb5-579fcefac01d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 27b08927861e9222fe87ebb108d8595f63edb813
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551740"
---
# <a name="mssqlserver_32043"></a>MSSQLSERVER_32043
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|32043|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum32043|  
|Texto del mensaje|Se ha producido la alerta para 'registro sin restaurar'. El valor actual de '%d' sobrepasa el umbral '%d'.|  
  
## <a name="explanation"></a>Explicación  
 Este evento de creación de reflejo de la base de datos se genera en la instancia del servidor reflejado para indicar que la cantidad de registro sin restaurar ha alcanzado el valor umbral especificado por el usuario. Normalmente, este evento se produce al cambiar el rendimiento del sistema. El ancho de banda entre los dos sistemas ha disminuido, o bien la carga ha aumentado.  
  
 Un registro sin restaurar es un registro recibido por la instancia del servidor reflejado y escrito en el disco, pero que está esperando a ser restaurado en la base de datos reflejada. La cantidad de registro no restaurado en kilobytes (KB) es una medida del rendimiento que le puede ayudar a evaluar el tiempo de conmutación por error actual. El tiempo necesario para aplicar el registro sin restaurar es el factor principal en el tiempo de conmutación por error, junto con un breve tiempo adicional necesario para recuperar la base de datos y ponerla en línea.  
  
> [!NOTE]  
>  En el caso de una conmutación automática por error, el tiempo para que el sistema notifique el error no depende del tiempo de conmutación por error.  
  
## <a name="user-action"></a>Acción del usuario  
 Compruebe las cargas en las instancias del servidor principal y reflejado y su conexión de red para localizar la causa.  
  
## <a name="see-also"></a>Consulte también  
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Usar alertas y umbrales de advertencia de las métricas de rendimiento de la creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
