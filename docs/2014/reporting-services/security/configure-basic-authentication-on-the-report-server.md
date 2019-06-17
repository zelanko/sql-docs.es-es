---
title: Configurar la autenticación básica en el servidor de informes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- Basic authentication
ms.assetid: 8faf2938-b71b-4e61-a172-46da2209ff55
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 32b46265b5da376bc974b55c48bf54bad88917d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102165"
---
# <a name="configure-basic-authentication-on-the-report-server"></a>Configurar la autenticación básica en el servidor de informes
  De forma predeterminada, Reporting Services acepta solicitudes que especifican la autenticación NTLM o Negotiate. Si su implementación incluye aplicaciones cliente o exploradores que utilizan la autenticación básica, debe agregar esta autenticación a la lista de tipos admitidos. Además, si desea utilizar el Generador de informes, debe permitir el acceso anónimo a los archivos del Generador de informes.  
  
 Para configurar la autenticación básica en el servidor de informes, modifique los valores y elementos XML en el archivo RSReportServer.config. Puede copiar y pegar los ejemplos de este tema para reemplazar los valores predeterminados.  
  
 Antes de habilitar la autenticación básica, compruebe que la infraestructura de seguridad la admite. Con la autenticación básica, el servicio web del servidor de informes pasará las credenciales a la entidad de seguridad local. Si las credenciales especifican una cuenta de usuario local, la entidad de seguridad local autentica al usuario en el equipo del servidor de informes y el usuario obtendrá un token de seguridad válido para los recursos locales. Las credenciales para las cuentas de usuario de dominio se reenvían a un controlador de dominio que las autentica. El vale resultante es válido para los recursos de red.  
  
 Si desea mitigar el riesgo de que se intercepten las credenciales mientras se dirigen a un controlador de dominio de la red, se requiere cifrado en el canal, como Capa de sockets seguros (SSL). Por sí sola, la autenticación básica transmite el nombre de usuario en texto sin cifrar y la contraseña en codificación en base 64. Cuando se agrega cifrado al canal, el paquete es ilegible. Para obtener más información, vea [Configurar conexiones SSL en un servidor de informes en modo nativo](configure-ssl-connections-on-a-native-mode-report-server.md).  
  
 Después de habilitar la autenticación básica, tenga en cuenta que los usuarios no pueden seleccionar la opción **Seguridad integrada de Windows** al establecer las propiedades de conexión en un origen de datos externo que proporciona los datos para un informe. La opción estará deshabilitada en las páginas de propiedades del origen de datos.  
  
> [!NOTE]  
>  Las instrucciones siguientes están pensadas para un servidor de informes en modo nativo. Si el servidor de informes se implementa en modo integrado de SharePoint, se deben utilizar los valores de autenticación predeterminados que especifican la seguridad integrada de Windows. El servidor de informes utiliza las características internas de la extensión de autenticación de Windows predeterminada para admitir el servidor de informes en modo integrado de SharePoint.  
  
### <a name="to-configure-a-report-server-to-use-basic-authentication"></a>Para configurar un servidor de informes de modo que use la autenticación básica  
  
1.  Abra RSReportServer.config en un editor de texto.  
  
     El archivo se encuentra en  *\<unidad >:* \Program Files\Microsoft SQL Server\MSRS12. MSSQLSERVER\Reporting Services\ReportServer.  
  
2.  Busque <`Authentication`>.  
  
