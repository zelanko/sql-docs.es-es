---
title: "Propiedades del servidor (página de seguridad) - Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8da36c90d2eb22600ad6560a37367e68de933971
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="server-properties-security-page---reporting-services"></a>Propiedades del servidor (página de seguridad) - Reporting Services
  Use esta página de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] en [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] para desactivar características que pueden poner en peligro un servidor de informes. Al desactivar estas características, se limitará alguna funcionalidad, pero puede mejorar la seguridad total del servidor de informes mitigando amenazas concretas.  
  
 Para abrir esta página:
 1) Inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2) Conéctese a una instancia del servidor de informes.
 3) Haga clic con el botón derecho en el nombre del servidor de informes y seleccione **Propiedades**. 
 4) Haga clic en **Seguridad** para abrir esta página.  
  
## <a name="options"></a>Opciones  
 **Habilitar la seguridad integrada de Windows para orígenes de datos de informe**  
 Especifique si puede realizarse una conexión a un origen de datos de informe con el token de seguridad de Windows del usuario que solicitó el informe.  
  
 Si desactiva esta característica, la característica de Seguridad integrada de Windows en las páginas de propiedades de origen de dato del informe no estará disponible. Si los orígenes de datos del informe se configuran para la seguridad integrada de Windows y desactiva posteriormente esta característica, el servidor de informes actualizará inmediatamente todas las propiedades de conexión a un origen de datos para solicitar las credenciales.  
  
 **Habilitar la notificación ad hoc**  
 Especifica si los usuarios pueden realizar consultas ad hoc desde un informe del Generador de informes, en el que los nuevos informes se generan automáticamente cuando un usuario hace clic en los datos de interés.  
  
 Al establecer esta opción se determina si la propiedad **EnableLoadReportDefinition** en el servidor de informes está se establece en **True** o **False**. Si borra esta opción, la propiedad se establecerá en **False** y el servidor de informes no generará informes click-through que se crean durante la exploración de datos. Se bloquearán todas las llamadas al método **LoadReportDefinition** .  
  
 Al desactivar esta opción, se mitiga una amenaza en la que un usuario malintencionado inicia un ataque por denegación de servicio sobrecargando el servidor de informes con solicitudes **LoadReportDefinition** .  
  
## <a name="see-also"></a>Vea también  
 [Establecer propiedades del servidor de informes &#40; Management Studio &#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Conectarse a un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Especificar credenciales y la información de conexión para orígenes de datos de informe](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Servidor de informes en Management Studio ayuda F1](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  

