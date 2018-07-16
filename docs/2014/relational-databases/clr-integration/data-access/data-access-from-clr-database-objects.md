---
title: Acceso a datos desde objetos de base de datos CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], data access
- routines [CLR integration]
- data access [CLR integration]
- ADO.NET [CLR integration]
- internal data access [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], data access
- managed code [SQL Server], database objects
- .NET Data Access Provider for SQL Server [CLR integration]
- managed code [SQL Server], data access
- SqlClient provider
- in-process data access providers [CLR integration]
ms.assetid: 9a0f4dee-71c1-42e9-a85e-52382807010f
caps.latest.revision: 41
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1c49134c931bc9f27e7c4856ce23ccde70364000
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37351147"
---
# <a name="data-access-from-clr-database-objects"></a>Acceso a datos de objetos de base de datos de CLR
  Una rutina de common language runtime (CLR) puede acceder fácilmente a los datos almacenados en la instancia de [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] en que se ejecuta, así como los datos almacenados en instancias remotas. El contexto del usuario en el que se ejecuta el código, determina los datos concretos a los que la rutina puede tener acceso. Acceso a datos desde dentro de un objeto de base de datos CLR mediante el proveedor de datos de .NET Framework para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datos de cliente administrado y las aplicaciones de nivel intermedio. Debido a esto, puede aprovechar sus conocimientos de ADO.NET y `SqlClient` en aplicaciones cliente y de nivel medio.  
  
> [!NOTE]  
>  De forma predeterminada, los métodos de tipo definido por el usuario y funciones definidas por el usuario no pueden tener acceso a datos. Debe establecer la propiedad `DataAccess` de `SqlMethodAttribute` o `SqlFunctionAttribute` en `DataAccessKind.Read` para habilitar el acceso a datos de solo lectura desde métodos de tipo definido por el usuario (UDT) o funciones definidas por el usuario. Las operaciones de modificación de datos o las funciones definidas por el usuario no se permiten desde los UDT y, si se intentan producen excepciones en tiempo de ejecución.  
  
 En esta sección únicamente se discuten las diferencias de funcionalidad y de comportamiento concretas cuando se tiene acceso a los datos desde un objeto de base de datos de CLR. Para obtener más información acerca de las características y funcionalidad de ADO.NET, vea la documentación de ADO.NET que se incluye en .NET Framework SDK.  
  
 En la siguiente tabla se muestran los temas de esta sección.  
  
 [Conexión de contexto](context-connection.md)  
 Describe la conexión de contexto a SQL Server.  
  
 [Suplantación y credenciales para conexiones](impersonation-and-credentials-for-connections.md)  
 Describe la suplantación de conexiones y las credenciales de conexión.  
  
 [Extensiones específicas en proceso de SQL Server a ADO.NET](../../clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
 Describe los objetos concretos en proceso `SqlPipe`, `SqlContext`, `SqlTriggerContext` y `SqlDataRecord`.  
  
 [Integración CLR y transacciones](../../native-client-ole-db-transactions/transactions.md)  
 Describe cómo se integra el nuevo marco de transacciones que se proporciona en el espacio de nombres System.Transactions con ADO.NET y con la integración CLR de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Serialización XML de objetos de base de datos de CLR](../../../database-engine/dev-guide/xml-serialization-from-clr-database-objects.md)  
 Explica cómo habilitar escenarios de serialización XML de objetos de base de datos de CLR en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
  
