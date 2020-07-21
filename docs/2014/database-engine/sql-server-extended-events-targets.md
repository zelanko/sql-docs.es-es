---
title: SQL Server destinos de eventos extendidos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events]
- extended events [SQL Server], targets
ms.assetid: e281684c-40d1-4cf9-a0d4-7ea1ecffa384
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 75270f5ce03de820828da65c765044a7dafdcb8f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928872"
---
# <a name="sql-server-extended-events-targets"></a>SQL Server Extended Events Targets
  Los destinos de Extended Events de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] son los consumidores de eventos. Los destinos escriben en un archivo, almacenan los datos de evento en un búfer de memoria o agregan los datos de evento. Los destinos procesan los datos de forma sincrónica o asincrónica.  
  
 El diseño de Extended Events garantiza que los destinos reciban eventos una sola vez por sesión.  
  
 Los eventos extendidos proporcionan los destinos siguientes que pueden utilizarse en una sesión de eventos extendidos:  
  
-   [Contador de eventos](../../2014/database-engine/event-counter-target.md)  
  
     Cuenta todos los eventos especificados que se producen durante una sesión de eventos extendidos. Se usa para obtener información sobre las características de carga de trabajo sin agregar la sobrecarga que supone una colección de eventos completa. Es un destino sincrónico.  
  
-   [Archivo de eventos](../../2014/database-engine/event-file-target.md)  
  
     Se usa para escribir en disco la salida de la sesión de eventos de los búferes de memoria completos. Es un destino asincrónico.  
  
-   [Emparejamiento de eventos](../../2014/database-engine/event-pairing-target.md)  
  
     Muchos tipos de eventos se producen en parejas, como por ejemplo, bloqueo y desbloqueo. Se usa para determinar cuándo un determinado evento emparejado no se produce en el conjunto correspondiente. Es un destino asincrónico.  
  
-   [Seguimiento de eventos para Windows (ETW)](../relational-databases/extended-events/event-tracing-for-windows-target.md)  
  
     Se usa para establecer correlaciones entre los eventos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y los datos de evento de la aplicación o del sistema operativo Windows. Es un destino sincrónico.  
  
-   [Histograma](../../2014/database-engine/histogram-target.md)  
  
     Se usa para contar el número de veces que se produce el evento especificado en función de la acción o columna de evento indicada. Es un destino asincrónico.  
  
-   [Búfer en anillo](../../2014/database-engine/ring-buffer-target.md)  
  
     Se usa para mantener los datos de evento en memoria con un orden FIFO (primero en entrar, primero en salir) o con un orden FIFO por evento. Es un destino asincrónico.  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../relational-databases/extended-events/extended-events.md)   
 [Paquetes de SQL Server Extended Events](../relational-databases/extended-events/sql-server-extended-events-packages.md)   
 [SQL Server sesiones de eventos extendidos](../relational-databases/extended-events/sql-server-extended-events-sessions.md)   
 [Motor de SQL Server Extended Events](../relational-databases/extended-events/sql-server-extended-events-engine.md)  
  
  
