---
title: Configurar Reporting Services para usar un nombre alternativo del sujeto | Documentos de Microsoft
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ce458f9f-4b4f-4a58-aa75-9a90dda1e622
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4c4d975e93e77f43c481b44644faaa310963527b
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name"></a>Configuración de Reporting Services para utilizar un nombre alternativo del asunto
  En este tema se explica cómo configurar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) para usar un nombre alternativo del asunto (SAN) modificando el archivo rsreportserver.config y usando la herramienta Netsh.exe.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] |  
  
 Las instrucciones son válidas para la dirección URL del servicio de generación de informes y para la dirección URL del servicio web.  
  
 Para utilizar el SAN, el certificado SSL debe estar registrado en el servidor, firmado y tener la clave privada. No puede utilizar un certificado autofirmado  
  
 Las direcciones URL en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se pueden configurar para utilizar un certificado SSL. Normalmente, un certificado solo tiene un nombre de asunto, lo que permite solo una dirección URL para una sesión SSL (Secure Sockets Layer). El SAN es un campo adicional del certificado que permite a un servicio SSL escuchar y ser válido para varias direcciones URL, y compartir el puerto SSL con otras aplicaciones. El SAN es tiene un aspecto parecido a lo siguiente: www.s2.com.  
  
 Para más información sobre la configuración de SSL para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Configurar conexiones SSL en un servidor de informes en modo nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md).  
  
### <a name="configure-ssrs-to-use-a-subject-alternative-name-for-web-service-url"></a>Configure SSRS para utilizar un nombre alternativo del asunto para la dirección URL del servicio web  
  
1.  Inicie el Administrador de configuración de Reporting Services.  
  
     Para obtener más información, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  En la página **Dirección URL del servicio web** , seleccione un puerto SSL y un certificado SSL.  
  
     ![Administrador de configuración de Reporting Services](../../reporting-services/report-server-sharepoint/media/reportingservices-configurationmanager.png "Administrador de configuración de Reporting Services")  
  
     El administrador de configuración registra el certificado SSL para el puerto.  
  
3.  Abra el archivo rsreportserver.config.  
  
     Para SSRS en el modo nativo, el archivo se encuentra predeterminadamente en la carpeta siguiente.  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
4.  Copie la sección de la URL para la aplicación de servicios web del servidor de informes.  
  
     Por ejemplo, la siguiente es la sección URL original.  
  
    ```  
        <URL>  
         <UrlString>https://localhost:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
     El siguiente es la sección URL modificada.  
  
    ```  
    <URL>  
         <UrlString>https://www.s1.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
        <URL>  
         <UrlString>https://www.s2.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
5.  Guarde el archivo rsreportserver.config.  
  
6.  Inicie un símbolo del sistema como administrador y ejecute la herramienta Netsh.exe.  
  
    ```  
    C:\windows\system32\netsh  
    ```  
  
7.  Cambie al contexto http escribiendo lo siguiente.  
  
    ```  
    Netsh>http  
    ```  
  
8.  Muestre las urlacls existentes escribiendo lo siguiente.  
  
    ```  
    Netsh http>show urlacl  
    ```  
  
     Aparece una entrada como la siguiente.  
  
    ```  
    Reserved URL            : https:// www.s1.com:443/ReportServer/  
        User: NT SERVICE\ReportServer  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;S-1-5-80-1234567890-123456789-123456789-123456789-1234567890)  
    ```  
  
     Una urlacl es una DACL (lista de control de acceso discrecional) para una dirección URL reservada.  
  
9. Cree una nueva entrada para el nombre alternativo del asunto, con el mismo usuario y SDDL que la entrada existente, escribiendo lo siguiente.  
  
    ```  
    netsh http>add urlacl  url=https://www.s2.com:443/ReportServer    
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-1234567980-12346579-123456789-123456789-1234567890)  
  
    ```  
  
10. En la página **Estado del servidor de informes** del Administrador de configuración de Reporting Services, haga clic en **Detener** y, a continuación, haga clic en **Iniciar** para reiniciar el servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
