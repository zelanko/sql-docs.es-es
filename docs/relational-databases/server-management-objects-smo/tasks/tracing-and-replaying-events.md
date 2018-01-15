---
title: "Seguimiento y reproducción de eventos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
caps.latest.revision: "21"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6a5501861717bf21e6004730b38f93b309c40e0e
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2018
---
# <a name="tracing-and-replaying-events"></a>Seguimiento y reproducción de eventos
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  En SMO, el **seguimiento** y **reproducción** objetos en el <xref:Microsoft.SqlServer.Management.Trace> espacio de nombres proporcionan acceso mediante programación a la [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] funcionalidad, que se usa para supervisar una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Puede capturar y guardar datos acerca de cada evento en un archivo o en una tabla para analizarlos posteriormente. Por ejemplo, puede supervisar un entorno de producción para ver qué procedimientos almacenados afectan negativamente al rendimiento al ejecutarse demasiado lentamente.  
  
 El **seguimiento** y **reproducción** objetos proporcionan un conjunto de objetos que puede usarse para crear seguimientos en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Puede utilizar estos objetos desde sus propias aplicaciones para crear seguimientos manualmente para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Además, SMO **seguimiento** objetos se pueden usar para leer los archivos de seguimiento de SQL y las tablas que se crearon mediante la supervisión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], o el registro de DTS.  
  
 Los objetos **Trace** de SMO permiten realizar las funciones siguientes:  
  
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
  
 Los datos de seguimiento de la **seguimiento** y **reproducción** objetos se puedan usar la aplicación SMO o se pueden examinar manualmente utilizando [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md). Los datos de seguimiento también son compatibles con el [SQL Trace](../../../relational-databases/sql-trace/sql-trace.md) procedimientos almacenados que también proporcionan funciones de seguimiento.  
  
 Los objetos de seguimiento de SMO residen en el espacio de nombres <xref:Microsoft.SqlServer.Management.Trace>, que requiere una referencia al archivo Microsoft.SQLServer.ConnectionInfo.dll.  
  
 El **seguimiento** y **reproducción** objetos requieren un [ServerConnection](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.common.serverconnection.aspx) <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> objeto que se va a establecer una conexión con la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El [ServerConnection](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.common.serverconnection.aspx) objeto se encuentra en la [Microsoft.SqlServer.Management.Common](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.common) espacio de nombres, que requiere una referencia al archivo Microsoft.SQLServer.ConnectionInfo.dll.  
  
> [!NOTE]  
>  Los objetos **Trace** y **Replay** no se pueden utilizar en una plataforma de 64 bits.  
  
  
