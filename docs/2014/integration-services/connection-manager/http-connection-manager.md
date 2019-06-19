---
title: Administrador de conexiones HTTP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- HTTP connection manager
- Web site connections [Integration Services]
- connection managers [Integration Services], HTTP
- Web server connections [Integration Services]
- connections [Integration Services], HTTP
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f79a882e3a3e4520cb8cfcd4468f3c908b79abf5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833763"
---
# <a name="http-connection-manager"></a>HTTP, administrador de conexiones
  Una conexión HTTP habilita a un paquete para obtener acceso a un servidor web mediante HTTP para enviar o recibir archivos. La tarea Servicio web que incluye [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa este administrador de conexiones.  
  
 Cuando agrega un administrador de conexiones HTTP a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión HTTP en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección `Connections` del paquete.  
  
 El `ConnectionManagerType` propiedad del Administrador de conexiones se establece en `HTTP.`  
  
 Puede configurar el administrador de conexiones HTTP de las maneras siguientes:  
  
-   Utilizar credenciales. Si el administrador de conexiones usa credenciales, sus propiedades incluyen el nombre de usuario, contraseña y dominio.  
  
    > [!IMPORTANT]  
    >  El administrador de conexiones HTTP solo es compatible con la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
-   Utilizar un certificado de cliente. Si el administrador de conexiones usa un certificado de cliente, sus propiedades incluyen el nombre de certificado.  
  
-   Proporcionar un tiempo de espera para conectarse al servidor y un tamaño de fragmento para escribir datos.  
  
-   Utilizar un servidor proxy. El servidor proxy también se puede configurar para usar credenciales y para omitir el servidor proxy y usar direcciones locales en su lugar.  
  
## <a name="configuration-of-the-http-connection-manager"></a>Configuración del administrador de conexiones HTTP  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor del administrador de conexiones HTTP &#40;página Servidor&#41;](../http-connection-manager-editor-server-page.md)  
  
-   [Editor del administrador de conexiones HTTP &#40;página Proxy&#41;](../http-connection-manager-editor-proxy-page.md)  
  
 Para más información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>.  
  
## <a name="see-also"></a>Vea también  
 [Tarea Servicio web](../control-flow/web-service-task.md)   
 [Conexiones de Integration Services &#40;SSIS&#41;](integration-services-ssis-connections.md)  
  
  
