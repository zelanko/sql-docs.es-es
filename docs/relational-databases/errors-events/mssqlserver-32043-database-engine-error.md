---
title: MSSQLSERVER_32043 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 32043 (Database Engine error)
ms.assetid: a0c48ae3-4c8c-419c-afb5-579fcefac01d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8f012c251d97fe5247fcf9f950f5d6d83e2f11ff
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47751799"
---
# <a name="mssqlserver32043"></a>MSSQLSERVER_32043
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|32043|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum32043|  
|Texto del mensaje|Se ha producido la alerta para 'registro sin restaurar'. El valor actual de '%d' sobrepasa el umbral '%d'.|  
  
## <a name="explanation"></a>Explicación  
Este evento de creación de reflejo de la base de datos se genera en la instancia del servidor reflejado para indicar que la cantidad de registro sin restaurar ha alcanzado el valor umbral especificado por el usuario. Normalmente, este evento se produce al cambiar el rendimiento del sistema. El ancho de banda entre los dos sistemas ha disminuido, o bien la carga ha aumentado.  
  
Un registro sin restaurar es un registro recibido por la instancia del servidor reflejado y escrito en el disco, pero que está esperando a ser restaurado en la base de datos reflejada. La cantidad de registro no restaurado en kilobytes (KB) es una medida del rendimiento que le puede ayudar a evaluar el tiempo de conmutación por error actual. El tiempo necesario para aplicar el registro sin restaurar es el factor principal en el tiempo de conmutación por error, junto con un breve tiempo adicional necesario para recuperar la base de datos y ponerla en línea.  
  
> [!NOTE]  
> En el caso de una conmutación automática por error, el tiempo para que el sistema notifique el error no depende del tiempo de conmutación por error.  
  
## <a name="user-action"></a>Acción del usuario  
Compruebe las cargas en las instancias del servidor principal y reflejado y su conexión de red para localizar la causa.  
  
## <a name="see-also"></a>Ver también  
[Creación de reflejo de la base de datos &#40;SQL Server&#41;](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[Usar alertas y umbrales de advertencia de las métricas de rendimiento de la creación de reflejo &#40;SQL Server&#41;](~/database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
