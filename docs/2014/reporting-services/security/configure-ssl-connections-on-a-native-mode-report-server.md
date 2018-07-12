---
title: Configurar conexiones SSL en un servidor de informes en modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Secure Sockets Layer (SSL)
ms.assetid: 212f2042-456a-4c0a-8d76-480b18f02431
caps.latest.revision: 34
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bd49900daf397575c90be86d0370f47824cc4d8e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150526"
---
# <a name="configure-ssl-connections-on-a-native-mode-report-server"></a>Configurar conexiones SSL en un servidor de informes en modo nativo
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] El modo nativo usa el servicio HTTP SSL (Capa de sockets seguros) para establecer conexiones cifradas con un servidor de informes. Si tiene el archivo de certificado (.cer) instalado en un almacén de certificados local en el equipo del servidor de informes, puede enlazar el certificado a una reserva de direcciones URL de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para admitir las conexiones con el servidor de informes en un canal cifrado.  
  
> [!TIP]  
>  Si usa el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vea la documentación de SharePoint para obtener más información. Por ejemplo, la entrada del blog [How to enable SSL on a SharePoint 2010 web application (http://blogs.msdn.com/b/sowmyancs/archive/2010/02/12/how-to-enable-ssl-on-a-sharepoint-web-application.aspx)](http://blogs.msdn.com/b/sowmyancs/archive/2010/02/12/how-to-enable-ssl-on-a-sharepoint-web-application.aspx) (Cómo habilitar SSL en una aplicación web de SharePoint 2010).  
  
 Como Internet Information Services (IIS) también usa HTTP SSL, hay importantes problemas de interoperabilidad que es necesario tener en cuenta si IIS y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se ejecutan en el mismo equipo. Asegúrese de revisar la sección Problemas de interoperabilidad con IIS para obtener información sobre cómo resolver estos problemas.  
  
## <a name="server-certificate-requirements"></a>Requisitos de certificado de servidor  
 Debe tener un certificado de servidor instalado en el equipo (no se admiten los certificados de cliente). Reporting Services no proporciona funciones para solicitar, generar, descargar o instalar un certificado. [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] proporciona un complemento Certificados que se puede usar para pedir un certificado de una entidad de certificación de confianza.  
  
 En esta prueba, puede generar un certificado localmente. Si usa la utilidad **MakeCert** y el comando de ejemplo como una plantilla, asegúrese de especificar el nombre del servidor como host y quite todos los saltos de línea antes de ejecutar el comando. Si ejecuta el comando en una ventana DOS, puede que tenga que aumentar el tamaño de búfer de la ventana para que pueda contener todo el comando.  
  
 Si ejecuta IIS y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] conjuntamente en el mismo equipo, puede usar la aplicación de consola [!INCLUDE[iismgr](../../includes/iismgr-md.md)] para hacer que se instale el certificado en el equipo. [!INCLUDE[iismgr](../../includes/iismgr-md.md)] incluye opciones para crear y empaquetar un archivo de solicitud de certificado (.crt) para su posterior procesamiento por una entidad de certificación de confianza. La entidad de certificación que use generará un archivo de certificado (.cer) y se lo enviará de vuelta. Puede utilizar la Consola de administración de IIS para instalar el archivo de certificado en el almacén local. Para obtener más información, vea [Using SSL to Encrypt Confidential Data](http://go.microsoft.com/fwlink/?LinkId=71123) en Technet.  
  
## <a name="interoperability-issues-with-iis"></a>Problemas de interoperabilidad con IIS  
 La presencia de IIS en el mismo equipo que [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] afectará significativamente a las conexiones SSL con un servidor de informes:  
  
-   Si IIS está instalado, el servicio World Wide Web (W3SVC) siempre debe estar ejecutándose. El servicio HTTP SSL establecerá una dependencia con IIS si detecta que IIS se está ejecutando. Esto significa que el servicio World Wide Web (W3SVC) tiene que ejecutarse siempre que IIS y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] estén instalados en el mismo equipo y se configuren direcciones URL de servidor de informes para las conexiones SSL.  
  
-   Si desinstala IIS, puede interrumpir temporalmente el servicio para una dirección URL de servidor de informes enlazada a SSL. Por esta razón, se recomienda encarecidamente reiniciar el equipo después de desinstalar IIS.  
  
     Es necesario reiniciar el equipo para borrar todas las sesiones SSL de la memoria caché. Algunos sistemas operativos almacenan en memoria caché las sesiones SSL hasta diez horas, con lo que una dirección URL https:// continúa funcionando incluso después de quitar el enlace SSL de la reserva de direcciones URL en HTTP.SYS. Al reiniciar el equipo, se cierra cualquier conexión abierta que utilice el canal.  
  
## <a name="bind-ssl-to-a-reporting-services-url-reservation"></a>Enlazar SSL a una reserva de direcciones URL de Reporting Services  
 Los pasos siguientes no incluyen instrucciones para solicitar, generar, descargar o instalar un certificado. Debe tener un certificado instalado y disponible para usarlo. Puede elegir libremente las propiedades del certificado que especifique, la entidad de certificación de la que lo obtenga y las herramientas y utilidades que use para solicitar e instalar el certificado.  
  
 Puede utilizar la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para enlazar el certificado. Si el certificado está instalado correctamente en el almacén del equipo local, la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] lo detectará y lo mostrará en la lista **Certificados SSL** en las páginas **Dirección URL del servicio web** y **Dirección URL del Administrador de informes** .  
  
