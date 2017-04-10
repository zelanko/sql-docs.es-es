---
title: "Configurar Analysis Services y Delegaci&#243;n limitada de Kerberos (KCD) | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0006e143-d3ba-4d10-a415-e42c45e2bb0a
caps.latest.revision: 20
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 19
---
# Configurar Analysis Services y Delegaci&#243;n limitada de Kerberos (KCD)
  La delegación limitada de Kerberos (KCD) es un protocolo de autenticación que se puede configurar con la autenticación de Windows para delegar las credenciales de cliente de servicio a servicio en todo el entorno. KCD requiere una infraestructura adicional, por ejemplo, un controlador de dominio y una configuración adicional del entorno. KCD es un requisito en algunos escenarios que implican datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] con SharePoint 2016. En SharePoint 2016, Excel Services se ha trasladado de la granja de SharePoint a un nuevo servidor independiente, **Office Online Server**. Puesto que Office Online Server es independiente, se hace más necesaria una forma de delegar las credenciales de cliente en los escenarios típicos de dos saltos.  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2016|  
  
## Información general  
 KCD permite a una cuenta suplantar a otra con el fin de proporcionar acceso a los recursos. La cuenta de suplantación corresponde a una cuenta de servicio asignada a una aplicación web o a la cuenta de equipo de un servidor web, mientras que la cuenta suplantada es una cuenta de usuario que requiere acceso a los recursos. KCD trabaja en el nivel de servicio, de modo que la cuenta de suplantación puede conceder acceso a unos servicios concretos de un servidor y denegárselo a la vez a otros servicios del mismo servidor o a servicios en otros servidores.  
  
 Las secciones de este tema abarcan escenarios comunes con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] donde se requiere KCD, así como una implementación de servidor de ejemplo y un resumen general de lo que se debe instalar y configurar. Vea la sección [Más información y contenido de la comunidad](#bkmk_moreinfo) para obtener vínculos a información más detallada sobre las tecnologías implicadas, como controladores de dominio y KCD.  
  
## Escenario 1: libro como origen de datos (WDS).  
 ![see 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "see 1") Office Online Server abre un libro de Excel y ![see 2](../../../analysis-services/instances/install-windows/media/ssas-callout2.png "see 2") detecta una conexión de datos a otro libro. Office Online Server envía una solicitud al servicio de redirector de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] ![see 3](../../../analysis-services/instances/install-windows/media/ssas-callout3.png "see 3") para abrir el segundo libro y los datos ![see 4](../../../analysis-services/instances/install-windows/media/ssas-callout4.png "see 4").  
  
 En este escenario, las credenciales de usuario se deben delegar de Office Online Server al servicio de redirector [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] de SharePoint en SharePoint.  
  
 ![workbook as a data source](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-wds.png "workbook as a data source")  
  
