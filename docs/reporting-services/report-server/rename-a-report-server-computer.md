---
title: Cambiar el nombre de un equipo de servidor de informes | Documentos de Microsoft
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- renaming report servers
ms.assetid: 82fc4ba2-291a-4939-a025-271b8d687c54
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 349180bb3cfe2b03bee076dfc2dbb90265118fa4
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="rename-a-report-server-computer"></a>Cambiar el nombre de un equipo que ejecuta un servidor de informes
  Al cambiar el nombre de un equipo, también se cambia el nombre correspondiente del servidor web y de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (si está en el mismo equipo). En algunos casos, puede que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no esté accesible después de un cambio en el nombre de equipo. Siga los pasos que aparecen en este tema para volver a configurar un servidor de informes después de haber cambiado el nombre de un equipo.  
  
## <a name="renaming-a-sql-server-database-engine"></a>Cambiar el nombre de un motor de base de datos de SQL Server  
 Si cambia el nombre de la instancia de  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que ejecuta la base de datos del servidor de informes, haga lo siguiente:  
  
1.  Inicie la herramienta de configuración de Reporting Services y conéctese al servidor de informes que utiliza la base de datos en el servidor de informes que ha cambiado de nombre.  
  
2.  Abra la página Instalación de base de datos.  
  
3.  En **Nombre del servidor**, escriba o seleccione el nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y, a continuación, haga clic en **Conectar**.  
  
4.  Haga clic en **Aplicar**.  
  
 Si el servidor de informes usa una instancia local de [!INCLUDE[ssDE](../../includes/ssde-md.md)] , puede usar *(local)* o *(local)\nombreDeInstancia* para especificar el servidor. Si usa *(local)* para referirse al servidor, puede cambiar el nombre del servidor y las conexiones continuarán funcionando. Si usa un servidor remoto o se ha configurado [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con el nombre del servidor, debe actualizar la información de conexión de la base de datos siempre que cambie el nombre del servidor.  
  
## <a name="renaming-a-report-server-computer"></a>Cambiar el nombre de un equipo que ejecuta un servidor de informes  
 Si cambia el nombre de un equipo que ejecuta un servidor de informes, haga lo siguiente:  
  
1.  Abra el archivo RSReportServer.config en un editor de texto y cambie la configuración de **UrlRoot** para que refleje el nuevo nombre del servidor. La extensiones de entrega utilizan el valor **UrlRoot** para crear la dirección URL utilizada para obtener acceso a elementos almacenados en el servidor de informes. Cambiar la dirección URL del servidor requiere actualizar la configuración de **UrlRoot** para que las suscripciones sigan entregando informes correctamente.  
  
2.  En el mismo archivo, si se establece, modifique el valor **ReportServerUrl** para reflejar el nuevo nombre del servidor. Observe que esta configuración no se utiliza en todas las instalaciones. Si está en blanco, no haga nada.  
  
    > [!NOTE]  
    >  Si utiliza el Servicio de nombres Internet de Windows (WINS) en su red corporativa, el servidor de informes y el Administrador de informes continuarán estando disponibles con el nombre anterior durante algún tiempo. WINS asigna una dirección IP a cada uno de los equipos a los que sirve. Después de que WINS actualice la dirección IP para el equipo que ha cambiado de nombre, el nombre antiguo no podrá utilizarse para obtener acceso a un servidor de informes ni al Administrador de informes.  
  
## <a name="see-also"></a>Vea también  
 [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services Configuration Manager &#40; Modo nativo &#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Informes de servidor de informes de servicios &#40; Modo nativo &#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Iniciar y detener el servicio de servidor de informes](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)   
 [rsconfig (utilidad) &#40; SSRS &#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)  
  
  
