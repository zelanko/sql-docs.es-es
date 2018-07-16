---
title: Administrador de conexiones FTP | Microsoft Docs
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
- FTP connection manager
- connections [Integration Services], FTP
- connection managers [Integration Services], FTP
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b22fbb63dda4b6e3211a5bb53cfd70e243e6960f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37193615"
---
# <a name="ftp-connection-manager"></a>FTP, administrador de conexiones
  Un administrador de conexiones FTP habilita un paquete para conectarse a un servidor de Protocolo de transferencia de archivos (FTP). La tarea FTP que incluye [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa este administrador de conexiones.  
  
 Cuando agrega un Administrador de conexiones FTP a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se puede resolver como una conexión FTP en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección `Connections` del paquete.  
  
 El `ConnectionManagerType` propiedad del Administrador de conexiones se establece en `FTP`.  
  
 Puede configurar el administrador de conexiones FTP de las maneras siguientes:  
  
-   Especificar un nombre de servidor y puerto de servidor.  
  
-   Especificar un acceso anónimo, o proporcionar un nombre de usuario y una contraseña para la autenticación básica.  
  
    > [!IMPORTANT]  
    >  El administrador de conexiones FTP solo admite la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
-   Establecer el tiempo de espera, el número de reintentos y la cantidad de datos que se pueden copiar simultáneamente.  
  
-   Indicar si el administrador de conexiones FTP usa el modo pasivo o activo.  
  
 Según la configuración del sitio FTP al que se conecta el administrador de conexiones FTP, es posible que necesite cambiar los siguientes valores predeterminados del administrador de conexiones:  
  
-   El puerto del servidor se establece en 21. Debe especificar el puerto que escucha el sitio FTP.  
  
-   El nombre del usuario se establece en "anónimo". Debe proporcionar las credenciales que requiere el sitio FTP.  
  
## <a name="activepassive-modes"></a>Modos activo/pasivo  
 Un administrador de conexiones FTP puede enviar y recibir archivos con el modo activo o modo pasivo. En el modo activo, el servidor inicia la conexión de datos, mientras que en el modo pasivo, la inicia el cliente.  
  
## <a name="configuration-of-the-ftp-connection-manager"></a>Configuración del administrador de conexiones FTP  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información sobre las propiedades que se pueden configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Editor del administrador de conexiones FTP](../ftp-connection-manager-editor.md).  
  
 Para obtener información acerca de cómo configurar un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vea también  
 [Tarea FTP](../control-flow/ftp-task.md)   
 [Servicios de integración &#40;SSIS&#41; conexiones](integration-services-ssis-connections.md)  
  
  
