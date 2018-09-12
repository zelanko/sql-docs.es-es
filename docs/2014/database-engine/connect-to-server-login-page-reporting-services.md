---
title: Conectar con el servidor (página Inicio de sesión de Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttors.login.f1
helpviewer_keywords:
- Connect to Server dialog box, Reporting Services
ms.assetid: d312c740-19d7-4931-84a2-88b805ec8439
caps.latest.revision: 28
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d6035f7f05a8687290cfb388cbf47dbc5222376
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43809261"
---
# <a name="connect-to-server-login-page-reporting-services"></a>Conectar al servidor (página Inicio de sesión de Reporting Services)
  Use esta pestaña para ver o especificar las siguientes opciones cuando se conecte a [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
 **Tipo de servidor**  
 Al registrar un servidor desde el Explorador de objetos, seleccione el tipo de servidor al que conectarse: [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services o Integration Services. El resto del cuadro de diálogo muestra simplemente las opciones que se aplican al tipo de servidor seleccionado. Cuando se registra un servidor desde Servidores registrados, el cuadro **Tipo de servidor** es de solo lectura y coincide con el tipo de servidor que se muestra en el componente Servidores registrados. Para registrar un tipo distinto de servidor, seleccione [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services o Integration Services desde la barra de herramientas Servidores registrados antes de comenzar a registrar un servidor nuevo.  
  
 **Nombre del servidor**  
 El modo de servidor de la instancia del servidor de informes al que se está conectando determina el valor que debe especificar.  
  
 En un servidor de informes que se ejecute en modo nativo, especifique la instancia del servidor de informes a la que conectarse. Si utiliza la instancia predeterminada, el nombre del servidor suele ser el nombre del equipo. Si ha instalado una instancia con nombre, anexe el nombre de instancia al nombre del servidor en este formato: \<servername >\\< nombreDeInstancia\>. Reporting Services usa el carácter de barra diagonal inversa para delimitar el nombre de instancia.  
  
 Con un servidor de informes que se ejecute en el modo integrado de SharePoint, debe especificar un sitio de SharePoint. Puede especificar un sitio de una colección de sitios que esté integrada con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. La dirección URL que proporcione debe incluir el prefijo HTTP o HTTPS. Debe disponer de permiso para tener acceso al sitio de SharePoint con el fin de conectarse a él en Management Studio. El nivel de permisos que se le asigne determinará qué elementos puede ver y administrar. Para obtener más información, consulte [conectarse a un servidor de informes en Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md).  
  
 **Autenticación**  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se puede configurar para aceptar solicitudes de autenticación de Windows o solicitudes de autenticación de formularios que son administradas mediante la extensión de autenticación personalizada que proporcione. Seleccione uno de los siguientes modos de autenticación al conectarse a Reporting Services:  
  
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
  
 **Recordar contraseña**  
 Guarda la contraseña que ha escrito. Esta opción solo se muestra al hacer clic en **Opciones**y solo puede modificarse si ha optado por establecer la conexión mediante **Autenticación básica** o **Autenticación de formularios**.  
  
 **Conectar**  
 Se conecta al servidor seleccionado.  
  
 **Opciones**  
 Muestra opciones de conexión al servidor adicionales, tales como recordar la contraseña.  
  
## <a name="see-also"></a>Vea también  
 [Configurar una conexión de base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Conectar con un servidor de informes en Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Autenticación con el servidor de informes](../reporting-services/security/authentication-with-the-report-server.md)  
  
  
