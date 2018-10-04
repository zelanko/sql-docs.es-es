---
title: Base de datos (modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.databasesetup.F1
ms.assetid: 8c9bb3b3-ea77-4a5b-ba35-7451ed11083d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d79b50e70f3eae3d9183ae220002136b39717e46
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102496"
---
# <a name="database-ssrs-native-mode"></a>Base de datos (Modo nativo de SSRS)
  Utilice la página Base de datos para crear y configurar las bases de datos del servidor de informes que permiten el almacenamiento interno de una o varias instancias del servidor de informes. Si está configurando un servidor de informes para utilizar una base de datos del servidor de informes remoto, debe usar el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager para crear la base de datos.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 La creación de una base de datos del servidor de informes y la configuración de la conexión es un proceso que consta de varios pasos. Para guiarle en los pasos, esta página proporciona asistentes para cada tipo de tarea. Los permisos e inicios de sesión se crean o actualizan automáticamente. Puede supervisar el estado de cada paso en la página Progreso. Si se produce un error, puede hacer clic en él para obtener información sobre cómo resolverlo.  
  
 Una base de datos del servidor de informes debe ser compatible con un modo de servidor específico. El modo predeterminado es el modo nativo, pero también puede crear una base de datos de servidor de informes para el modo integrado de SharePoint si está ejecutando un servidor de informes en una implementación de mayor tamaño de un producto o tecnología de SharePoint. Para más información, vea [Crear una base de datos del servidor de informes de modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
 Para abrir esta página, inicie el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager y haga clic en **base de datos** en el panel de navegación. Para obtener más información, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de SQL Server**  
 En la actual base de datos de servidor de informes, **nombre de SQL Server** especifica el nombre de la [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que ejecuta la base de datos del servidor de informes. Puede utilizar una instancia predeterminada o con nombre en un equipo local o remoto.  
  
 **Database Name**  
 Especifica el nombre de la base de datos del servidor de informes que almacena los datos del servidor.  
  
 **Modo de servidor de informes**  
 Indica si la base de datos del servidor de informes admite el modo nativo o el modo integrado de SharePoint. Para obtener más información, consulte [Reporting Services Report Server](../../../2014/reporting-services/reporting-services-report-server.md).  
  
 **Cambiar base de datos**  
 Inicie un asistente que le guíe por todos los pasos requeridos para crear o seleccionar una base de datos del servidor de informes.  
  
 **Tipo de credencial**  
 Especifica las credenciales que utiliza el servidor de informes para conectarse a la base de datos de servidor de informes. Tipos de credenciales que se puede especificar incluyen la cuenta de servicio, un usuario de dominio de Windows, el usuario local de Windows, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión de base de datos. Para obtener más información acerca de cómo seleccionar credenciales, vea [configurar una conexión de base de datos del servidor de informes &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 **Nombre de usuario**  
 Especifica una cuenta de usuario de dominio si está usando credenciales de Windows o un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión si usas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] credenciales. Si está usando credenciales de Windows, especifíquelas en este formato:  *\<dominio >\\< cuenta\>*.  
  
 **Contraseña**  
 Especifica la contraseña de la cuenta.  
  
 **Cambiar credenciales**  
 Inicie un asistente que le guíe a través de todos los pasos requeridos para seleccionar una cuenta diferente o actualizar la contraseña en la cuenta que se utiliza para conectarse a la base de datos del servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Crear una base de datos del servidor de informes de modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Temas de Ayuda de F1 de administrador de configuración de Reporting Services &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Base de datos del servidor de informes &#40;Modo nativo de SSRS&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [Configurar una conexión de base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
