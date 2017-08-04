---
title: Administrador de conexiones WMI | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d8bd256a462a8a0a51441024619f2ed81f6db753
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="wmi-connection-manager"></a>Administrador de conexiones WMI
  Un administrador de conexiones WMI habilita un paquete para que use Instrumental de administración de Windows (WMI) para administrar información en un entorno de empresa. La tarea Servicio web que incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa un administrador de conexiones WMI.  
  
 Cuando agrega un administrador de conexiones WMI a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión WMI en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Connections** del paquete. La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **WMI**.  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>Configuración del administrador de conexiones WMI  
 Puede configurar el administrador de conexiones WMI de las maneras siguientes:  
  
-   Especificar el nombre de un servidor.  
  
-   Especificar un espacio de nombre en el servidor.  
  
-   Seleccionar el modo de autenticación para conectarse al servidor.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información sobre las propiedades que se pueden configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Editor del administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md).  
  
 Para más información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vea también  
 [Tarea Servicio web](../../integration-services/control-flow/web-service-task.md)   
 [Integration Services &#40; SSIS &#41; Conexiones](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
