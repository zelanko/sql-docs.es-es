---
title: Asistente para cambiar credenciales (modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
ms.openlocfilehash: 9dba9988bec98f597a59fe4152b2abdde0d5ccea
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096705"
---
# <a name="change-credentials-wizard-ssrs-native-mode"></a>Asistente para cambiar credenciales (Modo nativo de SSRS)
  El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona el Asistente para cambiar credenciales. Este asistente actúa como guía por los pasos necesarios para reconfigurar la cuenta que el servidor de informes usa para conectar con la base de datos del servidor de informes. Al cambiar las credenciales, el Administrador de configuración actualizará todos los permisos y la información de inicio de sesión de base de datos en el servidor de bases de datos correspondiente a la base de datos que usa activamente el servidor de informes.  
  
 Para iniciar el asistente, haga clic en **Cambiar credenciales** en la página Base de datos del Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener instrucciones sobre cómo iniciar el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, vea [Reporting Services Configuration Manager &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="options"></a>Opciones  
 **Servidor de base de datos**  
 Especifica el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que ejecuta la base de datos del servidor de informes.  
  
 Para conectarse a la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , debe usar credenciales que tengan permiso para iniciar sesión en el servidor y para actualizar la información de las bases de datos. El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa sus credenciales actuales de Windows, pero si no tiene permisos de inicio de sesión o de base de datos, puede especificar un inicio de sesión de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 No puede especificar credenciales de Windows diferentes. Si desea conectarse como otro usuario de Windows, inicie sesión como ese usuario y, a continuación, inicie el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 **Credenciales**  
 Especifica la cuenta con la que el servidor de informes se conecta a la base de datos del servidor de informes. Los valores válidos incluyen la cuenta de servicio web del servidor de informes, un inicio de sesión de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definido en la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que usa para hospedar el servidor de informes o una cuenta de Windows. Si usa una cuenta de Windows, puede especificar una cuenta local (*\<nombreDeEquipo >\\< nombre de usuario\>*) si el servidor de informes y la base de datos están en el mismo equipo o un usuario de dominio cuenta (*\<dominio >\\< nombre de usuario\>*) si están en equipos diferentes en el mismo dominio.  
  
 El servidor de informes creará un inicio de sesión de base de datos y asignará permisos de base de datos a la cuenta que especifique.  
  
 El servidor de informes no crea la propia cuenta. La cuenta que especifique ya debe existir y ser válida en la configuración de implementación. En concreto, si la base de datos está en un equipo remoto y desea utilizar una cuenta de Windows, debe especificar una cuenta que tenga permisos de inicio de sesión en ese equipo.  
  
 Si el equipo está en un dominio diferente o que no sea de confianza, considere usar un inicio de sesión de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información acerca de cómo elegir una cuenta, consulte [configurar una conexión de base de datos del servidor de informes &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 **Resumen**  
 Compruebe los valores antes de que se ejecute el asistente.  
  
 **Avanzar y finalizar**  
 Supervise el progreso de cada tarea.  
  
## <a name="see-also"></a>Vea también  
 [Base de datos &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [Asistente para la base de datos cambiar &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [Crear una base de datos del servidor de informes de modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Temas de Ayuda de F1 de administrador de configuración de Reporting Services &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
