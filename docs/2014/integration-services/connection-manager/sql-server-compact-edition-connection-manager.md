---
title: Administrador de conexiones con SQL Server Compact Edition | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Compact, connection manager
- connections [Integration Services], SQL Server Compact
- connection managers [Integration Services], SQL Server Compact
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 752c825cb34fbf2afe5d2306afbd562a49f74b7f
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58384733"
---
# <a name="sql-server-compact-edition-connection-manager"></a>Administrador de conexiones con SQL Server Compact Edition
  Un administrador de conexiones con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact habilita un paquete para establecer conexión con una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact. El destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye usa este administrador de conexiones para cargar datos en una tabla de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
> [!NOTE]  
>  En un equipo de 64 bits, necesita ejecutar paquetes que se conecten a los orígenes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact en modo de 32 bits. El proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact que usa [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para establecer conexión con orígenes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact solo está disponible en una versión de 32 bits.  
  
## <a name="configuration-the-sql-server-compact-edition-connection-manager"></a>Configuración del administrador de conexiones con SQL Server Compact Edition  
 Cuando se agrega un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Administrador de conexiones Compact a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una conexión de administrador que se resuelve como un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexión Compact en tiempo de ejecución, Establece las propiedades del Administrador de la conexión y agrega el Administrador de conexiones a la `Connections` colección en el paquete.  
  
 La propiedad `ConnectionManagerType` del administrador de conexiones se establece en `SQLMOBILE`.  
  
 Puede configurar el administrador de conexiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact de las maneras siguientes:  
  
-   Proporcionar una cadena de conexión que especifica la ubicación de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
-   Proporcionar una contraseña para una base de datos protegida por contraseña.  
  
-   Especificar el servidor en el que se va a almacenar la base de datos.  
  
-   Indicar si la conexión creada desde el administrador de conexiones se conserva en el tiempo de ejecución.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor del administrador de conexiones con SQL Server Compact Edition &#40;página Conexión&#41;](../sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
-   [Editor del administrador de conexiones con SQL Server Compact Edition &#40;página Todo&#41;](../sql-server-compact-edition-connection-manager-editor-all-page.md)  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
