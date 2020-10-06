---
description: Administrador de conexiones WMI
title: Administrador de conexiones WMI | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.wmiconnection.f1
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bf98d6204a9c7794d9024e9289d81b2886e7cc53
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725931"
---
# <a name="wmi-connection-manager"></a>Administrador de conexiones WMI

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Un administrador de conexiones WMI habilita un paquete para que use Instrumental de administración de Windows (WMI) para administrar información en un entorno de empresa. La tarea Servicio web que incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa un administrador de conexiones WMI.  
  
 Cuando agrega un administrador de conexiones WMI a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión WMI en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Connections** del paquete. La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **WMI**.  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>Configuración del administrador de conexiones WMI  
 Puede configurar el administrador de conexiones WMI de las maneras siguientes:  
  
-   Especificar el nombre de un servidor.  
  
-   Especificar un espacio de nombre en el servidor.  
  
-   Seleccionar el modo de autenticación para conectarse al servidor.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información sobre las propiedades que se pueden configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Editor del administrador de conexiones WMI]().  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="wmi-connection-manager-editor"></a>Editor del administrador de conexiones WMI
  Use el cuadro de diálogo **Administrador de conexiones WMI** para especificar una conexión del Instrumental de administración de Microsoft Windows (WMI) a un servidor.  
  
 Para obtener más información acerca del administrador de conexiones WMI, vea [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Proporcione un nombre único para el administrador de conexiones.  
  
 **Descripción**  
 Describa el administrador de conexiones. Como método recomendado, describa el administrador de conexiones desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Nombre del servidor**  
 Proporcione el nombre del servidor con el que desea realizar la conexión WMI.  
  
 **Espacio de nombres**  
 Especifique el espacio de nombres WMI.  
  
 **Usar la autenticación de Windows**  
 Seleccione el uso de la autenticación de Windows. Si utiliza la autenticación de Windows, no será necesario que proporcione un nombre de usuario o una contraseña para la conexión.  
  
 **Nombre de usuario**  
 Si no utiliza la autenticación de Windows, deberá proporcionar un nombre de usuario para la conexión.  
  
 **Contraseña**  
 Si no utiliza la autenticación de Windows, deberá proporcionar la contraseña para la conexión.  
  
 **Prueba**  
 Permite probar la configuración del administrador de conexiones.  
  
## <a name="see-also"></a>Consulte también  
 [Tarea Servicio web](../../integration-services/control-flow/web-service-task.md)   
 [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)