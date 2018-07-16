---
title: Administrador de conexiones SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 85639e416be3870a52a9d44284534f080c62a1a9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37292905"
---
# <a name="smo-connection-manager"></a>SMO, administrador de conexiones
  Un administrador de conexiones SMO permite a un paquete conectarse a un servidor de Objeto de administración de SQL (SMO). Las tareas de transferencia que incluye [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usan un administrador de conexiones SMO. Por ejemplo, la tarea Transferir inicios de sesión que transfiere inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa un administrador de conexiones SMO.  
  
 Cuando se agrega un administrador de conexiones SMO a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una conexión de administrador que se resuelve como una conexión SMO en tiempo de ejecución, Establece las propiedades del Administrador de la conexión y agrega el Administrador de conexiones para el `Connections` colección en el paquete. El `ConnectionManagerType` propiedad del Administrador de conexiones se establece en `SMOServer`.  
  
 Puede configurar el administrador de conexiones SMO de las maneras siguientes:  
  
-   Especificar el nombre de un servidor en el que está instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Seleccionar el modo de autenticación para conectarse al servidor.  
  
## <a name="configuration-of-the-smo-connection-manager"></a>Configuración del administrador de conexiones SMO  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para más información sobre las propiedades que puede configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Editor del administrador de conexiones SMO](../smo-connection-manager-editor.md).  
  
 Para obtener información acerca de cómo configurar un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vea también  
 [Servicios de integración &#40;SSIS&#41; conexiones](integration-services-ssis-connections.md)  
  
  
