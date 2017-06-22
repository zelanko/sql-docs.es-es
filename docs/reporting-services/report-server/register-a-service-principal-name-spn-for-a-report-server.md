---
title: Registrar un nombre Principal de servicio (SPN) para un servidor de informes | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dda91d4f-77cc-4898-ad03-810ece5f8e74
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9518d1bd3ee166a0f21292ca08130214afc841be
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="register-a-service-principal-name-spn-for-a-report-server"></a>Registrar un nombre principal de servicio (SPN) para un servidor de informes
  Si está implementando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en una red que usa el protocolo Kerberos para la autenticación mutua, debe crear un nombre principal de servicio (SPN) para el servicio Servidor de informes si lo configura para que se ejecute como una cuenta de usuario de dominio.  
  
## <a name="about-spns"></a>Acerca de los nombres principales de servicio  
 Un SPN es un identificador único para un servicio en una red que utiliza la autenticación Kerberos. Está compuesto de una clase de servicio, un nombre de host y un puerto. En una red que utiliza la autenticación Kerberos, un SPN para el servidor se debe registrar en una cuenta de equipo integrada (como NetworkService o LocalSystem) o en una cuenta de usuario. Los SPN se registran automáticamente para las cuentas integradas. Sin embargo, al ejecutar un servicio en una cuenta de usuario de dominio, debe registrar manualmente el SPN para la cuenta que desea utilizar.  
  
 Para crear un SPN, puede emplear la utilidad de línea de comandos **SetSPN** . Para obtener más información, vea:  
  
-   [Setspn](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx) (http://technet.microsoft.com/es-es/library/cc731241(WS.10).aspx).  
  
-   [Service Principal Names (SPNs) SetSPN Syntax (Setspn.exe) (Sintaxis de SetSPN para nombres de entidad de seguridad de servicio [SPN])](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx) (http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx).  
  
 Debe ser administrador de dominio si desea ejecutar la utilidad en el controlador de dominio.  
  
## <a name="syntax"></a>Sintaxis  
 La sintaxis de comandos para utilizar la utilidad SetSPN con el fin de crear un SPN para el servidor de informes es similar a la siguiente:  
  
```  
Setspn -s http/<computername>.<domainname>:<port> <domain-user-account>  
```  
  
 **SetSPN** está disponible con Windows Server. El argumento **-s** agrega un SPN después de validar que no existe ningún duplicado. **NOTA: -s** está disponible en Windows Server a partir de Windows Server 2008.  
  
 **HTTP** es la clase de servicio. El servicio web del servidor de informes se ejecuta en HTTP.SYS. Una consecuencia de la creación de un SPN para HTTP es que a todas las aplicaciones web del mismo equipo que se ejecutan en HTTP.SYS (incluidas las que se hospedan en IIS) se les concederán vales en función de la cuenta de usuario de dominio. Si esos servicios se ejecutan en una cuenta diferente, se producirá un error en las solicitudes de autenticación. Para evitar este problema, asegúrese de configurar todas las aplicaciones HTTP para ejecutarse en la misma cuenta, o considere la posibilidad de crear los encabezados de host para cada aplicación y crear después SPN independientes para cada encabezado de host. Al configurar los encabezados de host, se requieren cambios de DNS con independencia de la configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Los valores que especifique para \< *computername*>, \< *domainname*>, y \< *puerto*> identifican la dirección de red única del equipo que hospeda el servidor de informes. Puede ser un nombre de host local o un nombre de dominio completo (FQDN). Si sólo tiene un dominio y usa el puerto 80, puede omitir \< *domainname*> y \< *puerto*> desde la línea de comandos. \<*cuenta de usuario de dominio*> es la cuenta de usuario en la que se ejecuta el servicio servidor de informes y para que se debe registrar el SPN.  
  
## <a name="register-an-spn-for-domain-user-account"></a>Registrar un nombre principal de servicio para la cuenta de usuario de dominio  
  
#### <a name="to-register-an-spn-for-a-report-server-service-running-as-a-domain-user"></a>Para registrar un SPN para un servicio Servidor de informes que se ejecute como un usuario de dominio  
  
1.  Instale [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y configure el servicio Servidor de informes para ejecutarse como una cuenta de usuario de dominio. Observe que los usuarios no podrán conectarse al servidor de informes hasta que complete los pasos siguientes.  
  
2.  Inicie sesión en el controlador de dominio como administrador de dominio.  
  
3.  Abra una ventana de símbolo del sistema.  
  
4.  Copie el comando siguiente, reemplazando los valores de los marcadores de posición con valores reales que sean válidos para su red:  
  
    ```  
    Setspn -s http/<computer-name>.<domain-name>:<port> <domain-user-account>  
    ```  
  
     Por ejemplo: `Setspn -s http/MyReportServer.MyDomain.com:80 MyDomainUser`  
  
5.  Ejecute el comando.  
  
6.  Abra el archivo **RsReportServer.config** y busque la sección `<AuthenticationTypes>` .  
  
7.  Agregue `<RSWindowsNegotiate/>` como primera entrada en esta sección para habilitar NTLM.  
  
## <a name="see-also"></a>Vea también  
 [Configurar una cuenta de servicio &#40;Administrador de configuración de SSRS&#41;](http://msdn.microsoft.com/library/25000ad5-3f80-4210-8331-d4754dc217e0)   
 [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Administrar un servidor de informes en modo nativo de Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
