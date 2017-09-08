---
title: Instalar Analysis Services en modo PowerPivot | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d3310562-82c1-454f-9c48-33a241749238
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 035348a23627db2346d319c69030e74e128e744b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="install-analysis-services-in-power-pivot-mode"></a>Instalación de Analysis Services en el modo PowerPivot
  Los procedimientos de este tema explican cómo realizar una instalación en un solo servidor de un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en el modo [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para realizar una implementación de SharePoint. Los pasos incluyen la ejecución del Asistente para la instalación de SQL Server, así como tareas de configuración que usan Administración central de SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]** SharePoint 2016 &#124; SharePoint 2013|  
  
 **En este tema:**  
  
 [Información previa](#bkmk_background)  
  
 [Requisitos previos](#bkmk_prereq)  
  
 [Paso 1: desinstalación de PowerPivot para SharePoint](#InstallSQL)  
  
 [Paso 2: configurar la integración de SharePoint básica de Analysis Services](#bkmk_config)  
  
 [Paso 3: comprobar la integración](#bkmk_verify)  
  
 [Configurar Firewall de Windows para permitir el acceso a Analysis Services](#bkmk_firewall)  
  
 [Actualizar libros y actualización de datos programada](#bkmk_upgrade_workbook)  
  
 [Más allá de la instalación en un solo servidor: PowerPivot para Microsoft SharePoint](#bkmk_multiple_servers)  
  
##  <a name="bkmk_background"></a> Información previa  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint es una colección de servicios de nivel intermedio y back-end que proporcionan acceso a datos de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en una granja de SharePoint 2016 o 2013.  
  
-   **Servicios back-end** : si usa [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel con el fin de crear libros que contienen datos analíticos, debe tener [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint para obtener acceso a esos datos en un entorno de servidor. Puede ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en un equipo que tenga instalado SharePoint Server, o bien en un equipo diferente que no tenga ningún software de SharePoint. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no tiene ninguna dependencia en SharePoint.  
  
     **Nota** : en este tema se describe la instalación del servidor y los servicios back-end de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
-   **Nivel intermedio:** mejoras en las experiencias de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en SharePoint, incluidas la galería de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , la programación de actualización de datos, el panel de administración y proveedores de datos. Para obtener información acerca de la instalación y la configuración de nivel intermedio, vea lo siguiente:  
  
    -   [Instalar o desinstalar el PowerPivot para SharePoint complemento (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
    -   [Instalar o desinstalar el complemento PowerPivot para SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
    -   [Configuración de PowerPivot e implementación de soluciones &#40;SharePoint 2016&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2016.md)  
  
    -   [Configuración de PowerPivot e implementación de soluciones &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
##  <a name="bkmk_prereq"></a> Requisitos previos  
  
1.  Debe ser administrador local para ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
2.  Se requiere SharePoint Server Enterprise Edition en [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint. También puede utilizar la edición Enterprise de evaluación.  
  
3.  El equipo debe estar unido a un dominio en el mismo bosque de Active Directory que Office Online Server (SharePoint 2016) o Excel Services (SharePoint 2013).  
  
4.  El nombre de instancia de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] debe estar disponible. No puede tener una instancia con nombre de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]en el equipo en el que está instalando Analysis Services en el modo de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     **Nota:** El nombre de la instancia debe ser POWERPIVOT.  
  
5.  Revise [Requisitos de hardware y software para el servidor de Analysis Services en modo de SharePoint](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f).  
  
6.  Examine las Notas de la versión de [SQL Server 2016 Release Notes](../../../sql-server/sql-server-2016-release-notes.md).  
  
###  <a name="bkmk_sqleditions"></a> Requisitos de edición de SQL Server  
 No todas las características de Business Intelligence están disponibles en todas las ediciones de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Para obtener más información, consulte [características de Analysis Services compatibles con las ediciones de SQL Server 2016](../../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) y [ediciones y componentes de SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
##  <a name="InstallSQL"></a> Paso 1: desinstalación de PowerPivot para SharePoint  
 En este paso, ejecutará el programa de instalación de SQL Server para instalar un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . En un paso posterior, configurará Excel Services para usar este servidor para los modelos de datos de libro.  
  
1.  Ejecute el Asistente para la instalación de SQL Server (Setup.exe).  
  
2.  Seleccione la opción **Instalación** del panel izquierdo.  
  
3.  Seleccione **Nueva instalación independiente de SQL Server o agregar características a una instalación existente**.  
  
4.  Si ve la página **Clave del producto** , especifique la edición de evaluación o escriba la clave del producto de una copia con licencia de la edición Enterprise. Seleccione **Siguiente**. Para obtener más información acerca de las ediciones, vea [Editions and Components of SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
5.  Revise y acepte los Términos de licencia del software de Microsoft y, después, seleccione **Siguiente**.  
  
6.  Si ve la página **Reglas globales** , examine la información de reglas que muestra el Asistente para la instalación.  
  
7.  En la página **Microsoft Update** , se recomienda usar Microsoft Update para comprobar si hay actualizaciones; después, seleccione **Siguiente**.  
  
8.  La página **Instalar archivos de configuración** se ejecuta durante varios minutos. Revise las advertencias de reglas o las reglas con errores y, después, seleccione **Siguiente**.  
  
9. Si vuelve a ver **Reglas auxiliares del programa de instalación**, revise las advertencias y seleccione **Siguiente**.  
  
     **Nota** : como Firewall de Windows está habilitado, verá una advertencia para que abra los puertos para habilitar el acceso remoto.  
  
10. En la página **Rol de instalación** , seleccione **Instalación de características de SQL Server**.  
  
     Seleccione **Siguiente**.  
  
11. En la página Selección de características, haga clic en **Analysis Services**. Esta opción le permite instalar cualquiera de los tres modos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Seleccionará el modo en un paso posterior. Seleccione **Siguiente**.  
  
12. En la página **Configuración de instancia** , seleccione **Instancia con nombre** y escriba **POWERPIVOT** en el nombre de la instancia. Haga clic en **Siguiente**.  
  
     ![El programa de instalación SQL - página de aterrizaje de configuración de instancia](../../../analysis-services/instances/install-windows/media/sql2016-pp-instance-config-landing-page.png "el programa de instalación SQL - página de aterrizaje de configuración de instancia")  
  
13. En la página **Configuración del servidor** , configure todos los servicios para el **Tipo de inicio**Automático. Especifique la cuenta de dominio y la contraseña que quiera para **SQL Server Analysis Services**, **(1)** en el diagrama siguiente.  
  
    -   Para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], puede usar una cuenta de **usuario de dominio** o la cuenta **NetworkService** . No use las cuentas LocalSystem o LocalService.  
  
    -   Si ha agregado el Motor de base de datos de SQL Server y el Agente SQL Server, puede configurar los servicios para que se ejecuten en las cuentas de usuario de dominio o en la cuenta virtual predeterminada.  
  
    -   Nunca aprovisione cuentas de servicio con su propia cuenta de usuario de dominio. Si lo hace, concede al servidor los mismos permisos que tiene en los recursos de su red. Si un usuario malintencionado pone en peligro el servidor, ese usuario iniciará sesión con sus credenciales de dominio. El usuario tiene permisos para descargar o usar los mismos datos y aplicaciones que usted.  
  
     Seleccione **Siguiente**.  
  
     ![El programa de instalación SQL - página de aterrizaje de configuración del servidor](../../../analysis-services/instances/install-windows/media/sql2016-pp-server-config-landing-page.png "el programa de instalación de SQL - página de aterrizaje de configuración del servidor")  
  
14. Si va a instalar el [!INCLUDE[ssDE](../../../includes/ssde-md.md)], aparecerá la página **Configuración del Motor de base de datos** . En la configuración de [!INCLUDE[ssDE](../../../includes/ssde-md.md)] , haga clic en **Agregar usuario actual** para conceder permisos de administrador a la cuenta de usuario en la instancia del motor de base de datos.  
  
     Seleccione **Siguiente**.  
  
15. En la página **Configuración de Analysis Services** , seleccione la opción **Modo PowerPivot** en **Modo de servidor**  
  
     ![El programa de instalación SQL - página de aterrizaje de configuración de Analysis Services](../../../analysis-services/instances/install-windows/media/sql2016-pp-as-config-landing-page.png "el programa de instalación SQL - página de aterrizaje de configuración de Analysis Services")  
  
16. En la página **Configuración de Analysis Services** , haga clic en **Agregar usuario actual** para conceder permisos administrativos a las cuentas de usuario. Necesitará permiso administrativo para configurar el servidor una vez finalizada la instalación.  
  
    -   En la misma página, agregue la cuenta de usuario de Windows de cualquier usuario que necesite también permisos administrativos. Por ejemplo, todo usuario que desee conectarse a la instancia de [!INCLUDE[ssGeminiSrv](../../../includes/ssgeminisrv-md.md)] en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] para solucionar problemas de conexión a bases de datos debe tener permisos de administrador del sistema. Agregue ahora la cuenta de usuario de todo usuario que podría tener que solucionar problemas o administrar el servidor.  
  
    -   > [!NOTE]  
        >  Todas las aplicaciones de servicio que necesiten acceso a la instancia del servidor de Analysis Services deben tener permisos administrativos de Analysis Services. Por ejemplo, agregue las cuentas de servicio para Excel Services, Power View y PerformancePoint Services. Además, agregue la cuenta de la granja de servidores de SharePoint, que se usa como la identidad de la aplicación web que hospeda Administración central.  
  
     Seleccione **Siguiente**.  
  
17. En la página **Informes de errores** , seleccione **Siguiente**.  
  
18. En la página **Preparado para instalar** , seleccione **Instalar**.  
  
19. Si ve el cuadro de diálogo **Se requiere reiniciar el equipo**, seleccione **Aceptar**.  
  
20. Cuando la instalación se haya completado, seleccione **Cerrar**.  
  
21. Reinicie el equipo.  
  
22. Si tiene un firewall en el entorno, vea el tema de los Libros en pantalla de SQL Server [Configure the Windows Firewall to Allow Analysis Services Access](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
### <a name="verify-the-sql-server-installation"></a>Comprobar la instalación de SQL Server  
 Compruebe que se está ejecutando el servicio Analysis Services.  
  
1.  En Microsoft Windows, haga clic en **Iniciar**, seleccione **Todos los programas**y, después, el grupo **Microsoft SQL Server 2016** .  
  
2.  Seleccione **SQL Server Management Studio**.  
  
3.  Conéctese a la instancia de Analysis Services, por ejemplo, **[nombre de su servidor]\POWERPIVOT**. Si puede conectarse a la instancia, ha comprobado que el servicio se está ejecutando.  
  
##  <a name="bkmk_config"></a> Paso 2: configurar la integración de SharePoint básica de Analysis Services  
 En los pasos siguientes se describen los cambios de configuración necesarios para poder interactuar con modelos de datos avanzados de Excel en una biblioteca de documentos de SharePoint. Complete estos pasos después de instalar SharePoint y SQL Server Analysis Services.  
  
### <a name="sharepoint-2016"></a>SharePoint 2016  
 Excel Services se ha quitado de SharePoint 2016 y, en su lugar, se utiliza Office Online Server para hospedar Excel.  
  
#### <a name="grant-office-online-server-machine-account-administration-rights-on-analysis-services"></a>Concesión de derechos de administración de cuentas de equipo en Analysis Services  
 No hay que completar esta sección si durante la instalación de Analysis Services agregó la cuenta de equipo de Office Online Server como administrador de Analysis Services.  
  
1.  En el servidor de Analysis Services, inicie SQL Server Management Studio y conéctese a la instancia de Analysis; por ejemplo, `[MyServer]\POWERPIVOT`.  
  
2.  En el Explorador de objetos, haga clic con el botón derecho en el nombre de la instancia y, después, seleccione **Propiedades**.  
  
     ![Ver las propiedades de un servidor de SSAS](../../../analysis-services/instances/install-windows/media/as-ssms-proeprties.gif "ver las propiedades de un servidor de SSAS")  
  
3.  En el panel izquierdo, seleccione **Seguridad**. Agregue la cuenta de equipo instalada en Office Online Server.  
  
     ![Configuración de seguridad de un servidor de SSAS](../../../analysis-services/instances/install-windows/media/as-ssms-security.gif "configuración de seguridad de un servidor de SSAS")  
  
#### <a name="register-analysis-services-server-with-office-online-server"></a>Registro del servidor de Analysis Services en Office Online Server  
 Deberá realizar estos pasos en Office Online Server.  
  
-   Abra una ventana de comandos de PowerShell como administrador.  
  
-   Cargue el módulo de PowerShell `OfficeWebApps` .  
  
     `Import-Module OfficeWebApps`  
  
-   Agregue el servidor de Analysis Services, por ejemplo, `[MyServer]\POWERPIVOT`.  
  
     `New-OfficeWebAppsExcelBIServer -ServerId [MyServer]\POWERPIVOT]`  
  
### <a name="sharepoint-2013"></a>SharePoint 2013  
  
#### <a name="grant-excel-services-server-administration-rights-on-analysis-services"></a>Conceder derechos de administración de servidor de Excel Services en Analysis Services  
 No es necesario completar esta sección si durante la instalación de Analysis Services agregó la cuenta de servicio Aplicación de Excel Services como administrador de Analysis Services.  
  
1.  En el servidor de Analysis Services, inicie SQL Server Management Studio y conéctese a la instancia de Analysis; por ejemplo, `[MyServer]\POWERPIVOT`.  
  
2.  En el Explorador de objetos, haga clic con el botón derecho en el nombre de la instancia y, después, seleccione **Propiedades**.  
  
     ![Ver las propiedades de un servidor de SSAS](../../../analysis-services/instances/install-windows/media/as-ssms-proeprties.gif "ver las propiedades de un servidor de SSAS")  
  
3.  En el panel izquierdo, seleccione **Seguridad**. Agregue el inicio de sesión de dominio que configuró para la aplicación de Excel Services en el paso 1.  
  
     ![Configuración de seguridad de un servidor de SSAS](../../../analysis-services/instances/install-windows/media/as-ssms-security.gif "configuración de seguridad de un servidor de SSAS")  
  
#### <a name="configure-excel-services-for-analysis-services-integration"></a>Configurar Excel Services para la integración de Analysis Services  
  
1.  En Administración central de SharePoint, en el grupo Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en el nombre de la aplicación de servicio; el nombre predeterminado es **Aplicación de Excel Services**.  
  
3.  En la página **Administrar la aplicación de Excel Services**, haga clic en **Configuración del modelo de datos**.  
  
4.  Haga clic en **Agregar servidor**.  
  
5.  En **Nombre del servidor**, escriba el nombre del servidor de Analysis Services y el de la instancia de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Por ejemplo, `MyServer\POWERPIVOT`. El nombre de la instancia de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] es obligatorio.  
  
     Escriba una descripción.  
  
6.  Haga clic en **Aceptar**.  
  
7.  Los cambios surtirán efecto en unos minutos; o bien, puede **Detener** e **Iniciar** el servicio **Excel Calculation Services**. Para  
  
     Otra opción es abrir un símbolo del sistema con privilegios de administrador y escribir `iisreset /noforce`.  
  
     Puede comprobar si Excel Services reconoce el servidor examinando las entradas del registro de ULS. Verá entradas similares a la siguiente:  
  
    ```  
    Excel Services Application            Data Model        27           Medium                Check Administrator Access ([ServerName]\POWERPIVOT): Pass.        f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Server Version ([ServerName]\POWERPIVOT): Pass (11.0.2809.24 >= 11.0.2800.0).         f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Deployment Mode ([ServerName]\POWERPIVOT): Pass.            f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
  
    ```  
  
##  <a name="bkmk_verify"></a> Paso 3: comprobar la integración  
 Los pasos siguientes le guían por la creación y carga de un nuevo libro para comprobar la integración de Analysis Services. Necesitará una base de datos de SQL Server para completar los pasos.  
  
1.  **Nota** : si ya tiene un libro avanzado con segmentaciones de datos o filtros, puede cargarlo en una biblioteca de documentos de SharePoint y comprobar que puede interactuar con las segmentaciones de datos y los filtros desde la vista de biblioteca de documentos.  
  
2.  Inicie un nuevo libro en Excel.  
  
3.  En la pestaña Datos, seleccione **De otros orígenes** en la cinta de opciones de **Obtener datos externos**.  
  
4.  Seleccione **De SQL Server**.  
  
5.  En el **Asistente para la conexión de datos**, escriba el nombre de la instancia de SQL Server que tiene la base de datos que desea usar.  
  
6.  En Credenciales de inicio de sesión, compruebe que se ha seleccionado **Usar autenticación de Windows** y seleccione **Siguiente**.  
  
7.  Seleccione la base de datos que desea usar.  
  
8.  Compruebe que la casilla **Conectar con una tabla específica** está activada.  
  
9. Active la casilla **Habilitar la selección de varias tablas y agregar tablas al modelo de datos de Excel** .  
  
10. Seleccione las tablas que desea importar.  
  
11. Active la casilla **Importar relaciones entre tablas seleccionadas**y, después, haga clic en **Siguiente**. La importación de varias tablas de una base de datos relacional le permite trabajar con tablas que ya están relacionadas. Ahorra pasos porque no tiene que crear las relaciones manualmente.  
  
12. En la página **Guardar archivo de conexión de datos y finalizar** del asistente, escriba un nombre para la conexión y seleccione **Finalizar**.  
  
13. Aparecerá el cuadro de diálogo **Importar datos** . Elija **Informe de tabla dinámica**y, después, haga clic en **Aceptar**.  
  
14. Aparecerá en el libro una lista de campos de tabla dinámica.   
    En la lista de campos, seleccione la pestaña **Todos** .  
  
15. Agregue campos a las áreas Fila, Columnas y Valor de la lista de campos.  
  
16. Agregue una segmentación de datos o un filtro a la tabla dinámica. **No omita este paso**. Una segmentación de datos o un filtro es el elemento que le ayudará a comprobar la instalación de Analysis Services.  
  
17. Guarde el libro en una biblioteca de documentos de la granja de SharePoint. También puede guardarlo en un recurso compartido de archivos y cargarlo después en la biblioteca de documentos de SharePoint.  
  
18. Haga clic en el nombre del libro para verlo en SharePoint y, luego, en la segmentación de datos, o bien cambie el filtro que agregó anteriormente. Si se actualizan los datos, sabrá que Analysis Services está instalado y disponible en Excel. Si abre el libro en Excel usará una copia almacenada en memoria caché y no el servidor de Analysis Services.  
  
##  <a name="bkmk_firewall"></a> Configurar Firewall de Windows para permitir el acceso a Analysis Services  
 Use la información del tema [Configurar Firewall de Windows para permitir el acceso a Analysis Services](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) para determinar si necesita desbloquear puertos de un firewall para permitir el acceso a Analysis Services o a [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint. Puede seguir los pasos proporcionados en el tema para configurar las opciones de los puertos y del firewall. En la práctica, debe realizar estos pasos juntos para permitir el acceso al servidor de Analysis Services.  
  
##  <a name="bkmk_upgrade_workbook"></a> Actualizar libros y actualización de datos programada  
 Los pasos necesarios para actualizar libros creados en versiones anteriores de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] dependen de la versión de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] que creó el libro. Para obtener más información, vea [Actualizar libros y actualización de datos programada &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
##  <a name="bkmk_multiple_servers"></a> Más allá de la instalación en un solo servidor: PowerPivot para Microsoft SharePoint  
 **Front-end web (WFE)** o **Nivel intermedio:**para usar un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en el modo de SharePoint en una granja de servidores de SharePoint mayor e instalar características adicionales de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en la granja, ejecute el paquete **spPowerPivot16.msi (SharePoint 2016) o spPowerPivot.msi (SharePoint 2013)** en todos los servidores de SharePoint. El archivo spPowerPivot16.msi o spPowerPivot.msi instala los proveedores de datos necesarios y la herramienta de configuración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2016 o 2013.  
  
 Para obtener información acerca de la instalación y la configuración de nivel intermedio, vea lo siguiente:  
  
-   [Instalar o desinstalar el complemento PowerPivot para SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   [Instalar o desinstalar el complemento PowerPivot para SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   Para descargar el archivo .msi, consulte [Microsoft SQL Server 2016 PowerPivot para Microsoft SharePoint 2016](http://go.microsoft.com/fwlink/?LinkID=324854).  
  
-   [Configuración de PowerPivot e implementación de soluciones &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
 **Redundancia y carga del servidor** : la instalación de un segundo servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , o de más servidores, en el modo de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] proporcionará redundancia de la funcionalidad de servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Los servidores adicionales también repartirán la carga entre distintos servidores. Para obtener más información, vea:  
  
-   [Configuración de Analysis Services para el procesamiento de modelos de datos en Excel Services (SharePoint 2013)](http://technet.microsoft.com/library/jj614437\(v=office.15\)) (http://technet.microsoft.com/library/jj614437(v=office.15)).  
  
-   [Administrar la configuración del modelo de datos de Excel Services (SharePoint 2013)](http://technet.microsoft.com/library/jj219780\(v=office.15\)) (http://technet.microsoft.com/library/jj219780(v=office.15)).  
  
 ![Configuración de SharePoint](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "configuración de SharePoint") [enviar comentarios e información de contacto a través de Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Vea también  
 [Migrar Power Pivot a SharePoint 2013](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [Instalar o desinstalar el complemento PowerPivot para SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [Actualizar libros y actualización de datos programada &#40; SharePoint 2013 &#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
