---
title: Configurar Analysis Services y limitada de Kerberos (KCD) de delegación | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cc8c2ee84c8210adc3a52d81deff5edf6d3f542f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52811157"
---
# <a name="configure-analysis-services-and-kerberos-constrained-delegation-kcd"></a>Configurar Analysis Services y Delegación limitada de Kerberos (KCD)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  La delegación limitada de Kerberos (KCD) es un protocolo de autenticación que se puede configurar con la autenticación de Windows para delegar las credenciales de cliente de servicio a servicio en todo el entorno. KCD requiere una infraestructura adicional, por ejemplo, un controlador de dominio y una configuración adicional del entorno. KCD es un requisito en algunos escenarios que implican datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] con SharePoint 2016. En SharePoint 2016, Excel Services se ha trasladado de la granja de SharePoint a un nuevo servidor independiente, **Office Online Server**. Puesto que Office Online Server es independiente, se hace más necesaria una forma de delegar las credenciales de cliente en los escenarios típicos de dos saltos.  
  
## <a name="overview"></a>Información general  
 KCD permite a una cuenta suplantar a otra con el fin de proporcionar acceso a los recursos. La cuenta de suplantación corresponde a una cuenta de servicio asignada a una aplicación web o a la cuenta de equipo de un servidor web, mientras que la cuenta suplantada es una cuenta de usuario que requiere acceso a los recursos. KCD trabaja en el nivel de servicio, de modo que la cuenta de suplantación puede conceder acceso a unos servicios concretos de un servidor y denegárselo a la vez a otros servicios del mismo servidor o a servicios en otros servidores.  
  
 Las secciones de este tema abarcan escenarios comunes con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] donde se requiere KCD, así como una implementación de servidor de ejemplo y un resumen general de lo que se debe instalar y configurar. Vea la sección [Más información y contenido de la comunidad](#bkmk_moreinfo) para obtener vínculos a información más detallada sobre las tecnologías implicadas, como controladores de dominio y KCD.  
  
## <a name="scenario-1-workbook-as-data-source-wds"></a>Escenario 1: Libro como origen de datos (WDS).  
 ![Consulte 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "consulte 1") Office Online Server abre un libro de Excel y ![consulte 2](../../../analysis-services/instances/install-windows/media/ssas-callout2.png "consulte 2") detecta una conexión de datos a otro libro. Office Online Server envía una solicitud para el [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] servicio Redirector ![consulte 3](../../../analysis-services/instances/install-windows/media/ssas-callout3.png "consulte 3") para abrir el segundo libro y los datos ![consulte 4](../../../analysis-services/instances/install-windows/media/ssas-callout4.png "consulte 4 ").  
  
 En este escenario, las credenciales de usuario se deben delegar de Office Online Server al servicio de redirector [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] de SharePoint en SharePoint.  
  
 ![libro como origen de datos](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-wds.png "libro como origen de datos")  
  
## <a name="scenario-2-an-analysis-services-tabular-model-links-to-an-excel-workbook"></a>Escenario 2: Un vínculos de modelo Tabular de Analysis Services a un libro de Excel  
 Un modelo Tabular de Analysis Services ![consulte 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "consulte 1") vínculos a un libro de Excel que contiene un modelo de PowerPivot. En este escenario, cuando [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] carga el modelo tabular, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] detecta el vínculo al libro. Al procesar el modelo, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] envía una solicitud de consulta a SharePoint para cargar el libro. En este escenario, **no** es necesario delegar las credenciales de cliente de Analysis Services a SharePoint, pero una aplicación cliente puede sobrescribir la información del origen de datos en un enlace temporal. Si la solicitud de enlace temporal especifica que se debe suplantar al usuario actual, se deberán delegar las credenciales de usuario, lo que requiere configurar KCD entre [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y SharePoint.  
  
 ![office online server](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-oos.png "office online server")  
  
## <a name="example-deployment-of-kcd-with-office-online-server-and-analysis-services"></a>Ejemplo de implementación de KCD con Office Online Server y Analysis Services  
 En esta sección se describe una implementación de ejemplo con cuatro equipos. En las siguientes secciones se resumen los pasos clave de instalación y configuración para cada equipo. Antes de iniciar las implementaciones, se recomienda que los equipos estén actualizados con las aplicaciones de revisiones del sistema operativo. Además, el usuario debe conocer los nombres de los equipos porque son necesarios en algunos pasos de la configuración.  
  
-   Controlador de dominio  
  
-   Motor de base de datos de SQL Server y Analysis Services en modo PowerPivot. La instancia del motor de base de datos se utilizará para las bases de datos de contenido de SharePoint.  
  
-   SharePoint Server 2016  
  
-   Office Online Server  
  
 ![domain controller](../../../analysis-services/instances/install-windows/media/ssas-kcd-domainserver-icon.png "domain controller")  
  
### <a name="domain-controller"></a>Controlador de dominio  
 A continuación se muestra un resumen de lo que se debe instalar para el controlador de dominio (DC).  
  
-   **Rol:** Servicios de dominio de Active Directory. Para obtener información general, vea [Configuring Active Directory (AD DS) in Windows Server 2012](http://sharepointgeorge.com/2012/configuring-active-directory-ad-ds-in-windows-server-2012/)(Configuración de Active Directory (AD DS) en Windows Server 2012).  
  
-   **Rol:** DNS Server  
  
-   **Característica:** características de .NET Framework 3.5/.NET Framework 3.5.  
  
-   **Característica:** Herramientas de administración remota del servidor / herramientas de administración de roles  
  
-   Configure Active Directory para crear un nuevo bosque y unir los equipos al dominio. Antes de intentar agregar otros equipos al dominio privado, deberá configurar los DNS de los equipos cliente en la dirección IP del controlador de dominio. En la máquina del controlador de dominio, ejecute `ipconfig /all` para obtener las direcciones IPv4 e IPv6 para el paso siguiente.  
  
-   Se recomienda configurar las ambas direcciones IPv4 e IPv6. Puede hacerlo en el panel de control de Windows:  
  
    1.  Haga clic en **Centro de redes y recursos compartidos**.  
  
    2.  Haga clic en la conexión Ethernet.  
  
    3.  Haga clic en **Propiedades**.  
  
    4.  Haga clic en **Protocolo de Internet versión 6 (TCP/IPv6)**.  
  
    5.  Haga clic en **Propiedades**.  
  
    6.  Haga clic en **Usar las siguientes direcciones de servidor DNS**.  
  
    7.  Escriba la dirección IP mediante el comando "ipconfig".  
  
    8.  Haga clic en el botón **Avanzadas** , en la pestaña **DNS** y compruebe que los sufijos DNS sean correctos.  
  
    9. Haga clic en **Anexar estos sufijos DNS**.  
  
    10. Repita los pasos para la dirección IPv4.  
  
-   **Nota:** Puede unir equipos al dominio desde el Panel de control de Windows, en la configuración del sistema. Para obtener más información, vea [How To Join Windows Server 2012 to a Domain](http://social.technet.microsoft.com/wiki/contents/articles/20260.how-to-join-windows-server-2012-to-a-domain.aspx)(Cómo unir Windows Server 2012 a un dominio).  
  
 ![servidor de SSAS en modo powerpivot](../../../analysis-services/instances/install-windows/media/ssas-kcd-powerpivotserver-icon.png "servidor ssas en modo powerpivot")  
  
### <a name="2016-sql-server-database-engine-and-analysis-services-in-power-pivot-mode"></a>Motor de base de datos de SQL Server 2016 y Analysis Services en modo PowerPivot  
 A continuación se muestra un resumen de lo que se debe instalar en el equipo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 ![Tenga en cuenta](../../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "Nota") en el [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Asistente para la instalación, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en Power Pivot está instalado como parte del flujo de trabajo de selección de características.  
  
1.  Ejecute el Asistente para instalación de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] y, en la página de selección de características, haga clic en el motor de base de datos, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], y en las Herramientas de administración. En una configuración posterior del Asistente para instalación puede especificar el modo [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
2.  Para la configuración de instancia, configure una instancia con nombre de "POWERPIVOT".  
  
3.  En la página Configuración de Analysis Services, configure el servidor de Analysis Services para el modo **Power Pivot** y agregue el **nombre de equipo** de Office Online Server a la lista de administradores de servidores de Analysis Services. Para obtener más información, consulte [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
4.  Tenga en cuenta que el tipo de objeto "Equipo" no se incluye en la búsqueda de forma predeterminada. Haga clic en ![haga clic en los objetos para agregar la cuenta de equipo](../../../analysis-services/instances/install-windows/media/ss-objects-button.png "haga clic en los objetos para agregar la cuenta de equipo") para agregar el objeto de los equipos.  
  
     ![agregar cuentas de equipo como administradores de ssas](../../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "agregar cuentas de equipo como administradores de ssas")  
  
5.  Cree los nombres de entidad de seguridad de servicio (SPN) para la instancia de Analysis Services.  
  
     Comandos útiles de SPN:  
  
    -   Indicar el SPN de un nombre de cuenta específico que ejecuta el servicio en cuestión: `SetSPN -l <account-name>`  
  
    -   Establecer un SPN de un nombre de cuenta que ejecuta el servicio en cuestión: `SetSPN -a <SPN> <account-name>`  
  
    -   Eliminar un SPN de un nombre de cuenta específico que ejecuta el servicio en cuestión: `SetSPN -D <SPN> <account-name>`  
  
    -   Buscar SPN duplicados: `SetSPN -X`  
  
     El formato del SPN para la instancia de PowerPivot será el siguiente:  
  
    ```  
    MSSQLSvc.3/\<Fully Qualified Domain Name (FQDN)>:POWERPIVOT  
    MSSQLSvc.3/<NetBIOS Name>:POWERPIVOT  
    ```  
  
     Donde los nombres FQDN y NetBIOS son el nombre del equipo en el que reside la instancia. Estos SPN se colocarán en la cuenta de dominio que se utiliza para la cuenta de servicio.  Si utiliza el servicio de red, el sistema local o el identificador de servicio, deberá colocar el SPN en la cuenta de equipo de dominio.  Si utiliza una cuenta de usuario de dominio, deberá colocar el SPN en dicha cuenta.  
  
6.  Cree el SPN para el servicio SQL Browser en el equipo de Analysis Services.  
  
     [Más información](https://support.microsoft.com/en-us/kb/950599)  
  
7.  **Configure las opciones de la delegación restringida** en la cuenta de servicio de Analysis Services para cualquier origen externo desde el que realice las actualizaciones, como archivos de SQL Server o Excel. En la cuenta de servicio de Analysis Services, debe asegurarse de establecer las opciones siguientes.  
  
     **Nota:** Si no ve la ficha delegación para la cuenta, dentro de los usuarios de Active Directory y los equipos, es porque no hay ningún SPN en dicha cuenta.  Puede agregar un SPN falso para que aparezca como `my/spn`.  
  
     **Confiar en este usuario para la delegación solo a los servicios especificados** y **Usar cualquier protocolo de autenticación**.  
  
     Esto se conoce como delegación restringida y es necesaria porque el token de Windows se originará a partir de una Notificación del servicio de token de Windows (C2WTS), que requiere delegación restringida con transición de protocolo.  
  
     ![Analysis Services - la delegación restringida](../../../analysis-services/instances/install-windows/media/analysis-services-constrained-delegation.png "Analysis Services - la delegación restringida")  
  
     También deberá agregar los servicios para los que aplicará la delegación. Esto variará en función de su entorno.  
  
### <a name="office-online-server"></a>Office Online Server  
  
1.  Office Online Server  
  
2.  **Configure Office Online Server** para conectarse al servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Recuerde que la cuenta de equipo de Office Online Server debe ser un administrador en el servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Esto se trata en una sección anterior de este tema sobre la instalación del servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
    1.  En Office Online Server, abra una ventana de PowerShell con privilegios administrativos y ejecute el siguiente comando.  
  
    2.  `New-OfficeWebAppsExcelBIServer -ServerId <AS instance name>`  
  
    3.  Ejemplo: `New-OfficeWebAppsExcelBIServer -ServerId "MTGQLSERVER-13\POWERPIVOT"`  
  
3.  **Configure Active Directory** para permitir que la cuenta de equipo de Office Online Server pueda suplantar a usuarios para la cuenta de servicio de SharePoint. Por lo tanto, establezca la propiedad de delegación en principal ejecuta el grupo de aplicaciones para servicios Web de SharePoint, en Office Online Server: Los comandos de PowerShell en esta sección requieren los objetos de PowerShell de Active Directory (AD).  
  
    1.  Obtener la identidad de Active Directory de Office Online Server  
  
        ```  
        $computer1 = Get-ADComputer -Identity [ComputerName]  
        ```  
  
         Para buscar el nombre de esta entidad de seguridad, vaya a Administrador de tareas/Detalles/Nombre de usuario de w3wp.exe. Por ejemplo, "svcSharePoint"  
  
        ```  
        Set-ADUser svcSharePoint -PrincipalsAllowedToDelegateToAccount $computer1  
  
        ```  
  
    2.  Para comprobar que la propiedad se haya establecido correctamente, haga lo siguiente:  
  
    3.  ```  
        Get-ADUser svcSharePoint -Properties PrincipalsAllowedToDelegateToAccount  
        ```  
  
4.  **Configure las opciones de la delegación restringida** en la cuenta de Office Online Server para la instancia de Power Pivot de Analysis Services. Debe ser la cuenta del equipo en el que se ejecuta Office Online Server. En la cuenta de Office Online Service, debe asegurarse de establecer las opciones siguientes.  
  
     **Nota:** Si no ve la ficha delegación para la cuenta, dentro de los usuarios de Active Directory y los equipos, es porque no hay ningún SPN en dicha cuenta.  Puede agregar un SPN falso para que aparezca como `my/spn`.  
  
     **Confiar en este usuario para la delegación solo a los servicios especificados** y **Usar cualquier protocolo de autenticación**.  
  
     Esto se conoce como delegación restringida y es necesaria porque el token de Windows se originará a partir de una Notificación del servicio de token de Windows (C2WTS), que requiere delegación restringida con transición de protocolo.  A continuación, deberá permitir la delegación en los SPN de MSOLAPSvc.3 y MSOLAPDisco.3 creados anteriormente.  
  
5.  Configurar Notificaciones del servicio de token de Windows (C2WTS) **Esto es necesario para el escenario 1**. Para obtener más información, vea [Información general sobre Claims to Windows Token Service (c2WTS)](https://msdn.microsoft.com/library/ee517278.aspx).  
  
6.  **Configure las opciones de la delegación restringida** en la cuenta de servicio de C2WTS.  La configuración debe corresponderse con la establecida en el paso 4.  
  
 ![SharePoint server](../../../analysis-services/instances/install-windows/media/ssas-kcd-sharepointserver-icon.png "sharepoint server")  
  
### <a name="sharepoint-server-2016"></a>SharePoint Server 2016  
 A continuación se muestra un resumen de la instalación de SharePoint Server.  
  
1.  Ejecutar el instalador de requisitos previos de SharePoint  
  
2.  Ejecute la instalación de SharePoint y seleccione el rol de instalación **Granja de servidor único** .  
  
3.  Ejecute el complemento de PowerPivot para SharePoint (spPowerPivot16.msi). Para obtener más información, consulte [instalar o desinstalar el Power Pivot para SharePoint Add-in (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
4.  Ejecute el Asistente para configuración de PowerPivot. Vea [Herramientas de configuración de Power Pivot](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
5. Conecte SharePoint a Office Online Server. (Configure_xlwac_on_SPO.ps1)
  
6.  Configure los proveedores de autenticación de SharePoint para Kerberos. **Esto es necesario para el escenario 1**. Para obtener más información, vea [Planear la autenticación Kerberos en SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).  
  
##  <a name="bkmk_moreinfo"></a> Más información y contenido de la comunidad  
 [Kerberos para la administración de disponibilidad](http://blogs.technet.com/b/askds/archive/2008/03/06/kerberos-for-the-busy-admin.aspx)  
  
 [Descripción de Kerberos de dos saltos](http://blogs.technet.com/b/askds/archive/2008/06/13/understanding-kerberos-double-hop.aspx)  
  
 [Contenido relacionado con .NET y SharePoint](http://sbrickey.com/Tech/Blog/Post/Kerberos_Primer)  
  
 [Delegación limitada de Kerberos basada en recursos](http://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)  
  
 [CONCEPTOS BÁSICOS DE KERBEROS: vídeos](http://blog.martinlund.it/kerberos-primer/)  
  
 [Microsoft® Kerberos Configuration Manager para SQL Server®](http://www.microsoft.com/en-us/download/details.aspx?id=39046)  
  
  
