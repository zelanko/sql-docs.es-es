---
title: "Administrador de conexiones HTTP | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "HTTP, administrador de conexiones"
  - "sitio web, conexiones [Integration Services]"
  - "administradores de conexión [Integration Services], HTTP"
  - "servidor web, conexiones [Integration Services]"
  - "conexiones [Integration Services], HTTP"
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# Administrador de conexiones HTTP
  Una conexión HTTP habilita a un paquete para obtener acceso a un servidor web mediante HTTP para enviar o recibir archivos. La tarea Servicio web que incluye [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa este administrador de conexiones.  
  
 Cuando agrega un administrador de conexiones HTTP a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión HTTP en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Conexiones** del paquete.  
  
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **HTTP.**.  
  
 Puede configurar el administrador de conexiones HTTP de las maneras siguientes:  
  
-   Utilizar credenciales. Si el administrador de conexiones usa credenciales, sus propiedades incluyen el nombre de usuario, contraseña y dominio.  
  
    > [!IMPORTANT]  
    >  El administrador de conexiones HTTP solo es compatible con la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
-   Utilizar un certificado de cliente. Si el administrador de conexiones usa un certificado de cliente, sus propiedades incluyen el nombre de certificado.  
  
-   Proporcionar un tiempo de espera para conectarse al servidor y un tamaño de fragmento para escribir datos.  
  
-   Utilizar un servidor proxy. El servidor proxy también se puede configurar para usar credenciales y para omitir el servidor proxy y usar direcciones locales en su lugar.  
  
## Configuración del administrador de conexiones HTTP  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor del administrador de conexiones HTTP &#40;página Servidor&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
-   [Editor del administrador de conexiones HTTP &#40;página Proxy&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)  
  
 Para más información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>.  
  
## Vea también  
 [Tarea Servicio web](../../integration-services/control-flow/web-service-task.md)   
 [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  