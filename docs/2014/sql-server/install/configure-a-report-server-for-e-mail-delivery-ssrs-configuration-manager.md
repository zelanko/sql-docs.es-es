---
title: Configurar un servidor de informes para la entrega de correo electrónico (Administrador de configuración de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], distributing
- report servers [Reporting Services], e-mail delivery
- remote SMTP service [Reporting Services]
- distributing reports [Reporting Services], e-mail
- CDO
- Collaboration Data Objects
- SMTP settings [Reporting Services]
- e-mail [Reporting Services]
- sending reports
- mail [Reporting Services]
- local SMTP service [Reporting Services]
ms.assetid: b838f970-d11a-4239-b164-8d11f4581d83
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e189890845bad34153ebef4231465c260b538848
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179202"
---
# <a name="configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager"></a>Configurar un servidor de informes para la entrega de correo electrónico (Administrador de configuración de SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye una extensión de entrega por correo electrónico para distribuir informes mediante el correo electrónico. Según cómo defina la suscripción del correo electrónico, una entrega podría estar compuesta de una notificación, un vínculo, datos adjuntos o un informe incrustado. La extensión de entrega por correo electrónico funciona con la tecnología de servidor de correo existente. El servidor de correo debe ser un servidor SMTP o un reenviador. El servidor de informes se conecta a un servidor SMTP a través de bibliotecas de Collaboration Data Objects (CDO), cdosys.dll, que el sistema operativo proporciona.  
  
 La extensión de entrega por correo electrónico del servidor de informes no está configurada de manera predeterminada. Debe utilizar el Administrador de configuración de Reporting Services para configurar dicha extensión mínimamente. Para establecer propiedades avanzadas, debe editar el archivo `RSReportServer.config` . Si no puede configurar el servidor de informes para que utilice esta extensión, puede entregar los informes en una carpeta compartida. Para obtener más información, vea [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md).  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo|  
  
 
  
##  <a name="bkmk_configuration_requirements"></a> Requisitos de configuración  
  
