---
title: Administrador de conexiones SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 32710f704e3d51d143e071178d690413735319f5
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380733"
---
# <a name="smo-connection-manager"></a>SMO, administrador de conexiones
  Un administrador de conexiones SMO permite a un paquete conectarse a un servidor de Objeto de administración de SQL (SMO). Las tareas de transferencia que incluye [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usan un administrador de conexiones SMO. Por ejemplo, la tarea Transferir inicios de sesión que transfiere inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa un administrador de conexiones SMO.  
  
 Cuando agrega un administrador de conexiones SMO a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión SMO en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección `Connections` del paquete. La propiedad `ConnectionManagerType` del administrador de conexiones se establece en `SMOServer`.  
  
 Puede configurar el administrador de conexiones SMO de las maneras siguientes:  
  
-   Especificar el nombre de un servidor en el que está instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Seleccionar el modo de autenticación para conectarse al servidor.  
  
## <a name="configuration-of-the-smo-connection-manager"></a>Configuración del administrador de conexiones SMO  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para más información sobre las propiedades que puede configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Editor del administrador de conexiones SMO](../smo-connection-manager-editor.md).  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vea también  
 [Conexiones de Integration Services &#40;SSIS&#41;](integration-services-ssis-connections.md)  
  
  
