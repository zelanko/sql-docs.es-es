---
title: Entrega por correo electrónico en Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: subscriptions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
caps.latest.revision: 45
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 44fd22755bc91784966e1b5b27107aad1d3f2ae4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33032892"
---
# <a name="e-mail-delivery-in-reporting-services"></a>Entrega por correo electrónico en Reporting Services
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye una extensión de entrega de correo electrónico que permite enviar por correo electrónico un informe a grupos o usuarios individuales. Para distribuir un informe por correo electrónico, debe 1) configurar el servidor de informes para la entrega de correo electrónico y 2) definir una suscripción estándar o una suscripción controlada por datos. Una suscripción única no puede entregar varios informes en un solo mensaje de correo electrónico. Sin embargo, se pueden crear varias suscripciones.  
  
 El servidor de informes se conecta con el servidor de correo electrónico a través de una conexión estándar. No utiliza ninguna comunicación que se haya cifrado mediante SSL (Capa de sockets seguros). El servidor de correo electrónico debe ser un servidor SMTP (Protocolo simple de transferencia de correo) remoto o local en la misma red que el servidor de informes.  
  
 Para obtener los pasos detallados que le pueden guiar para crear una suscripción, consulte lo siguiente:  
  
-   [Crear y administrar suscripciones para servidores de informes en modo nativo](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
-   [Creación y administración de suscripciones para servidores de informes en modo de SharePoint](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
  
## <a name="e-mail-delivery-options"></a>Opciones de entrega por correo electrónico  
 La entrega de correo electrónico del servidor de informes puede entregar informes de las siguientes maneras  
  
-   Enviar una notificación y un hipervínculo al informe generado.  
  
-   Enviar una notificación en la línea Asunto: de un mensaje de correo electrónico. De forma predeterminada, la línea Asunto: de la definición de suscripción incluye las variables siguientes que se reemplazan con información específica del informe cuando se procesa la suscripción:  
  
     **@ReportName** especifica el nombre del informe.  
  
     **@ExecutionTime** especifica cuándo se ejecutó el informe.  
  
     Puede combinar estas variables con texto estático o modificar el texto de la línea Asunto: para cada suscripción.  
  
-   Enviar un informe adjunto o incrustado. El formato de representación y el explorador determinan si el informe se incrusta o se adjunta.  
  
     Si el explorador es compatible con HTML 4.0 y MHTML, y se elige el formato de representación Archivo web, el informe se incrusta como parte del mensaje. Los demás formatos de representación (CSV, PDF, etc.) entregan los informes como datos adjuntos. En el caso de los servidores de informes en modo nativo, puede deshabilitar esta funcionalidad en el archivo de configuración RSReportServer.config.  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no comprueba el tamaño de los datos adjuntos ni del mensaje antes de enviar el informe. Si los datos adjuntos o el mensaje superan el límite máximo permitido por el servidor de correo, el informe no se entrega. Elija una de las otras opciones de entrega (como dirección URL o notificación) si el informe es de gran tamaño.  
  
 Establezca las opciones de entrega que determinarán cómo se entrega un informe al crear la suscripción. Por ejemplo, si selecciona **Incluir vínculo** en la suscripción, en el mensaje de correo se incluirá un hipervínculo al informe.  
  
## <a name="native-mode-role-based-e-mail-settings"></a>Configuración de correo electrónico basado en roles en modo nativo  
 En un entorno de servidor de informes en modo nativo, la configuración de entrega de correo electrónico con la que trabaje variará en función de que su rol incluya la tarea "Administrar suscripciones individuales" o la tarea "Administrar todas las suscripciones".  
  
|Tarea|Configuración disponible|  
|----------|------------------------|  
|Administrar suscripciones individuales|Muestra campos que permiten a un usuario automatizar y entregar un informe a sí mismo. En este modo, los campos que aceptan alias de correo electrónico no están disponibles.|  
|Administrar todas las suscripciones|Muestra los campos que admiten una mayor distribución, incluidos los campos Para:, CC:, CCO: y Responder a:, y proporciona más formas de enrutar un informe a más suscriptores. La disponibilidad de los campos de alias de correo electrónico se define mediante la configuración del archivo de configuración RSReportServer.|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>Especificar direcciones de correo electrónico en una suscripción  
 Si distribuye informes dentro de la intranet, y usa una puerta de enlace SMTP a un servidor [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange, escriba el alias de correo electrónico (como si estuviera enviando correo electrónico a un colega del trabajo). Si la entrega se dirige a una cuenta de correo electrónico externa, escriba la dirección de correo electrónico completa. Si especifica más direcciones de correo electrónico para agregar a otras personas a la suscripción, los suscriptores reciben una copia exacta del informe que se produce a partir de esta suscripción.  
  
 El servidor de informes no valida las direcciones de correo electrónico ni las obtiene de un servidor de correo electrónico. Debe conocer de antemano las direcciones de correo electrónico que desea utilizar. De forma predeterminada, puede enviar por correo electrónico informes a cualquier cuenta de correo electrónico válida, ya sea que esté dentro o fuera de su organización. Sin embargo, se pueden utilizar parámetros de configuración para restringir la entrega por correo electrónico a los hosts de servidor de correo que identifique por nombre. Puede especificar hosts adicionales si desea permitir la entrega por correo electrónico a personas que no formen parte de su organización.  
  
 El mensaje de correo electrónico utilizado para entregar el informe debe enviarse desde una cuenta de correo electrónico definida en el servidor de correo electrónico. Un valor de configuración especifica la cuenta de correo electrónico. La cuenta se utiliza para todos los informes entregados con la extensión de entrega por correo electrónico; no puede especificar varias cuentas ni modificar la cuenta para informes individuales.  
  
## <a name="controlling-e-mail-delivery"></a>Controlar la entrega por correo electrónico  
 Puede configurar un servidor de informes para limitar la distribución por correo electrónico a dominios de host específicos. Por ejemplo, puede evitar que un servidor de informes nativo entregue un informe a todos los dominios, excepto a los que figuran en el archivo de configuración **RSReportServer.config** .  
  
 También puede establecer los parámetros de configuración para ocultar el campo **Para** en una suscripción. En este caso, los informes solo se entregan al usuario que haya definido la suscripción. No obstante, una vez que se envíe un informe a un usuario, no puede impedir explícitamente que se reenvíe.  
  
 El método más eficaz de controlar la distribución de informes consiste en configurar el servidor de informes para que solo envíe una dirección URL de servidor de informes. El servidor de informes utiliza Autenticación de Windows y un modelo de autorización basada en roles para controlar el acceso a un informe. Si un usuario recibe accidentalmente mediante el correo electrónico un informe que no está autorizado para ver, el servidor de informes no lo mostrará. Para obtener más información acerca de las suscripciones, consulte lo siguiente.  
  
## <a name="e-mail-server-configuration"></a>Configuración del servidor de correo electrónico  
 Para un servidor de informes en modo nativo, la extensión de entrega de correo electrónico se configura con el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo y editando los archivos de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . En el caso de un servidor de informes en modo SharePoint, la extensión de entrega de correo electrónico en páginas de administración de SharePoint y scripts de PowerShell.  
  
 
 Para obtener información sobre cómo configurar un servidor de informes en modo nativo, vea [Configuración de correo electrónico: modo nativo de Reporting Services (Administrador de configuración)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)
 
 
 Para obtener información sobre cómo configurar un servidor de informes en modo de SharePoint, vea lo siguiente:  
  
  
## <a name="see-also"></a>Ver también  
 [Tareas y permisos](../../reporting-services/security/tasks-and-permissions.md)   
 [Suscripciones y entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Suscripciones controladas por datos](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Asignaciones de roles](../../reporting-services/security/role-assignments.md)  
  
  
