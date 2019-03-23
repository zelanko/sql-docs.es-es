---
title: Administrador de conexiones WMI | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5d57a0783c8af0121169f09622b8e5bd8547d1ad
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58386023"
---
# <a name="wmi-connection-manager"></a>Administrador de conexiones WMI
  Un administrador de conexiones WMI habilita un paquete para que use Instrumental de administración de Windows (WMI) para administrar información en un entorno de empresa. La tarea Servicio web que incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa un administrador de conexiones WMI.  
  
 Cuando se agrega un administrador de conexiones WMI a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una conexión de administrador que se resuelve como una conexión de WMI en tiempo de ejecución, Establece las propiedades del Administrador de la conexión y agrega el Administrador de conexiones para el `Connections` colección en el paquete . La propiedad `ConnectionManagerType` del administrador de conexiones se establece en `WMI`.  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>Configuración del administrador de conexiones WMI  
 Puede configurar el administrador de conexiones WMI de las maneras siguientes:  
  
-   Especificar el nombre de un servidor.  
  
-   Especificar un espacio de nombre en el servidor.  
  
-   Seleccionar el modo de autenticación para conectarse al servidor.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información sobre las propiedades que se pueden configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Editor del administrador de conexiones WMI](../wmi-connection-manager-editor.md).  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vea también  
 [Tarea Servicio web](../control-flow/web-service-task.md)   
 [Conexiones de Integration Services &#40;SSIS&#41;](integration-services-ssis-connections.md)  
  
  
