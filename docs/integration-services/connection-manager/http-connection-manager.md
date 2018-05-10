---
title: Administrador de conexiones HTTP | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.httpconnection.server.f1
- sql13.dts.designer.httpconnection.proxy.f1
helpviewer_keywords:
- HTTP connection manager
- Web site connections [Integration Services]
- connection managers [Integration Services], HTTP
- Web server connections [Integration Services]
- connections [Integration Services], HTTP
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3e80ca7ecf409f201a3d29904cb8693828a7c3ad
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="http-connection-manager"></a>HTTP, administrador de conexiones
  Una conexión HTTP habilita a un paquete para obtener acceso a un servidor web mediante HTTP para enviar o recibir archivos. La tarea Servicio web que incluye [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa este administrador de conexiones.  
  
 Cuando agrega un administrador de conexiones HTTP a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión HTTP en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Conexiones** del paquete.  
  
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **HTTP**.  
  
 Puede configurar el administrador de conexiones HTTP de las maneras siguientes:  
  
-   Utilizar credenciales. Si el administrador de conexiones usa credenciales, sus propiedades incluyen el nombre de usuario, contraseña y dominio.  
  
    > [!IMPORTANT]  
    >  El administrador de conexiones HTTP solo es compatible con la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
-   Utilizar un certificado de cliente. Si el administrador de conexiones usa un certificado de cliente, sus propiedades incluyen el nombre de certificado.  
  
-   Proporcionar un tiempo de espera para conectarse al servidor y un tamaño de fragmento para escribir datos.  
  
-   Utilizar un servidor proxy. El servidor proxy también se puede configurar para usar credenciales y para omitir el servidor proxy y usar direcciones locales en su lugar.  
  
## <a name="configuration-of-the-http-connection-manager"></a>Configuración del administrador de conexiones HTTP  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para más información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>.  
  
## <a name="http-connection-manager-editor-server-page"></a>Editor del administrador de conexiones HTTP (página Servidor)
  Utilice la pestaña **Servidor** del cuadro de diálogo **Editor del administrador de conexiones HTTP** para configurar el Administrador de conexiones HTTP especificando propiedades como la dirección URL y las credenciales de seguridad. Una conexión HTTP habilita a un paquete para obtener acceso a un servidor web mediante HTTP para enviar o recibir archivos. Después de configurar el Administrador de conexiones HTTP, también puede probar la conexión.  
  
> [!IMPORTANT]  
>  El administrador de conexiones HTTP solo es compatible con la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
 Para obtener más información acerca del administrador de conexiones HTTP, vea [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md). Para obtener más información acerca de un escenario común de uso para el Administrador de conexiones HTTP, vea [Web Service Task](../../integration-services/control-flow/web-service-task.md).  
  
### <a name="options"></a>Opciones  
 **Dirección URL del servidor**  
 Escriba la dirección URL del servidor.  
  
 Si piensa utilizar el botón **Descargar WSDL** de la página **General** del **Editor de la tarea Servicio web** para descargar un archivo WSDL, escriba la dirección URL del archivo WSDL. Esta dirección URL finaliza con"?wsdl".  
  
 **Utilizar credenciales**  
 Especifique si desea que el Administrador de conexiones HTTP utilice las credenciales de seguridad del usuario para la autenticación.  
  
 **User name**  
 Si el Administrador de conexiones HTTP utiliza credenciales, debe especificar un nombre de usuario, una contraseña y un dominio.  
  
 **Contraseña**  
 Si el Administrador de conexiones HTTP utiliza credenciales, debe especificar un nombre de usuario, una contraseña y un dominio.  
  
 **Dominio**  
 Si el Administrador de conexiones HTTP utiliza credenciales, debe especificar un nombre de usuario, una contraseña y un dominio.  
  
 **Utilizar certificado de cliente**  
 Especifique si desea que el Administrador de conexiones HTTP utilice un certificado de cliente para la autenticación.  
  
 **Certificado**  
 Seleccione un certificado de la lista mediante el cuadro de diálogo **Seleccionar certificado** . El cuadro de texto muestra el nombre asociado con este certificado.  
  
 **Tiempo de espera (en segundos)**  
 Indique un tiempo de espera para conectar con el servidor web. El valor predeterminado de esta propiedad es 30 segundos.  
  
 **Tamaño del fragmento (en KB)**  
 Indique un tamaño de fragmento para escribir datos.  
  
 **Probar conexión**  
 Después de configurar el Administrador de conexiones HTTP, haga clic en **Probar conexión**para confirmar que la conexión es viable.  
  
## <a name="http-connection-manager-editor-proxy-page"></a>Editor del administrador de conexiones HTTP (página Proxy)
  Utilice la pestaña **Proxy** del cuadro de diálogo **Editor del administrador de conexiones HTTP** para configurar el Administrador de conexiones HTTP para que utilice un servidor proxy. Una conexión HTTP habilita a un paquete para obtener acceso a un servidor web mediante HTTP para enviar o recibir archivos.  
  
 Para obtener más información acerca del administrador de conexiones HTTP, vea [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md). Para obtener más información acerca de un escenario común de uso para el Administrador de conexiones HTTP, vea [Web Service Task](../../integration-services/control-flow/web-service-task.md).  
  
### <a name="options"></a>Opciones  
 **Utilizar proxy**  
 Especifique si desea que el Administrador de conexiones HTTP se conecte a través de un servidor proxy.  
  
 **Dirección URL de proxy**  
 Escriba la dirección URL para el servidor de proxy.  
  
 **No usar servidor proxy en el equipo local**  
 Especifique si desea que el Administrador de conexiones HTTP no utilice el servidor proxy para direcciones locales.  
  
 **Utilizar credenciales**  
 Especifique si desea que el Administrador de conexiones HTTP utilice credenciales de seguridad para el servidor proxy.  
  
 **User name**  
 Si el Administrador de conexiones HTTP utiliza credenciales, debe especificar un nombre de usuario, una contraseña y un dominio.  
  
 **Contraseña**  
 Si el Administrador de conexiones HTTP utiliza credenciales, debe especificar un nombre de usuario, una contraseña y un dominio.  
  
 **Dominio**  
 Si el Administrador de conexiones HTTP utiliza credenciales, debe especificar un nombre de usuario, una contraseña y un dominio.  
  
 **Lista de omisión de proxy**  
 Lista de direcciones para la que desea omitir el servidor proxy.  
  
 **Agregar**  
 Escriba una dirección para la que no desee utilizar el servidor proxy.  
  
 **Quitar**  
 Seleccione una dirección y quítela haciendo clic en **Quitar**.  
  
## <a name="see-also"></a>Ver también  
 [Tarea Servicio web](../../integration-services/control-flow/web-service-task.md)   
 [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