-   La entrega por correo electrónico del servidor de informes se implementa en Collaboration Data Objects (CDO) y requiere un servidor del Protocolo simple de transferencia de correo (SMTP) local o remoto, o bien un reenviador SMTP. SMTP no se admite en todos los sistemas operativos Windows. Si usa la edición basada en Itanium de Windows Server 2008, no se admite SMTP. Para obtener más información sobre las opciones de configuración que se proporcionan a través de CDO, vea [el tema sobre la coclase Configuration](http://go.microsoft.com/fwlink/?LinkId=98237) en MSDN.  
  
-   La cuenta del servicio Servidor de informes debe tener permiso para enviar correo electrónico en el servidor SMTP.  
  
-   La extensión de entrega por correo electrónico utiliza la codificación UTF-8 en los datos adjuntos del correo electrónico. La codificación no se puede modificar; la extensión de representación en HTML solo admite UTF-8.  
  
> [!NOTE]  
>  La extensión de entrega por correo electrónico predeterminada no es compatible con la firma digital ni el cifrado de mensajes de correo salientes.  
  
 
  
##  <a name="bkmk_configure_for_local_or_remote_SMTP"></a> Configurar un servidor de informes para un servicio SMTP Local o remoto  
 Puede utilizar un servicio SMTP local o un servidor o reenviador SMTP remoto para admitir la entrega por correo electrónico. Si tiene acceso a un servidor SMTP remoto existente, debería plantearse utilizarlo. Si no hay ningún servidor SMTP disponible o si después encuentra errores de entrega de informes que pueden atribuirse a errores en la conexión del equipo, debería pasar a utilizar un servicio SMTP local. Más adelante en este tema se proporcionan detalles sobre cómo configurar un servidor de informes para un servicio local o remoto.  
  
  
  
##  <a name="bkmk_setting_email_delivery"></a> Las opciones de configuración para la entrega de correo electrónico  
 Para poder utilizar la entrega por correo electrónico del servidor de informes, debe establecer valores de configuración que proporcionen información sobre qué servidor SMTP se debe utilizar.  
  
 Para configurar un servidor de informes para la entrega por correo electrónico, siga este procedimiento:  
  
-   Use el Administrador de configuración de Reporting Services si solo va a especificar un servidor SMTP y una cuenta de usuario que tenga permiso para enviar correo electrónico. Ésta es la configuración mínima necesaria para configurar la extensión de entrega por correo electrónico del servidor de informes. Para obtener más información, consulte [configuración de correo electrónico - Administrador de configuración &#40;modo nativo de SSRS&#41; ](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md) y [entrega por correo electrónico en Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md).  
  
-   (Opcionalmente) Utilice un procesador de texto para especificar valores adicionales en el archivo RSreportserver.config. Este archivo contiene toda la configuración para la distribución del correo electrónico del servidor de informes. Si utiliza un servidor SMTP adicional o limita la entrega de correo electrónico a hosts específicos, debe configurar opciones adicionales en estos archivos. Para obtener más información sobre cómo buscar y modificar archivos de configuración, consulte [modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41; ](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) en libros en pantalla de SQL Server.  
  
> [!NOTE]  
>  Las opciones de correo electrónico del servidor de informes se basan en CDO. Si desea obtener más detalles acerca de opciones específicas, puede consultar la documentación de producción de CDO.  
  

  
##  <a name="bkmk_example_config_file"></a> Configuración de correo electrónico del servidor de informes de ejemplo  
 El ejemplo siguiente muestra las opciones de configuración del archivo RSreportserver.config para un servidor SMTP remoto. Para obtener información acerca de las descripciones de la configuración y los valores válidos, vea [RSReportServer Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla o la documentación del producto CDO.  
  
```  
<RSEmailDPConfiguration>  
     <SMTPServer>mySMTPServer.Adventure-Works.com</SMTPServer>  
     <SMTPServerPort></SMTPServerPort>  
     <SMTPAccountName></SMTPAccountName>  
     <SMTPConnectionTimeout></SMTPConnectionTimeout>  
     <SMTPServerPickupDirectory></SMTPServerPickupDirectory>  
     <SMTPUseSSL></SMTPUseSSL>  
     <SendUsing>2</SendUsing>  
     <SMTPAuthenticate></SMTPAuthenticate>  
     <From>my-rs-email-account@Adventure-Works.com</From>  
     <EmbeddedRenderFormats>  
          <RenderingExtension>MHTML</RenderingExtension>  
     </EmbeddedRenderFormats>  
     <PrivilegedUserRenderFormats></PrivilegedUserRenderFormats>  
     <ExcludedRenderFormats>  
          <RenderingExtension>HTMLOWC</RenderingExtension>  
          <RenderingExtension>NULL</RenderingExtension>  
     </ExcludedRenderFormats>  
     <SendEmailToUserAlias>True</SendEmailToUserAlias>  
     <DefaultHostName></DefaultHostName>  
     <PermittedHosts>  
          <HostName>Adventure-Works.com</HostName>  
          <HostName>hotmail.com</HostName>  
     </PermittedHosts>  
</RSEmailDPConfiguration>  
```  
  

  
##  <a name="bkmk_setting_TO_field"></a> Opciones de configuración para la configuración de la a: campo de un mensaje  
 Las suscripciones definidas por el usuario creadas según los permisos otorgados por la tarea **Administrar suscripciones individuales** contienen un nombre de usuario establecido previamente basado en la cuenta de usuario de dominio. Cuando el usuario crea la suscripción, el nombre del destinatario del campo **Para:** se rellena automáticamente mediante la cuenta de usuario de dominio de la persona que está creando la suscripción.  
  
 Si está utilizando un servidor SMTP o reenviador que emplee cuentas de correo electrónico distintas a la cuenta de usuario de dominio, la entrega del informe generará un error cuando el servidor SMTP intente entregar el informe al usuario.  
  
 Para solucionar este problema, puede modificar la configuración para permitir a los usuarios escribir un nombre en el campo **Para:** :  
  
1.  Abra RSReportServer.config en un editor de texto.  
  
2.  Establecer `SendEmailToUserAlias` a `False`.  
  
3.  Establecer `DefaultHostName` en el nombre de sistema de nombres de dominio (DNS) o la dirección IP del servidor SMTP o reenviador.  
  
4.  Guarde el archivo.  
  
  
  
##  <a name="bkmk_options_remote_SMTP"></a> Opciones de configuración para el servicio SMTP remoto  
 La conexión entre el servidor de informes y un servidor o reenviador SMTP viene determinada por las opciones de configuración siguientes:  
  
-   `SendUsing` Especifica un método para enviar mensajes. Se puede elegir entre un servicio SMTP de red o un directorio de recogida del servicio SMTP local. Para utilizar un servicio SMTP remoto, este valor debe establecerse en **2** en el archivo RSReportServer.config.  
  
-   `SMTPServer` Especifica el servidor SMTP o reenviador. Se trata de un valor necesario si utiliza un servidor o reenviador SMTP remoto.  
  
-   `From` establece el valor que aparece en el **desde:** línea de un mensaje de correo electrónico. Se trata de un valor necesario si utiliza un servidor o reenviador SMTP remoto.  
  
 Entre los demás valores que se utilizan para un servicio SMTP remoto se incluyen los siguientes (tenga en cuenta que no es necesario especificarlos a menos que desee reemplazar los valores predeterminados).  
  
-   **SMTPServerPort** se configura para el puerto 25.  
  
-   **SMTPAuthenticate** especifica cómo se conecta el servidor de informes al servidor SMTP remoto. El valor predeterminado es 0 (o sin autenticación). En tal caso, la conexión se realiza a través de un acceso anónimo. En función de su configuración de dominio, es posible que el servidor de informes y el servidor SMTP tengan que ser miembros del mismo dominio.  
  
     Para enviar correo electrónico a listas de distribución restringidas (por ejemplo, listas de distribución que acepten mensajes entrantes solo de cuentas autenticadas), establezca **SMTPAuthenticate** en **2**.  
  

  
##  <a name="bkmk_options_local_SMTP"></a> Opciones de configuración para el servicio SMTP Local  
 Configurar un servicio SMTP local resulta útil si se está probando o solucionando problemas de la entrega por correo electrónico del servidor de informes. El servicio SMTP local no está habilitado de forma predeterminada. Para obtener instrucciones sobre cómo habilitarlo, consulte [configurar un servidor de informes para la entrega de correo electrónico (Administrador de configuración de SSRS)](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) y [configuración de correo electrónico - Administrador de configuración &#40;modo nativo de SSRS&#41; ](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md) .  
  
 La conexión entre el servidor de informes y un servidor o reenviador SMTP local viene determinada por las opciones de configuración siguientes:  
  
-   `SendUsing` se establece en **1**.  
  
-   **SMTPServerPickupDirectory** se establece en una carpeta de la unidad local.  
  
    > [!NOTE]  
    >  Asegúrese de que no establezca `SMTPServer` si usa un servidor SMTP local.  
  
-   `From` establece el valor que aparece en el **desde:** línea de un mensaje de correo electrónico. Este valor es necesario.  
  
 
  
##  <a name="bkmk_use_configuration_manager"></a> Para configurar el correo electrónico del servidor de informes mediante el Administrador de configuración de Reporting Services  
  
1.  Compruebe que el servicio Servidor de informes de Windows disponga de permisos `Send As` para el servidor SMTP.  
  
2.  Inicie el Administrador de configuración de Reporting Services y conéctese a la instancia del servidor de informes  
  
3.  En la página Configuración de correo electrónico, escriba el nombre del servidor SMTP. Este valor puede ser una dirección IP, un nombre UNC de un equipo de la intranet corporativa o un nombre de dominio completo.  
  
4.  En **Dirección del remitente**, escriba el nombre de una cuenta que tenga permiso para enviar correo electrónico desde el servidor SMTP.  
  
5.  Haga clic en **Aplicar**.  
  

  
##  <a name="bkmk_confiugre_remote_SMTP"></a> Para configurar un servicio SMTP remoto para el servidor de informes  
  
1.  Compruebe que el servicio Servidor de informes de Windows disponga de permisos `Send As` para el servidor SMTP.  
  
2.  Abra el archivo RSReportServer.config en un editor de texto.  
  
3.  Compruebe que <`UrlRoot`> se establece en la dirección URL del servidor. Este valor se establece al configurar el servidor de informes y debe mostrar la dirección. Si no es así, escriba la dirección URL del servidor de informes.  
  
4.  En la sección Entrega, busque <`ReportServerEmail`>.  
  
5.  En <`SMTPServer`>, escriba el nombre del servidor SMTP. Este valor puede ser una dirección IP, un nombre UNC de un equipo de la intranet corporativa o un nombre de dominio completo.  
  
6.  Compruebe que <`SendUsing`> está establecido en 2. Si se especifica otro valor, el servidor de informes no se habrá configurado para utilizar un servicio SMTP remoto.  
  
7.  En <`From`>, escriba el nombre de una cuenta que tenga permiso para enviar correo electrónico desde el servidor SMTP.  
  
8.  Guarde el archivo.  
  
     El servidor de informes utilizará la nueva configuración de forma automática, por lo que no necesita reiniciar el servicio. Puede especificar valores adicionales para SMTP con el fin de configurar cómo se utilizará el servidor para la entrega por correo electrónico del servidor de informes. Para obtener más información, consulte [configurar un servidor de informes para la entrega de correo electrónico](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) y [RSReportServer Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  

  
##  <a name="bkmk_confiugre_local_SMTP"></a> Para configurar un servicio SMTP local para el servidor de informes  
  
1.  En el Panel de control, haga clic en **Agregar o quitar programas**.  
  
2.  Haga clic en **Agregar o quitar componentes de Windows** para iniciar el Asistente para componentes de Windows.  
  
3.  Seleccione **Servidor de aplicaciones** y haga clic en **Detalles**.  
  
4.  Seleccione **Internet Information Services (IIS)** y haga clic en **Detalles**.  
  
5.  Active la casilla **Servicio SMTP** y haga clic en **Aceptar**.  
  
6.  En el Asistente para componentes de Windows, haga clic en **Siguiente**. Haga clic en **Finalizar**.  
  
7.  Compruebe que el servicio esté ejecutándose en la consola **Servicios** .  
  
8.  Abra el archivo **RsReportServer.config** en un editor de texto.  
  
9. Compruebe que `<UrlRoot>` se haya establecido en la dirección URL del servidor de informes. Este valor se establece al configurar el servidor de informes y debe mostrar la dirección. Si no es así, escriba la dirección URL del servidor de informes.  
  
10. En la sección Entrega, busque `<ReportServerEmail>.`.  
  
11. En `<SMTPServer>`, borre todos los valores de esta configuración, pero no elimine las etiquetas.  
  
12. Establezca `<SendUsing>` en 1. Si se especifica otro valor, el servidor de informes no se habrá configurado para utilizar un servicio SMTP local.  
  
13. Establezca `<SMTPServerPickupDirectory>` en una carpeta de la unidad local.  
  
14. Establezca `<From>` en una cuenta con permiso para enviar correo electrónico desde el servidor SMTP.  
  
15. Guarde el archivo.  
  
 
  
## <a name="see-also"></a>Vea también  
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
