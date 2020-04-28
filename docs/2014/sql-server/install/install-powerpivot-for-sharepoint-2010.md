---
title: Instalación de PowerPivot para SharePoint 2010 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: eec38696-5e26-46fa-bc83-aa776f470ce8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b7d478761a1051114e0189c7fd11eddafcef086b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78172347"
---
# <a name="install-powerpivot-for-sharepoint-2010"></a>Instalar PowerPivot para SharePoint 2010
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] es una colección de servicios de nivel intermedio y back-end que proporcionan acceso a datos PowerPivot en una granja de SharePoint 2010. Si su organización usa la aplicación cliente, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel 2010, para crear libros que contienen datos analíticos, debe tener [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] para acceder a esos datos en un entorno de servidor. Este tema es una guía a través del proceso de instalación básico e incluye vínculos a temas adicionales para ayudarle a configurar PowerPivot.

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010|

 

 Para obtener instrucciones sobre cómo instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en el mismo servidor, vea [lista de comprobación de la implementación: Reporting Services, Power View y PowerPivot para SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md).

## <a name="prerequisites"></a>Prerrequisitos

1.  Debe ser administrador local para ejecutar el programa de instalación de SQL Server.

2.  Se requiere la edición Enterprise de Microsoft SharePoint Server 2010 para [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. También puede utilizar la edición Enterprise de evaluación.

3.  Debe instalarse SharePoint Server 2010 SP2. Sin él, no puede configurar la granja de servidores para usar las características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .

4.  El equipo debe estar unido a un dominio.

5.  Debe tener una cuenta de usuario de dominio para aprovisionar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. En una instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , la cuenta de servicio de Analysis Services debe ser una cuenta de usuario de dominio para poder administrarla desde Administración central. Deberá especificar la cuenta y las credenciales en la página de **Configuración del servidor** en los pasos que describe este documento.

6.  El nombre de instancia de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] debe estar disponible. No puede tener una instancia con nombre de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] existente en el equipo en el que está instalando PowerPivot para SharePoint.