## Escenario 2: modelo tabular de Analysis Services vinculado a un libro de Excel  
 Un modelo tabular de Analysis Services ![see 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "see 1") está vinculado a un libro de Excel que contiene un modelo de Power Pivot. En este escenario, cuando [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] carga el modelo tabular, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] detecta el vínculo al libro. Al procesar el modelo, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] envía una solicitud de consulta a SharePoint para cargar el libro. En este escenario, **no** es necesario delegar las credenciales de cliente de Analysis Services a SharePoint, pero una aplicación cliente puede sobrescribir la información del origen de datos en un enlace temporal. Si la solicitud de enlace temporal especifica que se debe suplantar al usuario actual, se deberán delegar las credenciales de usuario, lo que requiere configurar KCD entre [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y SharePoint.  
  
 ![office online server](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-oos.png "office online server")  
  
## Ejemplo de implementación de KCD con Office Online Server y Analysis Services  
 En esta sección se describe una implementación de ejemplo con cuatro equipos. En las siguientes secciones se resumen los pasos clave de instalación y configuración para cada equipo. Antes de iniciar las implementaciones, se recomienda que los equipos estén actualizados con las aplicaciones de revisiones del sistema operativo. Además, el usuario debe conocer los nombres de los equipos porque son necesarios en algunos pasos de la configuración.  
  
-   Controlador de dominio  
  
-   Motor de base de datos de SQL Server y Analysis Services en modo PowerPivot. La instancia del motor de base de datos se utilizará para las bases de datos de contenido de SharePoint.  
  
-   SharePoint Server 2016  
  
-   Office Online Server  
  
 ![domain controller](../../../analysis-services/instances/install-windows/media/ssas-kcd-domainserver-icon.png "domain controller")  
  
### Controlador de dominio  
 A continuación se muestra un resumen de lo que se debe instalar para el controlador de dominio (DC).  
  
-   **Rol:** Servicios de dominio de Active Directory. Para obtener información general, vea [Configuring Active Directory (AD DS) in Windows Server 2012](http://sharepointgeorge.com/2012/configuring-active-directory-ad-ds-in-windows-server-2012/) (Configuración de Active Directory (AD DS) en Windows Server 2012).  
  
-   **Rol:** servidor DNS.  
  
-   **Característica:** características de .NET Framework 3.5/.NET Framework 3.5.  
  
-   **Característica:** Herramientas de administración remota del servidor/Herramientas de administración de roles.  
  
-   Configure Active Directory para crear un nuevo bosque y unir los equipos al dominio. Antes de intentar agregar otros equipos al dominio privado, deberá configurar los DNS de los equipos cliente en la dirección IP del controlador de dominio. En la máquina del controlador de dominio, ejecute `ipconfig /all` para obtener las direcciones IPv4 e IPv6 para el paso siguiente.  
  
-   Se recomienda configurar las ambas direcciones IPv4 e IPv6. Puede hacerlo en el panel de control de Windows:  
  
    1.  Haga clic en **Centro de redes y recursos compartidos**.  
  
    2.  Haga clic en la conexión Ethernet.  
  
    3.  Haga clic en **Propiedades**.  
  
    4.  Haga clic en **Protocolo de Internet versión 6 (TCP/IPv6)**.  
  
    5.  Haga clic en **Propiedades**.  
  
    6.  Haga clic en **Usar las siguientes direcciones de servidor DNS**.  
  
    7.  Escriba la dirección IP mediante el comando "ipconfig".  
  
    8.  Haga clic en el botón **Avanzadas**, en la pestaña **DNS** y compruebe que los sufijos DNS sean correctos.  
  
    9. Haga clic en **Anexar estos sufijos DNS**.  
  
    10. Repita los pasos para la dirección IPv4.  
  
-   **Nota:** Puede unir equipos al dominio desde el Panel de control de Windows, en la configuración del sistema. Para obtener más información, vea [How To Join Windows Server 2012 to a Domain](http://social.technet.microsoft.com/wiki/contents/articles/20260.how-to-join-windows-server-2012-to-a-domain.aspx) (Cómo unir Windows Server 2012 a un dominio).  
  
 ![ssas server in powerpivot mode](../../../analysis-services/instances/install-windows/media/ssas-kcd-powerpivotserver-icon.png "ssas server in powerpivot mode")  
  
### Motor de base de datos de SQL Server 2016 y Analysis Services en modo PowerPivot  
 A continuación se muestra un resumen de lo que se debe instalar en el equipo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 ![nota](../../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "nota") En el Asistente para instalación de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], en el modo Power Pivot, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se instala como parte del flujo de trabajo de selección de características.  
  
1.  Ejecute el Asistente para instalación de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] y, en la página de selección de características, haga clic en el motor de base de datos, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], y en las Herramientas de administración. En una configuración posterior del Asistente para instalación puede especificar el modo [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
2.  Para la configuración de las instancias, configure una con nombre "POWERPIVOT".  
  
3.  En la página Configuración de Analysis Services, configure el servidor de Analysis Services para el modo **Power Pivot** y agregue el **nombre de equipo** de Office Online Server a la lista de administradores de servidores de Analysis Services. Para obtener más información, consulte [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
4.  Tenga en cuenta que el tipo de objeto "Equipo" no se incluye en la búsqueda de forma predeterminada. Haga clic en ![click objects to add computer account](../../../analysis-services/instances/install-windows/media/ss-objects-button.png "click objects to add computer account") para agregar el objeto "Equipo".  
  
     ![add computer accounts as ssas administrators](../../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "add computer accounts as ssas administrators")  
  
5.  Cree los nombres de entidad de seguridad de servicio (SPN) para la instancia de Analysis Services.  
  
     Comandos útiles de SPN:  
  
    -   Indicar el SPN de un nombre de cuenta específico que ejecuta el servicio en cuestión: `SetSPN -l <account-name>`  
  
    -   Establecer un SPN de un nombre de cuenta que ejecuta el servicio en cuestión: `SetSPN -a <SPN> <account-name>`  
  
    -   Eliminar un SPN de un nombre de cuenta específico que ejecuta el servicio en cuestión: `SetSPN -D <SPN> <account-name>`  
  
    -   Buscar SPN duplicados: `SetSPN -X`  
  
     El formato del SPN para la instancia de PowerPivot será el siguiente:  
  
    ```  
    MSSQLSvc.3/<Fully Qualified Domain Name (FQDN)>:POWERPIVOT  
    MSSQLSvc.3/<NetBIOS Name>:POWERPIVOT  
    ```  
  
     Donde los nombres FQDN y NetBIOS son el nombre del equipo en el que reside la instancia. Estos SPN se colocarán en la cuenta de dominio que se utiliza para la cuenta de servicio.  Si utiliza el servicio de red, el sistema local o el identificador de servicio, deberá colocar el SPN en la cuenta de equipo de dominio.  Si utiliza una cuenta de usuario de dominio, deberá colocar el SPN en dicha cuenta.  
  
6.  Cree el SPN para el servicio SQL Browser en el equipo de Analysis Services.  
  
     [Más información](https://support.microsoft.com/en-us/kb/950599)  
  
7.  **Configure las opciones de la delegación restringida** en la cuenta de servicio de Analysis Services para cualquier origen externo desde el que realice las actualizaciones, como archivos de SQL Server o Excel. En la cuenta de servicio de Analysis Services, debe asegurarse de establecer las opciones siguientes.  
  
     **Nota:** Si no ve la pestaña de delegación de la cuenta en Usuarios y equipos de Active Directory, significa que en dicha cuenta no hay ningún SPN.  Puede agregar un SPN falso para que aparezca como `my/spn`.  
  
     **Confiar en este usuario para la delegación solo a los servicios especificados** y **Usar cualquier protocolo de autenticación**.  
  
     Esto se conoce como delegación restringida y es necesaria porque el token de Windows se originará a partir de una Notificación del servicio de token de Windows (C2WTS), que requiere delegación restringida con transición de protocolo.  
  
     ![Analysis Services - Constrained Delegation](../../../analysis-services/instances/install-windows/media/analysis-services-constrained-delegation.png "Analysis Services - Constrained Delegation")  
  
     También deberá agregar los servicios para los que aplicará la delegación. Esto variará en función de su entorno.  
  
### Office Online Server  
  
1.  Office Online Server  
  
2.  **Configure Office Online Server** para conectarse al servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Recuerde que la cuenta de equipo de Office Online Server debe ser un administrador en el servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Esto se trata en una sección anterior de este tema sobre la instalación del servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
    1.  En Office Online Server, abra una ventana de PowerShell con privilegios administrativos y ejecute el siguiente comando.  
  
    2.  `New-OfficeWebAppsExcelBIServer –ServerId <AS instance name>`  
  
    3.  Ejemplo: `New-OfficeWebAppsExcelBIServer –ServerId "MTGQLSERVER-13\POWERPIVOT"`  
  
3.  **Configure Active Directory** para permitir que la cuenta de equipo de Office Online Server pueda suplantar a usuarios para la cuenta de servicio de SharePoint. Por lo tanto, establezca la propiedad de delegación en la entidad de seguridad que ejecute el grupo de aplicaciones de los servicios web de SharePoint, en Office Online Server. Los comandos de PowerShell de esta sección requieren los objetos de Active Directory (AD) PowerShell.  
  
    1.  Obtener la identidad de Active Directory de Office Online Server  
  
        ```  
        $computer1 = Get-ADComputer -Identity [ComputerName]  
        ```  
  
         Para buscar el nombre de esta entidad de seguridad, vaya a Administrador de tareas/Detalles/Nombre de usuario de w3wp.exe. Por ejemplo, "svcSharePoint".  
  
        ```  
        Set-ADUser svcSharePoint -PrincipalsAllowedToDelegateToAccount $computer1  
  
        ```  
  
    2.  Para comprobar que la propiedad se haya establecido correctamente, haga lo siguiente:  
  
    3.  ```  
        Get-ADUser svcSharePoint –Properties PrincipalsAllowedToDelegateToAccount  
        ```  
  
4.  **Configure las opciones de la delegación restringida** en la cuenta de Office Online Server para la instancia de Power Pivot de Analysis Services. Debe ser la cuenta del equipo en el que se ejecuta Office Online Server. En la cuenta de Office Online Service, debe asegurarse de establecer las opciones siguientes.  
  
     **Nota:** Si no ve la pestaña de delegación de la cuenta en Usuarios y equipos de Active Directory, significa que en dicha cuenta no hay ningún SPN.  Puede agregar un SPN falso para que aparezca como `my/spn`.  
  
     **Confiar en este usuario para la delegación solo a los servicios especificados** y **Usar cualquier protocolo de autenticación**.  
  
     Esto se conoce como delegación restringida y es necesaria porque el token de Windows se originará a partir de una Notificación del servicio de token de Windows (C2WTS), que requiere delegación restringida con transición de protocolo.  A continuación, deberá permitir la delegación en los SPN de MSOLAPSvc.3 y MSOLAPDisco.3 creados anteriormente.  
  
5.  Configurar Notificaciones del servicio de token de Windows (C2WTS) **Esto es necesario para el escenario 1**. Para obtener más información, vea [Información general sobre Claims to Windows Token Service (c2WTS)](https://msdn.microsoft.com/en-us/library/ee517278.aspx).  
  
6.  **Configure las opciones de la delegación restringida** en la cuenta de servicio de C2WTS.  La configuración debe corresponderse con la establecida en el paso 4.  
  
 ![sharepoint server](../../../analysis-services/instances/install-windows/media/ssas-kcd-sharepointserver-icon.png "sharepoint server")  
  
### SharePoint Server 2016  
 A continuación se muestra un resumen de la instalación de SharePoint Server.  
  
1.  Ejecutar el instalador de requisitos previos de SharePoint  
  
2.  Ejecute la instalación de SharePoint y seleccione el rol de instalación **Granja de servidor único**.  
  
3.  Ejecute el complemento de PowerPivot para SharePoint (spPowerPivot16.msi). Para obtener más información, vea [Instalar o desinstalar el complemento Power Pivot para SharePoint &#40;SharePoint 2016&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
4.  Ejecute el Asistente para configuración de PowerPivot. Vea [Herramientas de configuración de Power Pivot](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
5.  Conecte SharePoint a Office Online Server.    ??Configure_xlwac_on_SPO.ps1 ??  
  
6.  Configure los proveedores de autenticación de SharePoint para Kerberos. **Esto es necesario para el escenario 1**. Para obtener más información, vea [Planear la autenticación Kerberos en SharePoint 2013](https://technet.microsoft.com/en-us/library/ee806870.aspx).  
  
##  <a name="bkmk_moreinfo"></a> Más información y contenido de la comunidad  
 [Kerberos para la administración de disponibilidad](http://blogs.technet.com/b/askds/archive/2008/03/06/kerberos-for-the-busy-admin.aspx)  
  
 [Descripción de Kerberos de dos saltos](http://blogs.technet.com/b/askds/archive/2008/06/13/understanding-kerberos-double-hop.aspx)  
  
 [Contenido relacionado con .NET y SharePoint](http://sbrickey.com/Tech/Blog/Post/Kerberos_Primer)  
  
 [Delegación limitada de Kerberos basada en recursos](http://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)  
  
 [CONCEPTOS BÁSICOS DE KERBEROS: vídeos](http://blog.martinlund.it/kerberos-primer/)  
  
 [Microsoft® Kerberos Configuration Manager para SQL Server®](http://www.microsoft.com/en-us/download/details.aspx?id=39046)  
  
  