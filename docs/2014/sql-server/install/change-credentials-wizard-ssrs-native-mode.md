---
title: Asistente para cambiar credenciales (modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.changecredentialswizard.F1
helpviewer_keywords:
- Change Credentials Wizard
- report server database, reconfigure
ms.assetid: 9eb4060a-9c3e-41e0-8767-3cfaebc45de7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 632cfe6f1ea61612f59225f38a665ef73da0d898
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078503"
---
# <a name="change-credentials-wizard-ssrs-native-mode"></a>Asistente para cambiar credenciales (Modo nativo de SSRS)
  El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona el Asistente para cambiar credenciales. Este asistente actúa como guía por los pasos necesarios para reconfigurar la cuenta que el servidor de informes usa para conectar con la base de datos del servidor de informes. Al cambiar las credenciales, el Administrador de configuración actualizará todos los permisos y la información de inicio de sesión de base de datos en el servidor de bases de datos correspondiente a la base de datos que usa activamente el servidor de informes.  
  
 Para iniciar el asistente, haga clic en **Cambiar credenciales** en la página de base de datos en el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. Para obtener instrucciones sobre cómo iniciar el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, vea [Reporting Services Configuration Manager &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="options"></a>Opciones  
 **Servidor de base de datos**  
 Especifica el nombre de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instancia que se ejecuta la base de datos del servidor de informes.  
  
 Para conectarse a la [!INCLUDE[ssDE](../../includes/ssde-md.md)] instancia, debe usar las credenciales que tienen permiso para iniciar sesión en el servidor y actualizar la información de base de datos. El [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager usa las credenciales de Windows actuales, pero si no tiene los permisos de inicio de sesión o la base de datos, puede especificar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión de base de datos.  
  
 No puede especificar credenciales de Windows diferentes. Si desea conectarse como un usuario de Windows diferente, inicie sesión como ese usuario y, a continuación, inicie el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager.  
  
 **Credenciales**  
 Especifica la cuenta con la que el servidor de informes se conecta a la base de datos del servidor de informes. Los valores válidos incluyen la cuenta de servicio del servicio Web del servidor de informes, un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión de base de datos definido en el [!INCLUDE[ssDE](../../includes/ssde-md.md)] instancia que se usa para hospedar el servidor de informes o una cuenta de Windows. Si usa una cuenta de Windows, puede especificar una cuenta local (*\<nombreDeEquipo >\\< nombre de usuario\>*) si el servidor de informes y la base de datos están en el mismo equipo o un usuario de dominio cuenta (*\<dominio >\\< nombre de usuario\>*) si están en equipos diferentes en el mismo dominio.  
  
 El servidor de informes creará un inicio de sesión de base de datos y asignará permisos de base de datos a la cuenta que especifique.  
  
 El servidor de informes no crea la propia cuenta. La cuenta que especifique ya debe existir y ser válida en la configuración de implementación. En concreto, si la base de datos está en un equipo remoto y desea utilizar una cuenta de Windows, debe especificar una cuenta que tenga permisos de inicio de sesión en ese equipo.  
  
 Si el equipo está en un dominio diferente o que no son de confianza, considere el uso de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión de base de datos. Para obtener más información acerca de cómo elegir una cuenta, consulte [configurar una conexión de base de datos del servidor de informes &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 **Resumen**  
 Compruebe los valores antes de que se ejecute el asistente.  
  
 **Avanzar y finalizar**  
 Supervise el progreso de cada tarea.  
  
## <a name="see-also"></a>Vea también  
 [Base de datos &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [Asistente para la base de datos cambiar &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [Crear una base de datos del servidor de informes de modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Temas de Ayuda de F1 de administrador de configuración de Reporting Services &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Configurar una conexión de base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
