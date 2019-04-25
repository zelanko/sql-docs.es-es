---
title: Entrega por correo electrónico en Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 45e72fe3c163f05f283965beb5fb3cf6ce62c50e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62510949"
---
# <a name="e-mail-delivery-in-reporting-services"></a>Entrega por correo electrónico en Reporting Services
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye una extensión de entrega de correo electrónico que permite enviar por correo electrónico un informe a grupos o usuarios individuales. La extensión de entrega de correo electrónico se configura con el Administrador de configuración de Reporting Services y mediante la edición de los archivos de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para distribuir o recibir un informe por correo electrónico, defina una suscripción estándar o controlada por datos. Puede suscribirse o distribuir solo un informe a la vez. No puede crear una suscripción que entregue varios informes en un solo mensaje de correo electrónico. Para obtener más información acerca de las suscripciones, vea [crear, modificar y eliminar suscripciones estándar &#40;Reporting Services en modo nativo&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] El modo de SharePoint &#124; SharePoint 2010 y SharePoint 2013<br /><br /> **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] |  
  
## <a name="e-mail-delivery-options"></a>Opciones de entrega por correo electrónico  
 La entrega por correo electrónico del servidor de informes puede entregar informes de las siguientes maneras:  
  
-   Enviar una notificación y un hipervínculo al informe generado.  
  
-   Enviar una notificación en la línea Asunto: de un mensaje de correo electrónico. De forma predeterminada, la línea Asunto: de la definición de suscripción incluye las variables siguientes que se reemplazan con información específica del informe cuando se procesa la suscripción:  
  
     **@ReportName** especifica el nombre del informe.  
  
     **@ExecutionTime** especifica cuándo se ejecutó el informe.  
  
     Puede combinar estas variables con texto estático o modificar el texto de la línea Asunto: para cada suscripción.  
  
-   Enviar un informe adjunto o incrustado. El formato de representación y el explorador determinan si el informe se incrusta o se adjunta.  
  
     Si el explorador es compatible con HTML 4.0 y MHTML, y se elige el formato de representación Archivo web, el informe se incrusta como parte del mensaje. Los demás formatos de representación (CSV, PDF, etc.) entregan los informes como datos adjuntos. Puede deshabilitar esta funcionalidad en el archivo de configuración RSReportServer.  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no comprueba el tamaño de los datos adjuntos ni del mensaje antes de enviar el informe. Si los datos adjuntos o el mensaje superan el límite máximo permitido por el servidor de correo, el informe no se entrega. Elija una de las otras opciones de entrega (como dirección URL o notificación) si el informe es de gran tamaño.  
  
 Establezca las opciones de entrega que determinarán cómo se entrega un informe al crear la suscripción. Por ejemplo, si selecciona **Incluir vínculo** en la suscripción, el mensaje de correo electrónico incluye un hipervínculo al informe.  
  
## <a name="role-based-e-mail-settings"></a>Configuración de correo electrónico basado en roles  
 Cuando se suscriba a un informe, la configuración de entrega por correo electrónico con la que trabaje variará en función de que su rol incluya la tarea "Administrar suscripciones individuales" o la tarea "Administrar todas las suscripciones".  
  
|Tarea|Configuración disponible|  
|----------|------------------------|  
|Administrar suscripciones individuales|Muestra campos que permiten a un usuario automatizar y entregar un informe a sí mismo. En este modo, los campos que aceptan alias de correo electrónico no están disponibles.|  
|Administrar todas las suscripciones|Muestra los campos que admiten una mayor distribución, incluidos los campos Para:, CC:, CCO: y Responder a:, y proporciona más formas de enrutar un informe a más suscriptores. La disponibilidad de los campos de alias de correo electrónico se define mediante la configuración del archivo de configuración RSReportServer.|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>Especificar direcciones de correo electrónico en una suscripción  
 Si distribuye informes dentro de la intranet, y usa una puerta de enlace SMTP a un servidor [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange, escriba el alias de correo electrónico (como si estuviera enviando correo electrónico a un colega del trabajo). Si la entrega se dirige a una cuenta de correo electrónico externa, escriba la dirección de correo electrónico completa. Si especifica más direcciones de correo electrónico para agregar a otras personas a la suscripción, los suscriptores reciben una copia exacta del informe que se produce a partir de esta suscripción.  
  
 El servidor de informes no valida las direcciones de correo electrónico ni las obtiene de un servidor de correo electrónico. Debe conocer de antemano las direcciones de correo electrónico que desea utilizar. De forma predeterminada, puede enviar por correo electrónico informes a cualquier cuenta de correo electrónico válida, ya sea que esté dentro o fuera de su organización. Sin embargo, se pueden utilizar parámetros de configuración para restringir la entrega por correo electrónico a los hosts de servidor de correo que identifique por nombre. Puede especificar hosts adicionales si desea permitir la entrega por correo electrónico a personas que no formen parte de su organización.  
  
 El mensaje de correo electrónico utilizado para entregar el informe debe enviarse desde una cuenta de correo electrónico definida en el servidor de correo electrónico. Un valor de configuración especifica la cuenta de correo electrónico. La cuenta se utiliza para todos los informes entregados con la extensión de entrega por correo electrónico; no puede especificar varias cuentas ni modificar la cuenta para informes individuales.  
  
## <a name="e-mail-server-configuration"></a>Configuración del servidor de correo electrónico  
 El servidor de informes se conecta con el servidor de correo electrónico a través de una conexión estándar. No utiliza ninguna comunicación que se haya cifrado mediante SSL (Capa de sockets seguros). El servidor de correo electrónico debe ser un servidor SMTP (Protocolo simple de transferencia de correo) remoto o local en la misma red que el servidor de informes.  
  
 Para obtener información sobre cómo configurar un servidor de informes en modo nativo, vea lo siguiente:  
  
-   [Configurar un servidor de informes para la entrega de correo electrónico &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
  
-   [Configuración - Administrador de configuración de correo electrónico &#40;modo nativo de SSRS&#41;](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)  
  
 Para obtener información sobre cómo configurar un servidor de informes en modo de SharePoint, vea lo siguiente:  
  
-   [Configurar el correo electrónico para una aplicación de servicio de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](../install-windows/configure-e-mail-for-a-reporting-services-service-application.md)  
  
## <a name="see-also"></a>Vea también  
 [Tareas y permisos](../security/tasks-and-permissions.md)   
 [Suscripciones y entrega &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [Suscripciones controladas por datos](data-driven-subscriptions.md)   
 [Asignaciones de roles](../security/role-assignments.md)  
  
  