### <a name="to-configure-a-report-server-url-for-ssl"></a>Para configurar una dirección URL del servidor de informes para SSL  
  
1.  Inicie la herramienta Configuración de Reporting Services y conéctese al servidor de informes.  
  
2.  Haga clic en **Dirección URL del servicio web**.  
  
3.  Expanda la lista de certificados SSL. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] detecta los certificados de autenticación del servidor en el almacén local. Si instaló un certificado y no lo ve en la lista, puede que tenga que reiniciar el servicio. Puede utilizar los botones **Detener** e **Iniciar** en la página **Estado del servidor de informes** en la herramienta Configuración de Reporting Services para reiniciar el servicio.  
  
4.  Seleccione el certificado.  
  
5.  Haga clic en **Aplicar**.  
  
6.  Haga clic en la dirección URL para comprobar que funciona.  
  
 La configuración de la base de datos del servidor de informes es un requisito para probar la dirección URL. Si aún no ha creado la base de datos del servidor de informes, hágalo antes de probar la dirección URL.  
  
 Las reservas de direcciones URL del Administrador de informes y el servicio web del servidor de informes se configuran de forma independiente. Si también desea configurar el acceso del Administrador de informes a través de un canal cifrado con SSL, continúe con los pasos siguientes:  
  
1.  Haga clic en **Dirección URL del Administrador de informes**.  
  
2.  Haga clic en **Avanzadas**.  
  
3.  En **Varias identidades SSL para el Administrador de informes**, haga clic en **Agregar**.  
  
4.  Seleccione el certificado, haga clic en **Aceptar**y, después, haga clic en **Aplicar**.  
  
5.  Haga clic en la dirección URL para comprobar que funciona.  
  
## <a name="how-certificate-bindings-are-stored"></a>Cómo se almacenan los enlaces de certificados  
 Los enlaces de certificados se almacenarán en HTTP.SYS. También se almacenarán en una representación de los enlaces que definió el `URLReservations` sección del archivo RSReportServer.config. Los valores del archivo de configuración solo son una representación de los valores reales que se especifican en otro lugar. No modifique directamente los valores en el archivo de configuración. La configuración solo aparecerá en el archivo después de utilizar la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o el proveedor de Instrumental de administración de Windows (WMI) del servidor de informes para enlazar un certificado.  
  
> [!NOTE]  
>  Si configura un enlace con un certificado SSL en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y posteriormente desea quitar el certificado del equipo, asegúrese de quitar el enlace de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] antes de quitar el certificado del equipo. De lo contrario, no podrá quitar el enlace mediante la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o WMI y recibirá el error "Parámetro no válido". Si ya ha quitado el certificado del equipo, puede utilizar la herramienta Httpcfg.exe para quitar el enlace de HTTP.SYS. Para obtener más información sobre Httpcfg.exe, consulte la documentación del producto de Windows.  
  
 Los enlaces SSL son un recurso compartido en Microsoft Windows. Los cambios realizados por el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] u otras herramientas como el Administrador de IIS pueden afectar a otras aplicaciones ubicadas en el mismo equipo. Se recomienda usar la misma herramienta para editar los enlaces que usó para crearlos.  Por ejemplo, si creó enlaces SSL mediante el Administrador de configuración, se recomienda usar este administrador para configurar el ciclo de vida de los enlaces. Si utiliza el administrador de IIS para crear enlaces, se recomienda usar este administrador para administrar el ciclo de vida de los enlaces. Si IIS estaba instalado en el equipo antes de que se instalara [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , es recomendable que revise la configuración de SSL en IIS antes de configurar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Si quita enlaces SSL de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con el Administrador de configuración de Reporting Services, puede que los enlaces SSL ya no funcionen para los sitios web en un servidor que ejecute Internet Information Services (IIS) o en otro servidor HTTP.SYS. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] quite la siguiente clave del Registro. Cuando se quita esta clave del Registro, también se quita el enlace SSL para IIS. Sin este enlace, SSL no se proporciona para el protocolo HTTPS. Para diagnosticar este problema, use el Administrador de IIS o la utilidad de línea de comandos HTTPCFG.exe. Para resolver el problema, restaure el enlace SSL para los sitios web mediante el Administrador de IIS. Para evitar que se produzca este problema en el futuro, use el Administrador de IIS para quitar los enlaces SSL y use el Administrador de IIS para restaurar el enlace para los sitios web que desee. Para más información, consulte el artículo de la base de conocimiento [SSL no funciona después de quitar un enlace SSL (http://support.microsoft.com/kb/956209/n)](http://support.microsoft.com/kb/956209/n).  
  
## <a name="see-also"></a>Vea también  
 [Autenticación con el servidor de informes](authentication-with-the-report-server.md)   
 [Configurar y administrar un servidor de informes &#40;modo nativo de SSRS&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Archivo de configuración RSReportServer](../report-server/rsreportserver-config-configuration-file.md)   
 [Administrador de configuración de Reporting Services &#40;SUPR&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
