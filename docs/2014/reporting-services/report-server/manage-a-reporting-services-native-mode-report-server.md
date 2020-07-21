---
title: Administrar un servidor de informes en modo nativo de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
ms.assetid: 6ca03a09-d6a8-4c93-ba12-1c99dcbfb618
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: da2eb97e5ce57a2e6a82dda3e264b33e1e3a3b11
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66103792"
---
# <a name="manage-a-reporting-services-native-mode-report-server"></a>Administrar un servidor de informes en modo nativo de Reporting Services
  Esta sección contiene procedimientos para configurar una instancia de servidor de informes en modo nativo utilizando el Administrador de configuración de Reporting Services.  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas de esta sección se organizan en categorías para que pueda encontrar las instrucciones que desea más fácilmente. La primera sección contiene los temas para las tareas de configuración básicas para un servidor de informes en modo nativo. La segunda sección contiene temas de configuración avanzados. La tercera sección contiene temas para configurar un servidor de informes de manera que se ejecute en modo integrado de SharePoint.  
  
### <a name="basic-configuration"></a>Configuración básica  
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
 Proporciona los pasos para iniciar la herramienta de configuración de Reporting Services.  
  
 [Configurar una cuenta de servicio &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)  
 Explica cómo especificar la información de cuenta y contraseña para el servicio Servidor de informes.  
  
 [Registrar un nombre principal de servicio &#40;SPN&#41; para un servidor de informes](register-a-service-principal-name-spn-for-a-report-server.md)  
 Explica cómo registrar manualmente un SPN para un servidor de informes que se ejecuta en una cuenta de usuario de dominio en una red que utiliza la autenticación Kerberos.  
  
 [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)  
 Explica cómo establecer una o varias direcciones URL que se usan para tener acceso al servicio web del servidor de informes y el Administrador de informes.  
  
 [Crear una base de datos del servidor de informes de modo nativo &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)  
 Proporciona los pasos para crear una base de datos de servidor de informes. Este paso es necesario para implementar una instalación de Reporting Services.  
  
### <a name="advanced-or-optional-configuration"></a>Configuración avanzada u opcional  
 [Configurar una implementación escalada horizontalmente del servidor de informes en modo nativo &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 Proporciona los pasos para configurar varios servidores de informes para compartir una base de datos del servidor de informes.  
  
 [Configurar un servidor de informes para la entrega por correo electrónico &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 Ofrece pasos para configurar un servidor de informes para la distribución por correo electrónico.  
  
 [Configurar un firewall para el acceso del Servidor de informes](configure-a-firewall-for-report-server-access.md)  
 Explica cómo abrir los puertos que se usan para las solicitudes entrantes y las respuestas salientes desde un servidor de informes.  
  
 [Configurar un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
 Describe los pasos adicionales necesarios para conectarse al Administrador de informes o a un servidor de informes mediante http://localhost.  
  
 [Configuración de un servidor de informes para la administración remota](configure-a-report-server-for-remote-administration.md)  
 Explica cómo configurar una instancia del servidor de informes remota para que pueda conectarse y configurarla desde un equipo diferente.  
  
 [Activación o desactivación de las características de Reporting Services](turn-reporting-services-features-on-or-off.md)  
 Explica cómo quitar las características que no se usan en una instalación de Reporting Services.  
  
 [Habilitar los errores remotos &#40;Reporting Services&#41;](enable-remote-errors-reporting-services.md)  
 Explica cómo establecer las propiedades de servidor en un servidor de informes para devolver información adicional sobre condiciones de error que se produzcan en servidores remotos.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar y administrar un servidor de informes &#40;modo nativo de SSRS&#41;](configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Configuración y administración de un servidor de informes &#40;modo de SharePoint de Reporting Services&#41;](../configure-administer-report-server-reporting-services-sharepoint-mode.md)  
  
  
