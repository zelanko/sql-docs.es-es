---
title: Administrador de conexiones SMO | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.smoconnection.f1
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eace0d881304757c067c95a30fadb2bc0e960641
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="smo-connection-manager"></a>SMO, administrador de conexiones
  Un administrador de conexiones SMO permite a un paquete conectarse a un servidor de Objeto de administración de SQL (SMO). Las tareas de transferencia que incluye [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usan un administrador de conexiones SMO. Por ejemplo, la tarea Transferir inicios de sesión que transfiere inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa un administrador de conexiones SMO.  
  
 Cuando agrega un administrador de conexiones SMO a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión SMO en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Conexiones** del paquete. La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **SMOServer**.  
  
 Puede configurar el administrador de conexiones SMO de las maneras siguientes:  
  
-   Especificar el nombre de un servidor en el que está instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Seleccionar el modo de autenticación para conectarse al servidor.  
  
## <a name="configuration-of-the-smo-connection-manager"></a>Configuración del administrador de conexiones SMO  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para más información sobre las propiedades que puede configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Editor del administrador de conexiones SMO](../../integration-services/connection-manager/smo-connection-manager-editor.md).  
  
 Para más información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="smo-connection-manager-editor"></a>administrador de conexiones SMO, editor del
  Utilice el **Editor del administrador de conexiones SMO** para configurar una conexión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para las diferentes tareas que transfieren objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obtener más información acerca del administrador de conexiones SMO, vea [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Nombre del servidor**  
 Escriba el nombre de la sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o seleccione el nombre de servidor en la lista.  
  
 **Actualizar**  
 Actualiza la lista de sesiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponibles que se pueden detectar en la red.  
  
 **Utilizar autenticación de Windows**  
 Utiliza la autenticación de Windows para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seleccionada.  
  
 **Utilizar autenticación de SQL Server**  
 Utiliza la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seleccionada.  
  
 **Nombre de usuario.**  
 Si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , escriba el nombre de usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Contraseña**  
 Si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , escriba la contraseña.  
  
 **Probar conexión**  
 Pruebe la conexión con la configuración establecida.  
  
## <a name="see-also"></a>Vea también  
 [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
