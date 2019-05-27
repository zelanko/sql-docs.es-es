---
title: PowerPivot para SharePoint 2013 Installation | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d3310562-82c1-454f-9c48-33a241749238
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f89ba75ab8d13960b3c86193862f5061f6727bb6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079937"
---
# <a name="powerpivot-for-sharepoint-2013-installation"></a>PowerPivot for SharePoint 2013 Installation
  Los procedimientos de este tema le guían por la instalación en un solo servidor de un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de implementación de SharePoint. Los pasos incluyen la ejecución del Asistente para la instalación de SQL Server, así como tareas de configuración que usan Administración central de SharePoint 2013.  
  
 **[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 201  
  
 **En este tema:**  
  
 [Información previa](#bkmk_background)  
  
 [Requisitos previos](#bkmk_prereq)  
  
 [Paso 1: Instalar PowerPivot para SharePoint](#InstallSQL)  
  
 [Paso 2: Configurar la integración de SharePoint básica de Analysis Services](#bkmk_config)  
  
 [Paso 3: Comprobar la integración](#bkmk_verify)  
  
 [Configurar Firewall de Windows para permitir el acceso a Analysis Services](#bkmk_firewall)  
  
 [Actualizar libros y actualización de datos programada](#bkmk_upgrade_workbook)  
  
 [Más allá de la instalación de servidor único, PowerPivot para Microsoft SharePoint](#bkmk_multiple_servers)  
  
##  <a name="bkmk_background"></a> Información previa  
 PowerPivot para SharePoint es una colección de servicios de nivel intermedio y back-end que proporcionan acceso a datos PowerPivot en una granja de SharePoint 2013.  
  
-   **Servicios de back-end:** Si usa PowerPivot para Excel para crear libros que contienen datos analíticos, debe tener PowerPivot para SharePoint tener acceso a esos datos en un entorno de servidor. Puede ejecutar el programa de instalación de SQL Server en un equipo que tenga instalado SharePoint Server 2013 o en un equipo diferente que no tenga ningún software de SharePoint. Analysis Services no tiene ninguna dependencia en SharePoint.  
  
     **Nota:** En este tema se describe la instalación de la [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] servidor y los servicios de back-end.  
  
-   **Nivel intermedio:** Mejoras en las experiencias de PowerPivot en SharePoint, incluidas la Galería de PowerPivot, programar la actualización de datos, panel de administración y proveedores de datos. Para obtener información acerca de la instalación y la configuración de nivel intermedio, vea lo siguiente:  
  
    -   [Instalar o desinstalar PowerPivot para SharePoint complemento &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
    -   [Configurar PowerPivot e implementar soluciones &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
##  <a name="bkmk_prereq"></a> Requisitos previos  
  
1.  Debe ser administrador local para ejecutar el programa de instalación de SQL Server.  
  
2.  Se requiere SharePoint Server 2013 para PowerPivot para SharePoint. También puede utilizar la edición Enterprise de evaluación.  
  
3.  Se debe unir el equipo a un dominio del mismo bosque de Active Directory que Excel Services.  
  
4.  El nombre de instancia de PowerPivot debe estar disponible. No puede tener una instancia con nombre de PowerPivot existente en el equipo en el que está instalando Analysis Services en modo de SharePoint.  
  
5.  Revisión [requisitos de Hardware y Software para el servidor de Analysis Services en modo de SharePoint &#40;SQL Server 2014&#41;](../../../sql-server/install/hardware-software-requirements-analysis-services-server-sharepoint-mode.md).  
  
6.  Revise las notas de la versión en [SQL Server 2012 Service Pack 1 Release Notes](https://go.microsoft.com/fwlink/?LinkID=248389) (https://go.microsoft.com/fwlink/?LinkID=248389).  
  
###  <a name="bkmk_sqleditions"></a> Requisitos de edición de SQL Server  
 No todas las características de Business Intelligence están disponibles en todas las ediciones de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Para obtener más información, consulte [características compatibles con las ediciones de SQL Server 2012 (https://go.microsoft.com/fwlink/?linkid=232473) ](https://go.microsoft.com/fwlink/?linkid=232473) y [ediciones y componentes de SQL Server 2014](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
 Las notas de la versión actual pueden encontrarse en [SQL Server 2012 SP1 Release Notes](ttp://go.microsoft.com/fwlink/?LinkID=248389) (https://go.microsoft.com/fwlink/?LinkID=248389).  
  
 [Notas de la versión de Microsoft SQL Server 2012 (https://go.microsoft.com/fwlink/?LinkId=236893)](https://go.microsoft.com/fwlink/?LinkId=236893).  
  
##  <a name="InstallSQL"></a> Paso 1: Instalar PowerPivot para SharePoint  
 En este paso, ejecutará el programa de instalación de SQL Server para instalar un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de SharePoint. En un paso posterior, configurará Excel Services para usar este servidor para los modelos de datos de libro.  
  
1.  Ejecute el Asistente para la instalación de SQL Server (Setup.exe).  
  
2.  Haga clic en **Instalación** en el panel izquierdo.  
  
3.  Haga clic en **Nueva instalación independiente de SQL Server o agregar características a una instalación existente**.  
  
4.  Si ve la página **Clave del producto** , especifique la edición de evaluación o escriba la clave del producto de una copia con licencia de la edición Enterprise. Haga clic en **Siguiente**. Para obtener más información acerca de las ediciones, vea [Editions and Components of SQL Server 2014](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
5.  Revise y acepte los Términos de licencia del software de Microsoft y, a continuación, haga clic en **Siguiente**.  
  
6.  Si ve la página **Reglas globales** , examine la información de reglas que muestra el Asistente para la instalación.  
  
7.  En la página **Microsoft Update** , se recomienda usar Microsoft Update para comprobar si hay actualizaciones y, a continuación, haga clic en **Siguiente**.  
  
8.  La página **Instalar archivos de configuración** se ejecuta durante varios minutos. Revise las advertencias de reglas o las reglas con errores y, a continuación, haga clic en **Siguiente**.  
  
9. Si vuelve a ver **Reglas auxiliares del programa de instalación**, revise las advertencias y haga clic en **Siguiente**.  
  
     **Nota:** Dado que Firewall de Windows está habilitado, verá una advertencia para abrir los puertos para habilitar el acceso remoto.  
  
10. En la página **Rol de instalación** , seleccione **SQL Server PowerPivot para SharePoint**. Esta opción instala Analysis Services en modo de SharePoint.  
  
     Opcionalmente, puede agregar una instancia del motor de base de datos a la instalación. Puede agregar el motor de base de datos al configurar una granja de servidores y necesita un servidor de base de datos para ejecutar las bases de datos de contenido y configuración de la granja de servidores. Esta opción también instala [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
     Si agrega el Motor de base de datos, se instala como una instancia con nombre de **PowerPivot** . Siempre que especifique una conexión a esta instancia, escriba el nombre de la base de datos en este formato: [`servername`]\PowerPivot.  
  
     Haga clic en **Siguiente**.  
  
     ![Rol de instalación](../../../sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "rol de instalación")  
  
11. En Selección de características, se muestra una lista de solo lectura de las características con carácter informativo. No puede agregar ni quitar elementos que ya están seleccionados para este rol. Haga clic en **Siguiente**.  
  
12. En la página **Configuración de instancia** , se muestra el nombre de instancia de solo lectura 'PowerPivot', con carácter informativo. Este nombre de instancia es necesario y no se puede modificar. Con todo, puede escribir un identificador de instancia único para especificar un nombre de directorio descriptivo y claves del Registro. Haga clic en **Siguiente**.  
  
13. En la página **Configuración del servidor** , configure todos los servicios para el **Tipo de inicio**Automático. Especifique la cuenta de dominio y la contraseña que quiera para **SQL Server Analysis Services**, **(1)** en el diagrama siguiente.  
  
    -   Para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], puede usar una cuenta de **usuario de dominio** o la cuenta **NetworkService** . No use las cuentas LocalSystem o LocalService.  
  
    -   Si ha agregado el Motor de base de datos de SQL Server y el Agente SQL Server, puede configurar los servicios para que se ejecuten en las cuentas de usuario de dominio o en la cuenta virtual predeterminada.  
  
    -   Nunca aprovisione cuentas de servicio con su propia cuenta de usuario de dominio. Si lo hace, concede al servidor los mismos permisos que tiene en los recursos de su red. Si un usuario malintencionado pone en peligro el servidor, ese usuario iniciará sesión con sus credenciales de dominio. El usuario tiene permisos para descargar o usar los mismos datos y aplicaciones que usted.  
  
     Haga clic en **Siguiente**.  
  
     ![Configuración del servidor SSAS](../../../sql-server/install/media/ssas-powerpivotsetupsql2012sp1-serverconfiguration.gif "configurar SSAS Server")  
  
14. Si va a instalar el [!INCLUDE[ssDE](../../../includes/ssde-md.md)], aparecerá la página **Configuración del Motor de base de datos** . En Configuración del [!INCLUDE[ssDE](../../../includes/ssde-md.md)] , haga clic en **Agregar usuario actual** para conceder permisos de administrador de cuenta de usuario en la instancia del motor de base de datos.  
  
     Haga clic en **Siguiente**.  
  
15. En la página **Configuración de Analysis Services** , haga clic en **Agregar usuario actual** para conceder permisos administrativos a la cuenta de usuario. Necesitará permiso administrativo para configurar el servidor una vez finalizada la instalación.  
  
    -   En la misma página, agregue la cuenta de usuario de Windows de cualquier usuario que necesite también permisos administrativos. Por ejemplo, todo usuario que desee conectarse a la instancia de [!INCLUDE[ssGeminiSrv](../../../includes/ssgeminisrv-md.md)] en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] para solucionar problemas de conexión a bases de datos debe tener permisos de administrador del sistema. Agregue ahora la cuenta de usuario de todo usuario que podría tener que solucionar problemas o administrar el servidor.  
  
    -   > [!NOTE]  
        >  Todas las aplicaciones de servicio que necesiten acceso a la instancia del servidor de Analysis Services deben tener permisos administrativos de Analysis Services. Por ejemplo, agregue las cuentas de servicio para Excel Services, Power View y PerformancePoint Services. Además, agregue la cuenta de la granja de servidores de SharePoint, que se usa como la identidad de la aplicación web que hospeda Administración central.  
  
     Haga clic en **Siguiente**.  
  
16. En la página **Informes de errores** , haga clic en **Siguiente**.  
  
17. En la página **Preparado para instalar** , haga clic en **Instalar**.  
  
18. Si ve el cuadro de diálogo **Se requiere reiniciar el equipo**, haga clic en **Aceptar**.  
  
19. Cuando la instalación se haya completado, haga clic en **Cerrar**.  
  
20. Reinicie el equipo.  
  
21. Si tiene un firewall en el entorno, vea el tema de los Libros en pantalla de SQL Server [Configure the Windows Firewall to Allow Analysis Services Access](../configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
### <a name="verify-the-sql-server-installation"></a>Comprobar la instalación de SQL Server  
 Compruebe que se está ejecutando el servicio Analysis Services.  
  
1.  En Microsoft Windows, haga clic en **Iniciar**, haga clic en **Todos los programas**y, después, haga clic en el grupo **Microsoft SQL Server 2012** .  
  
2.  Haga clic en **SQL Server Management Studio**.  
  
3.  Conéctese a la instancia de Analysis Services, por ejemplo **[su nombre de servidor]\POWERPIVOT**. Si puede conectarse a la instancia, ha comprobado que el servicio se está ejecutando.  
  
##  <a name="bkmk_config"></a> Paso 2: Configurar la integración de SharePoint básica de Analysis Services  
 En los pasos siguientes se describen los cambios de configuración necesarios para poder interactuar con modelos de datos avanzados de Excel en una biblioteca de documentos de SharePoint. Complete estos pasos después de instalar SharePoint Server 2013 y SQL Server Analysis Services.  
  
### <a name="grant-excel-services-server-administration-rights-on-analysis-services"></a>Conceder derechos de administración de servidor de Excel Services en Analysis Services  
 No es necesario completar esta sección si durante la instalación de Analysis Services agregó la cuenta de servicio Aplicación de Excel Services como administrador de Analysis Services.  
  
1.  En el servidor de Analysis Services, inicie SQL Server Management Studio y conéctese a la instancia de Analysis; por ejemplo, `[MyServer]\POWERPIVOT`.  
  
2.  En el Explorador de objetos, haga clic con el botón secundario en el nombre de instancia y, a continuación, haga clic en **Propiedades**.  
  
     ![Ver las propiedades de un servidor SSAS](../../../sql-server/install/media/as-ssms-proeprties.gif "ver las propiedades de un servidor de SSAS")  
  
3.  En el panel izquierdo, haga clic en **Seguridad**. Agregue el inicio de sesión de dominio que configuró para la aplicación de Excel Services en el paso 1.  
  
     ![Configuración de seguridad de un servidor SSAS](../../../sql-server/install/media/as-ssms-security.gif "configuración de seguridad de un servidor de SSAS")  
  
### <a name="configure-excel-services-for-analysis-services-integration"></a>Configurar Excel Services para la integración de Analysis Services  
  
1.  En Administración central de SharePoint, en el grupo Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en el nombre de la aplicación de servicio; el nombre predeterminado es **Aplicación de Excel Services**.  
  
3.  En la página **Administrar la aplicación de Excel Services**, haga clic en **Configuración del modelo de datos**.  
  
4.  Haga clic en **Agregar servidor**.  
  
5.  En **Nombre del servidor**, escriba el nombre del servidor de Analysis Services y el nombre de instancia de PowerPivot. Por ejemplo, `MyServer\POWERPIVOT`. El nombre de instancia de PowerPivot es necesario.  
  
     Escriba una descripción.  
  
6.  Haga clic en **Aceptar**.  
  
7.  Los cambios surtirán efecto en unos minutos; o bien, puede **Detener** e **Iniciar** el servicio **Excel Calculation Services**. En  
  
     Otra opción es abrir un símbolo del sistema con privilegios de administrador y escribir `iisreset /noforce`.  
  
     Puede comprobar si Excel Services reconoce el servidor examinando las entradas del registro de ULS. Verá entradas similares a la siguiente:  
  
    ```  
    Excel Services Application            Data Model        27           Medium                Check Administrator Access ([ServerName]\POWERPIVOT): Pass.        f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Server Version ([ServerName]\POWERPIVOT): Pass (11.0.2809.24 >= 11.0.2800.0).         f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Deployment Mode ([ServerName]\POWERPIVOT): Pass.            f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
  
    ```  
  
##  <a name="bkmk_verify"></a> Paso 3: Comprobar la integración  
 Los pasos siguientes le guían por la creación y carga de un nuevo libro para comprobar la integración de Analysis Services. Necesitará una base de datos de SQL Server para completar los pasos.  
  
1.  **Nota:** Si ya tiene un libro avanzado con segmentaciones de datos o filtros, puede cargarlo en la biblioteca de documentos de SharePoint y comprobar que puede interactuar con los filtros y segmentaciones de datos desde la vista de biblioteca de documentos.  
  
2.  Inicie un nuevo libro en Excel.  
  
3.  En la pestaña Datos, haga clic en **De otros orígenes** en la cinta de opciones de **Obtener datos externos**.  
  
4.  Seleccione **De SQL Server**.  
  
5.  En el **Asistente para la conexión de datos**, escriba el nombre de la instancia de SQL Server que tiene la base de datos que desea usar.  
  
6.  En Credenciales de inicio de sesión, compruebe que se ha seleccionado **Usar autenticación de Windows** y haga clic en **Siguiente**.  
  
7.  Seleccione la base de datos que desea usar.  
  
8.  Compruebe que la casilla **Conectar con una tabla específica** está activada.  
  
9. Active la casilla **Habilitar la selección de varias tablas y agregar tablas al modelo de datos de Excel** .  
  
10. Seleccione las tablas que desea importar.  
  
11. Active la casilla **Importar las relaciones entre las tablas seleccionadas**y haga clic en **Siguiente**. La importación de varias tablas de una base de datos relacional le permite trabajar con tablas que ya están relacionadas. Ahorra pasos porque no tiene que crear las relaciones manualmente.  
  
12. En la página **Guardar archivo de conexión de datos y finalizar** del asistente, escriba un nombre para la conexión y haga clic en **Finalizar**.  
  
13. Aparecerá el cuadro de diálogo **Importar datos** . Elija **Informe de tabla dinámica**y haga clic en **Aceptar**.  
  
14. Aparecerá en el libro una lista de campos de tabla dinámica.   
    En la lista de campos, haga clic en la pestaña **Todos** .  
  
15. Agregue campos a las áreas Fila, Columnas y Valor de la lista de campos.  
  
16. Agregue una segmentación de datos o un filtro a la tabla dinámica. **No omita este paso**. Una segmentación de datos o un filtro es el elemento que le ayudará a comprobar la instalación de Analysis Services.  
  
17. Guarde el libro en una biblioteca de documentos de un servidor de SharePoint Server 2013 que tenga Excel Services configurado. También puede guardar el libro en un recurso compartido de archivos y cargarlo en la biblioteca de documentos de SharePoint Server 2013.  
  
18. Haga clic en el nombre del libro para verlo en SharePoint y haga clic en la segmentación de datos o cambie el filtro que agregó anteriormente. Si se produce una actualización de datos, sabe que Analysis Services está instalado y disponible para Excel Services. Si abre el libro en Excel usará una copia almacenada en memoria caché y no el servidor de Analysis Services.  
  
##  <a name="bkmk_firewall"></a> Configurar Firewall de Windows para permitir el acceso a Analysis Services  
 Use la información del tema [Configure the Windows Firewall to Allow Analysis Services Access](../configure-the-windows-firewall-to-allow-analysis-services-access.md) para determinar si necesita desbloquear puertos de un firewall para permitir el acceso a Analysis Services o a PowerPivot para SharePoint. Puede seguir los pasos proporcionados en el tema para configurar las opciones de los puertos y del firewall. En la práctica, debe realizar estos pasos juntos para permitir el acceso al servidor de Analysis Services.  
  
##  <a name="bkmk_upgrade_workbook"></a> Actualizar libros y actualización de datos programada  
 Los pasos necesarios para actualizar libros creados en versiones anteriores de PowerPivot dependen de la versión de PowerPivot que creó el libro. Para obtener más información, vea [Actualizar libros y actualización de datos programada &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
##  <a name="bkmk_multiple_servers"></a> Más allá de la instalación de servidor único, PowerPivot para Microsoft SharePoint  
 **Web front-end (WFE)** o **nivel intermedio:**: Para usar un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] servidor en modo de SharePoint en una granja de servidores de SharePoint mayor e instalar características adicionales de PowerPivot en la granja, ejecute el paquete del instalador **spPowerPivot.msi** en cada uno de los servidores de SharePoint. El archivo spPowerPivot.msi instala los proveedores de datos necesarios y la herramienta de configuración de PowerPivot para SharePoint 2013.  
  
 Para obtener información acerca de la instalación y la configuración de nivel intermedio, vea lo siguiente:  
  
-   [Instalar o desinstalar PowerPivot para SharePoint complemento &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   Para descargar el archivo .msi, vea [Microsoft SQL Server 2014 PowerPivot para Microsoft SharePoint 2013](https://go.microsoft.com/fwlink/?LinkID=324854).  
  
-   [Configurar PowerPivot e implementar soluciones &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
 **Redundancia y carga del servidor:** Instalar un segundo o más [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] servidores en modo de SharePoint proporcionará redundancia de la [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] funcionalidad del servidor. Los servidores adicionales también repartirán la carga entre distintos servidores. Para obtener más información, vea:  
  
-   [Configurar Analysis Services para procesar los modelos de datos de Excel Services](https://technet.microsoft.com/library/jj614437\(v=office.15\)) (https://technet.microsoft.com/library/jj614437(v=office.15)).  
  
-   [Administrar la configuración de modelo de datos de Excel Services (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780\(v=office.15\)) (https://technet.microsoft.com/library/jj219780(v=office.15)).  
  
 ![Configuración de SharePoint](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "configuración de SharePoint") [enviar comentarios e información de contacto a través de Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Vea también  
 [Migrar PowerPivot para SharePoint 2013](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [Instalar o desinstalar PowerPivot para SharePoint complemento &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [Actualizar libros y actualización de datos programada &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
