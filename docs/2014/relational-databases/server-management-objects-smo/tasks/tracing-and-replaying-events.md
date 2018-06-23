---
title: Seguimiento y reproducción de eventos | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 41de47825af581e0584b8a58254e485691da1420
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202670"
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
  
 Los datos de seguimiento de la `Trace` y `Replay` objetos se puedan usar la aplicación SMO o se pueden examinar manualmente utilizando [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md). Los datos de seguimiento también son compatibles con el [SQL Trace](../../sql-trace/sql-trace.md) procedimientos almacenados que también proporcionan funciones de seguimiento.  
  
 Los objetos de seguimiento de SMO residen en el espacio de nombres <xref:Microsoft.SqlServer.Management.Trace>, que requiere una referencia al archivo Microsoft.SQLServer.ConnectionInfo.dll.  
  
 El `Trace` y `Replay` objetos requieren un <xref:Microsoft.SqlServer.Management.Common.ServerConnection> <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> objeto que se va a establecer una conexión con la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> reside en el espacio de nombres <xref:Microsoft.SqlServer.Management.Common>, que requiere una referencia al archivo Microsoft.SQLServer.ConnectionInfo.dll.  
  
> [!NOTE]  
>  Los objetos `Trace` y `Replay` no se pueden utilizar en una plataforma de 64 bits.  
  
  