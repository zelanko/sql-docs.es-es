---
title: Editor del administrador de conexiones HTTP (página servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.httpconnection.server.f1
helpviewer_keywords:
- HTTP Connection Manager Editor
ms.assetid: 774778a0-ece6-4971-b93f-b121d8fc1fc1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 197a2668beb60acf2473a1f53786d7b553e08cf6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058252"
---
# <a name="http-connection-manager-editor-server-page"></a>Editor del administrador de conexiones HTTP (página Servidor)
  Utilice la pestaña **Servidor** del cuadro de diálogo **Editor del administrador de conexiones HTTP** para configurar el Administrador de conexiones HTTP especificando propiedades como la dirección URL y las credenciales de seguridad. Una conexión HTTP habilita a un paquete para obtener acceso a un servidor web mediante HTTP para enviar o recibir archivos. Después de configurar el Administrador de conexiones HTTP, también puede probar la conexión.  
  
> [!IMPORTANT]  
>  El administrador de conexiones HTTP solo es compatible con la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
 Para obtener más información acerca del administrador de conexiones HTTP, vea [HTTP Connection Manager](connection-manager/http-connection-manager.md). Para obtener más información acerca de un escenario común de uso para el Administrador de conexiones HTTP, vea [Web Service Task](control-flow/web-service-task.md).  
  
## <a name="options"></a>Opciones  
 **Dirección URL del servidor**  
 Escriba la dirección URL del servidor.  
  
 Si piensa utilizar el botón **Descargar WSDL** de la página **General** del **Editor de la tarea Servicio web** para descargar un archivo WSDL, escriba la dirección URL del archivo WSDL. Esta dirección URL finaliza con"?wsdl".  
  
 **Utilizar credenciales**  
 Especifique si desea que el Administrador de conexiones HTTP utilice las credenciales de seguridad del usuario para la autenticación.  
  
 **Nombre de usuario**  
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
  
 **Probar la conexión**  
 Después de configurar el Administrador de conexiones HTTP, haga clic en **Probar conexión**para confirmar que la conexión es viable.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor del administrador de conexiones HTTP &#40;página Proxy&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)  
  
  
