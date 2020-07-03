---
title: Seguimiento y reproducción de eventos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c6a164927ed5a6dd711dc6d2243dd3b96c85ca08
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896315"
---
# <a name="tracing-and-replaying-events"></a>Seguimiento y reproducción de eventos
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw.md)]

  En SMO, los objetos **Trace** y **Replay** del espacio de <xref:Microsoft.SqlServer.Management.Trace> nombres proporcionan acceso mediante programación a la [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] funcionalidad, que se usa para supervisar una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Puede capturar y guardar datos acerca de cada evento en un archivo o en una tabla para analizarlos posteriormente. Por ejemplo, puede supervisar un entorno de producción para ver qué procedimientos almacenados afectan negativamente al rendimiento al ejecutarse demasiado lentamente.  
  
 Los objetos **Trace** y **Replay** proporcionan un conjunto de objetos que se pueden utilizar para crear seguimientos en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Puede utilizar estos objetos desde sus propias aplicaciones para crear seguimientos manualmente para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Además, los objetos de **seguimiento** de SMO se pueden usar para leer los archivos de seguimiento de SQL y las tablas que se crearon mediante la supervisión [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o el registro de DTS.  
  
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
  
 La aplicación SMO puede utilizar los datos de seguimiento de los objetos **Trace** y **Replay** o estos datos se pueden examinar manualmente utilizando [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md). Los datos de seguimiento también son compatibles con los procedimientos almacenados de [SQL Trace](../../../relational-databases/sql-trace/sql-trace.md) que también proporcionan funciones de seguimiento.  
  
 Los objetos de seguimiento de SMO residen en el espacio de nombres <xref:Microsoft.SqlServer.Management.Trace>, que requiere una referencia al archivo Microsoft.SQLServer.ConnectionInfo.dll.  
  
 Los objetos **Trace** y **Replay** requieren un objeto [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> para establecer una conexión con la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . El objeto [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) se encuentra en el espacio de nombres [Microsoft. SqlServer. Management. Common](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common) , que requiere una referencia al archivo Microsoft.SQLServer.ConnectionInfo.dll.  
  
> [!NOTE]  
>  Los objetos **Trace** y **Replay** no se pueden utilizar en una plataforma de 64 bits.  
  
  
