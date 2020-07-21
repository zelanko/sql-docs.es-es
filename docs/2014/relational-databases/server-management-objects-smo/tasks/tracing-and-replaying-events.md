---
title: Seguimiento y reproducción de eventos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
author: stevestein
ms.author: sstein
ms.openlocfilehash: bd75fdae7fc871101aa07785561c8277783a424f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063056"
---
# <a name="tracing-and-replaying-events"></a>Seguimiento y reproducción de eventos
  En SMO, los objetos `Trace` y `Replay` del espacio de nombres <xref:Microsoft.SqlServer.Management.Trace> proporcionan acceso mediante programación a la funcionalidad de [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)], que se utiliza para supervisar una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Puede capturar y guardar datos acerca de cada evento en un archivo o en una tabla para analizarlos posteriormente. Por ejemplo, puede supervisar un entorno de producción para ver qué procedimientos almacenados afectan negativamente al rendimiento al ejecutarse demasiado lentamente.  
  
 Los objetos `Trace` y `Replay` proporcionan un conjunto de objetos que se pueden utilizar para crear seguimientos en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Puede utilizar estos objetos desde sus propias aplicaciones para crear seguimientos manualmente para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Asimismo, se puede utilizar los objetos `Trace` de SMO para leer los archivos y las tablas de Seguimiento de SQL que se crearon al supervisar el registro de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o DTS.  
  
 Los objetos `Trace` de SMO permiten realizar las funciones siguientes:  
  
-   Crear un seguimiento.  
  
-   Establecer filtros en el seguimiento.  
  
-   Establecer los eventos de los que se va a realizar un seguimiento.  
  
-   Detener o iniciar un seguimiento.  
  
-   Leer los archivos y las tablas de seguimiento.  
  
-   Obtener información sobre los eventos en un seguimiento.  
  
-   Obtener información sobre los filtros en un seguimiento.  
  
-   Manipular mediante programación los datos de seguimiento.  
  
-   Escribir archivos y tablas de seguimiento.  
  
-   Reproducir archivos o tablas de seguimiento.  
  
 La aplicación SMO puede utilizar los datos de seguimiento de los `Trace` `Replay` objetos y, o bien se puede examinar manualmente mediante [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md). Los datos de seguimiento también son compatibles con los procedimientos almacenados de [SQL Trace](../../sql-trace/sql-trace.md) que también proporcionan funciones de seguimiento.  
  
 Los objetos de seguimiento de SMO residen en el espacio de nombres <xref:Microsoft.SqlServer.Management.Trace>, que requiere una referencia al archivo Microsoft.SQLServer.ConnectionInfo.dll.  
  
 Los objetos `Trace` y `Replay` requieren un objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection><xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> que establezca una conexión con la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> reside en el espacio de nombres <xref:Microsoft.SqlServer.Management.Common>, que requiere una referencia al archivo Microsoft.SQLServer.ConnectionInfo.dll.  
  
> [!NOTE]  
>  Los objetos `Trace` y `Replay` no se pueden utilizar en una plataforma de 64 bits.  
  
  
