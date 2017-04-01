---
title: "Notificaciones del servicio de token de Windows (c2WTS) y Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "06/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "c2wts.exe.config"
  - "en modo SharePoint"
  - "C2WTS"
  - "WSS_WPG"
ms.assetid: 4d380509-deed-4b4b-a9c1-a9134cc40641
caps.latest.revision: 17
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 16
---
# Notificaciones del servicio de token de Windows (c2WTS) y Reporting Services
  Necesita Notificaciones del servicio de token de Windows (c2WTS) de SharePoint con el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] si quiere usar la autenticación de Windows para los orígenes de datos que están fuera de la granja de SharePoint. Esto es cierto incluso si el usuario obtiene acceso a los orígenes de datos con la autenticación de Windows porque la comunicación entre el servicio front-end web (WFE) y el servicio compartido de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se realizará siempre con autenticación de notificaciones.  
  
 c2WTS es necesario aunque los orígenes de datos estén en el mismo equipo que el servicio compartido. Sin embargo, en este escenario no es necesaria la delegación restringida.  
  
 Los tokens creados por c2WTS funcionarán solo con delegación restringida (limitaciones a servicios concretos) y la opción de configuración "Usar cualquier protocolo de autenticación". Como se indicaba anteriormente, si los orígenes de datos están en el mismo equipo que el servicio compartido, la delegación restringida no es necesaria.  
  
 Si en su entorno se usa la delegación limitada de Kerberos, el servicio SharePoint Server y los orígenes de datos externos deben residir en el mismo dominio de Windows. Cualquier servicio que use Notificaciones del servicio de token de Windows (c2WTS) debe emplear la delegación **restringida** de Kerberos para permitir que c2WTS use la transición del protocolo Kerberos para traducir las notificaciones en credenciales de Windows. Estos requisitos son verdaderos para todos los servicios compartidos de SharePoint. Para obtener más información, vea [Planear la autenticación Kerberos en SharePoint 2013](http://technet.microsoft.com/library/ee806870.aspx).  
  
 El procedimiento se resume en este tema.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2016 &#124; SharePoint 2013|  
  
## Requisitos previos  
  
> [!NOTE]  
>  Nota: algunos pasos de configuración pueden cambiar o no funcionar en algunas topologías de granja. Por ejemplo, una instalación de un solo servidor no admite los servicios c2WTS de Windows Identity Foundation, por lo que las notificaciones a los escenarios de delegación de token de Windows no son posibles con esta configuración de granja. 

> [!IMPORTANT] Si usa Power View para trabajar con libros de Power Pivot, debe realizar una configuración adicional para [Office Online Server](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx). Para obtener más información, vea las siguientes notas del producto. 
>
> - [Implementación de SQL Server 2016 PowerPivot y Power View en SharePoint 2016](../../analysis-services/instances/install-windows/deploying-sql-server-2016-powerpivot-and-power-view-in-sharepoint-2016.md)
> 
> - [Implementación de SQL Server 2016 PowerPivot y Power View en una granja de SharePoint 2016 de niveles múltiples](../../analysis-services/instances/install-windows/deploy powerpivot and power view - multi-tier sharepoint 2016 farm.md)
  
### Pasos básicos necesarios para configurar c2WTS  
  
1.  Configure la cuenta de servicio c2WTS. Agregue la cuenta de servicio al grupo de administradores local en cada servidor de aplicaciones ejecuta c2WTS. Además, compruebe que la cuenta tiene los siguientes derechos de directiva de seguridad local:  
  
    -   Actuar como parte del sistema operativo  
  
    -   Suplantar un cliente después de autenticación  
  
    -   Iniciar sesión como servicio  
  
2.  Configure la delegación para la cuenta de servicio de c2WTS. La cuenta necesita una delegación restringida con transición de protocolo así como permisos para delegar a los servicios con los que requiere comunicación (es decir, motor de SQL Server, SQL Server Analysis Services). Para configurar la delegación puede utilizar el complemento Usuarios y equipos de Active Directory.  

    > [!IMPORTANT] Las opciones que configure para la cuenta de servicio de C2WTS en la pestaña de delegación deben coincidir con las de la cuenta de servicio de Reporting Services. Por ejemplo, si permite que la cuenta de servicio de C2WTS delegue en un servicio de SQL, debe hacer lo mismo en la cuenta de servicio de Reporting Services.
  
    1.  Haga clic con el botón secundario en cada cuenta de servicio y abra el cuadro de diálogo de propiedades. En el cuadro de diálogo, haga clic en la pestaña **Delegación** .  
  
        > [!NOTE]  
        >  Nota: La pestaña de delegación solo está visible si el objeto tiene asignado un nombre de entidad de seguridad de servicio (SPN). c2WTS no requiere un SPN en la cuenta de c2WTS pero, sin un SPN, la pestaña **Delegación** no estará visible. Una manera alternativa de configurar la delegación restringida es utilizar una herramienta como **ADSIEdit**.  
  
    2.  Las opciones de configuración clave en la pestaña de delegación son las siguientes:  
  
        -   Seleccionar "Confiar en este usuario para la delegación solo a los servicios especificados"  
  
        -   Seleccionar "Usar cualquier protocolo de autenticación"  

    3. Seleccione **Agregar** para agregar un servicio en el que delegar.
    
    4. Seleccione **Usuarios o equipos...*** y especifique la cuenta que hospeda el servicio. Por ejemplo, si un servidor SQL Server se ejecuta en una cuenta denominada *sqlservice*, escriba `sqlservice`.
    
    5. Seleccione la lista de servicios. Esto mostrará los SPN disponibles en esa cuenta. Si el servicio no está indicado en la cuenta, es posible que falte o que esté en otra cuenta. Puede usar la utilidad SetSPN para ajustar los SPN.
    
    6. Seleccione Aceptar para salir de los cuadros de diálogo.
  
3.  Configurar "AllowedCallers" de c2WTS  
  
     c2WTS requiere que las identidades de los "autores de llamadas" estén enumeradas explícitamente en el archivo de configuración, **c2WTShost.exe.config**. c2WTS no acepta solicitudes de todos los usuarios autenticados en el sistema a menos que esté configurado para ello. En este caso el "autor de la llamada" es el grupo de Windows WSS_WPG. El archivo c2WTShost.exe.confi se guarda en la ubicación siguiente:  
     
     > [!NOTE] Si cambia la cuenta de servicio en la Administración central de SharePoint para el servicio C2WTS, agregará esa cuenta al grupo WSS_WPG.
  
     **\Archivos de programa\Windows Identity Foundation\v3.5\c2WTShost.exe.config**  
  
     A continuación se muestra un ejemplo del archivo de configuración:  
  
    ```  
    <configuration>  
      <windowsTokenService>  
        <!--  
            By default no callers are allowed to use the Windows Identity Foundation Claims To NT Token Service.  
            Add the identities you wish to allow below.  
          -->  
        <allowedCallers>  
          <clear/>  
          <add value="WSS_WPG" />  
        </allowedCallers>  
      </windowsTokenService>  
    </configuration>  
    ```    
4.  Iniciar las "Notificaciones al servicio de token de Windows" de SharePoint: inicie las Notificaciones al servicio de token de Windows mediante Administración central de SharePoint en la página **Administrar servicios en el servidor** . El servicio se debe iniciar en el servidor que realizará la acción. Por ejemplo, si tiene un servidor que es un servidor web front-end (WFE) y otro servidor que es un servidor de aplicaciones que tiene la ejecución del servicio compartido de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , solo tiene que iniciar c2WTS en el servidor de aplicaciones. c2WTS no es necesario en el servidor web front-end (WFE).  
  
## Vea también  
 [Información general de Notificaciones al servicio de token de Windows (C2WTS)](http://msdn.microsoft.com/library/ee517278.aspx)   
 [Planear la autenticación Kerberos en SharePoint 2013](http://technet.microsoft.com/library/ee806870.aspx)  
  
  