3.  De las estructuras XML siguientes, copie la que mejor se ajuste a sus necesidades. La primera estructura XML proporciona marcadores de posición para especificar todos los elementos, que se describen en la sección siguiente:  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsBasic>  
                       <LogonMethod>3</LogonMethod>  
                       <Realm></Realm>  
                       <DefaultDomain></DefaultDomain>  
                 </RSWindowsBasic>  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
     Si usa los valores predeterminados, puede copiar la estructura de elementos mínima:  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsBasic/>  
          </AuthenticationTypes>  
    ```  
  
4.  Péguela sobre las entradas existentes para <`Authentication`>.  
  
     Si usa varios tipos de autenticación, basta con que agregue el elemento `RSWindowsBasic`, pero no elimine las entradas correspondientes a `RSWindowsNegotiate`, `RSWindowsNTLM` o `RSWindowsKerberos`.  
  
     Para admitir el explorador Safari, no puede configurar el servidor de informes de modo que use varios tipos de autenticación. Debe especificar solo `RSWindowsBasic` y eliminar las demás entradas.  
  
     Observe que no puede utilizar `Custom` con otros tipos de autenticación.  
  
5.  Reemplace los valores vacíos para <`Realm`> o <`DefaultDomain`> cuyos valores son válidos para su entorno.  
  
6.  Guarde el archivo.  
  
7.  Si configuró una implementación escalada, repita estos pasos con los demás servidores de informes de la implementación.  
  
8.  Reinicie el servidor de informes para borrar las sesiones que estén abiertas en ese momento.  
  
## <a name="rswindowsbasic-reference"></a>Referencia de RSWindowsBasic  
 Se pueden especificar los elementos siguientes al configurar la autenticación básica.  
  
|Elemento|Obligatorio|Valores válidos|  
|-------------|--------------|------------------|  
|LogonMethod|Sí<br /><br /> Si no especifica un valor, se usará 3.|`2` = inicio de sesión en red; diseñado para servidores de alto rendimiento para autenticar las contraseñas de texto simple.<br /><br /> `3`: inicio de sesión con texto no cifrado, que conserva las credenciales de inicio de sesión en el paquete de autenticación que se envía con cada solicitud HTTP. Esto permite que el servidor suplante al usuario a la hora de establecer la conexión con otros servidores de la red. (Es el valor predeterminado).<br /><br /> Nota: Los valores 0 (para el inicio de sesión interactivo) y 1 (para el inicio de sesión por lotes) no se admiten en [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].|  
|Dominio|Opcional|Especifica una partición de recurso que incluye características de autorización y de autenticación que se utilizan para controlar el acceso a los recursos protegidos de una organización.|  
|DominioPredeterminado|Opcional|Especifica el dominio que utiliza el servidor para autenticar al usuario. Este valor es opcional, pero si lo omite, el servidor de informes utilizará el nombre de equipo como dominio. Si el equipo es miembro de dominio, ese dominio es el predeterminado. Si instaló el servidor de informes en un controlador de dominio, el dominio que se utilizará será el controlado por el equipo .|  
  
## <a name="enabling-anonymous-access-to-report-builder-application-files"></a>Habilitar el acceso anónimo a los archivos de aplicación del Generador de informes  
 El Generador de informes utiliza la tecnología ClickOnce para descargar e instalar los archivos de aplicación en un equipo cliente. Cuando se inicie en el equipo cliente, el iniciador de la aplicación ClickOnce realizará una solicitud para los archivos de aplicación adicionales en el equipo del servidor de informes. Si el servidor de informes se configura para la autenticación básica, el iniciador de la aplicación ClickOnce producirá un error en la comprobación de la autenticación porque no admite este tipo de autenticación.  
  
 Para evitar este problema, puede configurar el acceso anónimo a los archivos de programa del Generador de informes. De esta forma, permite a ClickOnce omitir la comprobación de autenticación al recuperar sus archivos. Para habilitar el acceso anónimo, realice el siguiente procedimiento:  
  
-   Compruebe que el servidor de informes esté configurado para la autenticación básica.  
  
-   Cree una carpeta Bin debajo de ReportBuilder y copie cuatro ensamblados en ella.  
  
-   Agregue el elemento `IsReportBuilderAnonymousAccessEnabled` a RSReportServer.config y establézcalo en `True`. Después de guardar el archivo, el servidor de informes crea un nuevo extremo para el Generador de informes. El extremo se utiliza internamente para tener acceso a los archivos de programa y no tiene ninguna interfaz de programación que se pueda utilizar en el código. Tener un extremo independiente permite al Generador de informes ejecutarse en su propio dominio de aplicación dentro del límite del proceso del servicio del servidor de informes.  
  
-   Opcionalmente, puede especificar una cuenta con privilegios mínimos para procesar las solicitudes en un contexto de seguridad diferente del servidor de informes. Esta cuenta se convierte en la cuenta anónima para tener acceso a los archivos del Generador de informes en un servidor de informes. La cuenta establece la identidad del subproceso en el proceso de trabajo de ASP.NET. Las solicitudes que se ejecutan en ese subproceso se pasan al servidor de informes sin comprobar la autenticación. Esta cuenta es equivalente a la cuenta IUSR_\<machine > cuenta en Internet Information Services (IIS), que se usa para establecer el contexto de seguridad para el trabajo de ASP.NET procesa cuando se habilitan el acceso anónimo y la suplantación. Para especificar la cuenta, agréguela a un archivo Web.config del Generador de informes.  
  
 El servidor de informes se debe configurar para la autenticación básica si desea habilitar el acceso anónimo a los archivos de programa del Generador de informes. Si el servidor de informes no está configurado para la autenticación básica, obtendrá un error al intentar habilitar el acceso anónimo.  
  
 Para obtener más información sobre los problemas de autenticación y el Generador de informes, vea [Configurar el acceso al Generador de informes](../report-server/configure-report-builder-access.md).  
  
#### <a name="to-configure-report-builder-access-on-a-report-server-configured-for-basic-authentication"></a>Para configurar el acceso del generador de informes en un servidor de informes configurado para la autenticación básica  
  
1.  Compruebe que el servidor de informes está configurado para la autenticación básica comprobando la configuración de autenticación en el archivo RSReportServer.config.  
  
2.  Cree una carpeta BIN debajo de la carpeta ReportBuilder. De forma predeterminada, esta carpeta se encuentra en :\Archivos de programa\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\ReportBuilder.  
  
3.  Copie los ensamblados siguientes de la carpeta ReportServer\Bin en la carpeta ReportBuilder\BIN:  
  
     Microsoft.ReportingServices.Diagnostics.dll  
  
     Microsoft.ReportingServices.Interfaces.dll  
  
     ReportingServicesAppDomainManager.dll  
  
     RSHttpRuntime.dll  
  
4.  Si lo desea, cree un archivo Web.config para procesar las solicitudes del Generador de informes bajo una cuenta anónima:  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
    <system.web>  
    <authentication mode="Windows" />    
    <identity impersonate="true " userName="username" password="password"/>  
    </system.web>  
    </configuration>  
    ```  
  
     El modo de autenticación debe estar establecido en `Windows` si incluye un archivo Web.config.  
  
     `Identity impersonate` puede ser `True` o `False`.  
  
    -   Establézcalo en `False` si no desea que ASP.NET lea el token de seguridad. La solicitud se ejecutará en el contexto de seguridad del servicio del servidor de informes.  
  
    -   Establézcalo en `True` si desea que ASP.NET lea el token de seguridad del nivel de host. Si lo establece en `True`, también debe especificar `userName` y `password` para designar una cuenta anónima. Las credenciales que especifique determinarán el contexto de seguridad bajo el que se emite la solicitud.  
  
5.  Guarde el archivo Web.config en la carpeta ReportBuilder\bin.  
  
6.  Abra el archivo RSReportServer.config, en la sección Servicios, busque `IsReportManagerEnabled` y agregue el valor siguiente debajo de él:  
  
    ```  
    <IsReportBuilderAnonymousAccessEnabled>True</IsReportBuilderAnonymousAccessEnabled>  
    ```  
  
7.  Guarde el archivo RSReportServer.config y ciérrelo.  
  
8.  Reinicie el servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Dominios de aplicación para las aplicaciones del servidor de informes](../report-server/application-domains-for-report-server-applications.md)   
 [Seguridad y protección de Reporting Services](reporting-services-security-and-protection.md)  
  
  
