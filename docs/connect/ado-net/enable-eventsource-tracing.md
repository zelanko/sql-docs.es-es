---
title: Habilitar el seguimiento de eventos en SqlClient
description: Describe cómo habilitar el seguimiento de eventos en SqlClient implementando un agente de escucha de eventos y cómo obtener acceso a los datos del evento.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 4eac1ab519549ccace092cfc175c735dd4537269
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725746"
---
# <a name="enabling-event-tracing-in-sqlclient"></a>Habilitar el seguimiento de eventos en SqlClient

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

[Seguimiento de eventos para Windows (ETW)](/windows/win32/etw/event-tracing-portal) es una eficaz herramienta de seguimiento de nivel de kernel que permite registrar eventos definidos por el controlador para la depuración y la realización de pruebas. SqlClient admite la captura de eventos ETW en diferentes niveles informativos. Para comenzar a capturar seguimientos de eventos, las aplicaciones cliente deberían escuchar eventos de la implementación de EventSource de SqlClient:

```
Microsoft.Data.SqlClient.EventSource
```

La implementación actual admite las siguientes palabras clave de evento:

| Nombre de palabra clave | Value | Descripción |
| ------------ | ----- | ----------- |
| ExecutionTrace | 1 | Activa la captura de eventos de inicio y detención antes y después de la ejecución del comando. |
| Seguimiento | 2 | Activa la captura de eventos de seguimiento de flujo de aplicación básicos. |
| Ámbito | 4 | Activa la captura de eventos de entrada y salida. |
| NotificationTrace | 8 | Activa la captura de eventos de seguimiento `SqlNotification`. |
| NotificationScope | 16 | Activa la captura de eventos de entrada y salida del ámbito `SqlNotification`. |
| PoolerTrace | 32 | Activa la captura de eventos de seguimiento de flujo de agrupación de conexiones. |
| PoolerScope | 64 | Activa la captura de eventos de seguimiento de ámbito de agrupación de conexiones. |
| AdvancedTrace | 128 | Activa la captura de eventos de seguimiento de flujo avanzados. |
| AdvancedTraceBin  | 256 | Activa la captura de eventos de seguimiento de flujo avanzados con información adicional. |
| CorrelationTrace | 512 | Activa la captura de eventos de seguimiento de flujo de correlación. |
| StateDump | 1024 | Activa la captura del volcado del estado completo de `SqlConnection`. |
| SNITrace | 2048 | Activa la captura de eventos de seguimiento de flujo de la implementación de redes administradas (solo es aplicable en .NET Core). |
| SNIScope | 4096 | Activa la captura de eventos de ámbito de la implementación de redes administradas (solo es aplicable en .NET Core). |
|||

## <a name="example"></a>Ejemplo
En el ejemplo siguiente se habilita el seguimiento de eventos para una operación de datos en la base de datos de ejemplo **AdventureWorks** y se muestran los eventos en la ventana de la consola.

[!code-csharp [SqlClientEventSource#1](~/../sqlclient/doc/samples/SqlClientEventSource.cs#1)]

## <a name="external-resources"></a>Recursos externos  
Para obtener más información, vea los recursos siguientes.  
  
|Recurso|Descripción|  
|--------------|-----------------|  
|[clase EventSource](/dotnet/api/system.diagnostics.tracing.eventsource)|Ofrece la capacidad de crear y modificar eventos ETW.| 
|[Clase EventListener](/dotnet/api/system.diagnostics.tracing.eventlistener)|Proporciona métodos para habilitar y deshabilitar eventos de orígenes de eventos.|