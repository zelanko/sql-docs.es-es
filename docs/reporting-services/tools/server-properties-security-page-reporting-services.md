---
title: Propiedades del servidor (página de seguridad) - Reporting Services | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
author: maggiesMSFT
ms.author: maggies
ms.date: 06/10/2016
ms.openlocfilehash: 0e29dcf7681d105f92b3bf187c38ebe764d2449e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571312"
---
# <a name="server-properties-security-page---reporting-services"></a>Propiedades del servidor (página de seguridad) - Reporting Services

  Use esta página de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] en [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] para desactivar características que pueden poner en peligro un servidor de informes. Al desactivar estas características, se limita alguna funcionalidad, pero puede mejorar la seguridad total del servidor de informes mitigando amenazas concretas.  
  
 Para abrir esta página:
 1) Inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2) Conéctese a una instancia del servidor de informes.
 3) Haga clic con el botón derecho en el nombre del servidor de informes y seleccione **Propiedades**.
 4) Haga clic en **Seguridad** para abrir esta página.  
  
## <a name="options"></a>Opciones

### <a name="enable-windows-integrated-security-for-report-data-sources"></a>Habilitar la seguridad integrada de Windows para orígenes de datos de informe

 Especifique si una conexión a un origen de datos de informe usa el token de seguridad de Windows del usuario que solicitó el informe.  
  
 Si desactiva esta característica, la característica de Seguridad integrada de Windows en las páginas de propiedades de origen de datos del informe no estará disponible. Si los orígenes de datos del informe se configuran para la seguridad integrada de Windows y posteriormente se desactiva esta característica, el servidor de informes actualiza de forma inmediata todas las propiedades de conexión de origen de datos para solicitar las credenciales.  
  
### <a name="enable-ad-hoc-reporting"></a>Habilitar la notificación ad hoc

 Especifica si los usuarios pueden realizar consultas ad hoc desde un informe del Generador de informes, en el que los nuevos informes se generan automáticamente cuando un usuario hace clic en los datos de interés.  
  
 Al establecer esta opción se determina si la propiedad **EnableLoadReportDefinition** en el servidor de informes está se establece en **True** o **False**. Si se desactiva esta opción, la propiedad se establece en **False** y el servidor de informes no genera los informes click-through que se crean durante la exploración de datos. Se bloquean todas las llamadas al método **LoadReportDefinition**.  
  
 Al desactivar esta opción, se mitiga una amenaza en la que un usuario malintencionado inicia un ataque por denegación de servicio sobrecargando el servidor de informes con solicitudes **LoadReportDefinition** .  
  
## <a name="see-also"></a>Consulte también

 [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md) [Conectar con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md) [Especificar información de credenciales y conexión para los orígenes de datos de informes](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) [Servidor de informes en Management Studio (Ayuda F1)](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)
