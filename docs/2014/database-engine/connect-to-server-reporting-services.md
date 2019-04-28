---
title: Conectar con el servidor (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connection.login.reportserver.f1
ms.assetid: ef81b658-8eb5-4636-ac81-eead10cc7b9f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 41e0ca3ee7ccaa7bb57e5667092c0660e35c4c52
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62808684"
---
# <a name="connect-to-server-reporting-services"></a>Conectar al servidor (Reporting Services)
  Use este cuadro de diálogo para ver o especificar opciones cuando se conecte a [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
 **Tipo de servidor**  
 Al registrar un servidor desde el **Explorador de objetos**, seleccione el tipo de servidor al que conectarse: [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services o Integration Services. El resto del cuadro de diálogo muestra simplemente las opciones que se aplican al tipo de servidor seleccionado. Cuando se registra un servidor desde **Servidores registrados**, el cuadro **Tipo de servidor** es de solo lectura y coincide con el tipo de servidor que se muestra en el componente **Servidores registrados** . Para registrar un tipo distinto de servidor, seleccione [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services o Integration Services desde la barra de herramientas **Servidores registrados** antes de comenzar a registrar un servidor nuevo.  
  
 **Nombre del servidor**  
 El modo de servidor de la instancia del servidor de informes al que se está conectando determina el valor que debe especificar.  
  
 En un servidor de informes que se ejecute en modo nativo, especifique la instancia del servidor de informes a la que conectarse. Si utiliza la instancia predeterminada, el nombre del servidor suele ser el nombre del equipo. Si ha instalado una instancia con nombre, anexe el nombre de instancia al nombre del servidor en este formato: \<servername >\\< nombreDeInstancia\>. Reporting Services usa el carácter de barra diagonal inversa para delimitar el nombre de instancia.  
  
 Con un servidor de informes que se ejecute en el modo integrado de SharePoint, debe especificar un sitio de SharePoint. Puede especificar un sitio de una colección de sitios que esté integrada con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. La dirección URL que proporcione debe incluir el prefijo HTTP o HTTPS. Debe disponer de permiso para tener acceso al sitio de SharePoint con el fin de conectarse a él en Management Studio. El nivel de permisos que se le asigne determinará qué elementos puede ver y administrar. Para obtener más información, consulte [conectarse a un servidor de informes en Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md).  
  
 **Autenticación**  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se puede configurar para aceptar solicitudes de autenticación de Windows o solicitudes de autenticación de formularios que son administradas mediante la extensión de autenticación personalizada que proporcione. Seleccione uno de los siguientes modos de autenticación al conectarse a [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]:  
  
 **Modo de autenticación de Windows (autenticación de Windows)**  
 Se conecta a una instancia de servidor de informes usando sus credenciales de [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows.  
  
 **Autenticación básica**  
 Conéctese mediante la **Autenticación básica** si la instalación de Reporting Services está configurada para usar la Autenticación básica.  
  
 **Autenticación de formularios**  
 Conéctese mediante la **Autenticación de formularios** si la instalación de Reporting Services está configurada para usar una extensión de autenticación personalizada.  
  
 **Nombre de usuario**  
 Escriba el nombre de inicio de sesión que se va a usar en la conexión. Esta opción solo se encuentra disponible si ha seleccionado **Autenticación básica** o **Autenticación de formularios**.  
  
 **Contraseña**  
 Escriba la contraseña del nombre de usuario. Esta opción solo se puede editar si ha seleccionado **Autenticación básica** o **Autenticación de formularios**.  
  
 **Conectar**  
 Haga clic aquí para conectarse al servidor seleccionado anteriormente.  
  
 **Opciones**  
 Haga clic aquí para que se muestren las opciones adicionales de conexión al servidor, como registrar un servidor y recordar la contraseña.  
  
## <a name="see-also"></a>Vea también  
 [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Conectar con un servidor de informes en Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Autenticación con el servidor de informes](../reporting-services/security/authentication-with-the-report-server.md)  
  
  