7.  La instancia de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] no pueden formar parte de un clúster de conmutación por error de SQL Server. Use las características de gran disponibilidad del producto de SharePoint. Por ejemplo, Servicios de Excel administra el equilibrio de carga de PowerPivot para SharePoint Server. Para obtener más información, vea [administrar la configuración del modelo de datos de servicios de Excel (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx) (.https://technet.microsoft.com/library/jj219780.aspx)

8.  Si va a instalar [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] en una granja existente, debe tener una o más aplicaciones web de SharePoint que estén configuradas para la autenticación en modo clásico. El acceso a datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] solo funcionará si la aplicación web admite la autenticación en modo clásico. Para obtener más información acerca de los requisitos en modo clásico, vea [PowerPivot Authentication and Authorization](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization).

9. Revise los siguientes temas adicionales para conocer los requisitos del sistema y de las versiones:

    -   [Instrucciones para usar las características de SQL Server BI en una granja de servidores de SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)

##  <a name="step-1-install-powerpivot-for-sharepoint"></a><a name="InstallSQL"></a>Paso 1: instalar PowerPivot para SharePoint
 En este paso, ejecuta el programa de instalación de SQL Server para instalar [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. En un paso posterior, configurará el servidor como una tarea posterior a la instalación.

1.  Inserte el disco de instalación o abra la carpeta que contenga los archivos de instalación para SQL Server y haga doble clic en **setup.exe**.

2.  En el panel izquierdo, haga clic en **Instalación** .

3.  Haga clic en **Nueva instalación independiente de SQL Server o agregar características a una instalación existente**.

4.  En la página **Clave del producto** , especifique la edición Evaluation o escriba la clave del producto de una copia con licencia de la edición Enterprise.

     Haga clic en **Next**.

5.  Acepte los Términos del acuerdo de licencia de software de Microsoft y le agradeceríamos que activara los informes sobre errores y experiencia del cliente. Haga clic en **Next**.

6.  Actualice los archivos de instalación si le piden que lo haga.

7.  En la página **Reglas de instalación** , el programa de instalación identifica cualquier problema que pueda impedir la instalación. Revise la lista para determinar si el programa de instalación detectó los posibles problemas en el sistema.

    > [!NOTE]
    >  Como Firewall de Windows está habilitado, se le avisará de que debe abrir los puertos para habilitar el acceso remoto. Esta advertencia no suele ser aplicable a las instalaciones de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Las conexiones a los archivos de datos y servicios [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se realizan usando los puertos de SharePoint que ya están abiertos para la comunicación entre servicios de SharePoint.

     Haga clic en **Next**. Espere mientras los archivos de programa del programa de instalación de SQL Server se instalan en el servidor.

8.  En la página **Rol de instalación** , seleccione **SQL Server PowerPivot para SharePoint**.

9. Opcionalmente, puede agregar una instancia del motor de base de datos a la instalación. Podría hacer esto si está configurando una nueva granja y necesita un servidor de base de datos para ejecutar las bases de datos de contenido y configuración de la granja. Si agrega el Motor de base de datos, se instalará como una instancia con nombre de PowerPivot. Siempre que necesite especificar una conexión a esta instancia (por ejemplo, en el Asistente para configuración de granja de servidores si está usando ese Asistente para configurar la granja de servidores), escriba el nombre de la `servername` base de datos en este formato: <> \powerpivot.

     ![GMNI_SetupUI_FeatureRole](../../../2014/sql-server/install/media/gmni-setupui-featurerole.gif "GMNI_SetupUI_FeatureRole")

10. Haga clic en **Next**.

11. En la página **Selección de características** , se muestra una lista de solo lectura de las características que se instalarán, con carácter informativo. No puede agregar ni quitar elementos, que ya están seleccionados para este rol. Haga clic en **Next**.

12. En la página **Reglas de características** , haga clic en **Siguiente**. Se puede omitir esta página.

13. En la página **Configuración de instancia** , se muestra el nombre de instancia de solo lectura 'PowerPivot', con carácter informativo. Este nombre de instancia de **POWERPIVOT** es **necesario y no se puede modificar**. Con todo, puede escribir un identificador de instancia único para especificar un nombre de directorio descriptivo y claves del Registro. Haga clic en **Next**.

14. En la página **Configuración del servidor** , escriba la información de cuenta deseada.

     En el caso de SQL Server Analysis Services, debe especificar una cuenta de usuario de dominio. No especifique una cuenta integrada. Se requieren cuentas de dominio para administrar la cuenta de servicio de Analysis Services como una *cuenta administrada* en Administración central de SharePoint.

     ![Configurar SSAS Server](../../../2014/sql-server/install/media/ssas-powerpivotsetupsql2012sp1-serverconfiguration.gif "Configurar SSAS Server")

     Si ha agregado el Motor de base de datos de SQL Server y el Agente SQL Server, puede configurar los servicios para que se ejecuten en las cuentas de usuario de dominio o en la cuenta virtual predeterminada.

     Nunca use su propia cuenta de usuario de dominio para proporcionar ningún servicio. Si lo hace, concede al servidor los mismos permisos que tiene en los recursos de su red. Si un usuario malintencionado pone en peligro el servidor, ese usuario iniciará sesión con sus mismas credenciales de dominio y con su misma capacidad de descargar o usar los datos y aplicaciones.

15. Haga clic en **Next**.

16. Si va a instalar el Motor de base de datos, aparece la página Configuración del Motor de base de datos. En Configuración del motor de base de datos, haga clic en **Agregar usuario actual** para conceder permisos de administrador de cuenta de usuario en la instancia del motor de base de datos. Haga clic en **Agregar** para agregar cuentas adicionales. Haga clic en **Next**.

17. En la página **Configuración de Analysis Services** , haga clic en **Agregar usuario actual** para conceder permisos administrativos a la cuenta de usuario. Necesitará permiso administrativo para configurar el servidor una vez finalizada la instalación.

18. En la misma página, agregue la cuenta de usuario de Windows de cualquier usuario que necesite también permisos administrativos. Por ejemplo, todo usuario que desee conectarse a la instancia de [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] en SQL Server Management Studio para solucionar problemas de conexión a bases de datos o para obtener información de versión, debe tener permisos de administrador del sistema en el servidor. Agregue ahora la cuenta de usuario de todo usuario que podría tener que solucionar problemas o administrar el servidor.

19. Haga clic en **Next**.

20. Haga clic en **Siguiente** en todas las páginas que quedan hasta que llegue a la página Listo para instalar.

21. Haga clic en **Instalar**.

> [!TIP]
>  Si necesita solucionar problemas con la instalación de SQL Server, vea [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).

##  <a name="step-2-configure-the-server"></a><a name="bkmk_config"></a>Paso 2: configurar el servidor

> [!IMPORTANT]
>  SharePoint 2010 SP2 debe instalarse antes de configurar [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] o una granja de servidores de SharePoint que use un servidor de bases de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Si no ha instalado todavía el Service Pack, hágalo ahora antes de empezar la configuración del servidor.

 La instalación no se completa hasta que se configure el servidor. En esta versión, la configuración del servidor siempre se realiza como una tarea posterior a la instalación, mediante uno de los métodos siguientes: [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Herramienta de configuración, Administración central o PowerShell. Para continuar, elija uno de los métodos siguientes:

-   [Configurar o reparar 2010 PowerPivot para SharePoint &#40;herramienta de configuración de PowerPivot&#41;](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)

-   [Administración y configuración del servidor PowerPivot en Administración central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)

-   [Configuración de PowerPivot mediante Windows PowerShell](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)

 **Conectarse a la instancia del Motor de base de datos.** Cuando instaló [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], el programa de instalación de SQL Server le dio la opción de agregar una instancia del Motor de base de datos a la instalación. Es posible que haya agregado una instancia de Motor de base de datos a la instalación si está configurando una nueva granja y necesita un servidor de base de datos para ejecutar las bases de datos de contenido y configuración de la granja. Si agregó el Motor de base de datos, se instaló como una instancia con nombre de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Siempre que necesite especificar una conexión a esta instancia (por ejemplo, en el Asistente para configuración de granja de servidores si está usando ese Asistente para configurar la granja de servidores), Recuerde escribir el nombre de la base `servername` de datos en este formato: <> \powerpivot.

##  <a name="step-3-install-analysis-services-ole-db-providers-on-excel-services-application-servers"></a><a name="bkmk_redist"></a>Paso 3: instalar los proveedores de OLE DB de Analysis Services en los servidores de aplicaciones de Excel Services
 Se necesitan pasos de instalación adicionales si ejecuta Excel Calculation Services y [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en servidores de aplicaciones diferentes. En los servidores de aplicaciones que ejecutan Excel Calculation Services, instale la versión adecuada del proveedor OLE DB de Analysis Services (MSOLAP).

-   La versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de MSOLAP se incluye en el programa de instalación de SQL Server, por lo que solo es necesario instalar explícitamente la versión [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de MSOLAP si su servidor de aplicaciones no es un servidor de aplicaciones de PowerPivot.

    > [!NOTE]
    >  El servidor de aplicaciones de Excel Calculation Services también necesita una instancia del archivo **Microsoft.AnalysisServices.Xmla.dll** en el ensamblado global. Para instalar el archivo .dll en el servidor de aplicaciones, instale [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Seleccione la "herramientas de administración-completa" en la página **selección de características** del Asistente para la instalación de SQL Server.

-   Si desea que el servidor de aplicaciones admita libros anteriores de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , debe instalar la versión de SQL Server 2008 R2 de MSOLAP.

 Para obtener más información acerca de cómo instalar el proveedor, incluidos los pasos de comprobación, vea [Install the Analysis Services OLE DB Provider on SharePoint Servers](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).

##  <a name="step-4-verify-the-installation"></a><a name="bkmk_verify"></a>Paso 4: comprobar la instalación
 En este último paso, comprobará que SharePoint 2010 y [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] son totalmente funcionales. Para obtener instrucciones, vea [Verify a PowerPivot for SharePoint Installation](https://docs.microsoft.com/analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation).

## <a name="see-also"></a>Consulte también
 Lista de comprobación de implementación de [PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md) [: Reporting Services, Power View y PowerPivot para SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md) [lista de comprobación de la implementación: escalado horizontal agregando servidores de PowerPivot a una](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md) [lista de comprobación de implementación de granja de servidores de 2010 SharePoint: instalación en varios servidores de PowerPivot para SharePoint 2010](../../../2014/sql-server/install/deployment-checklist-multiserver-installation-powerpivot-sharepoint-2010.md)


