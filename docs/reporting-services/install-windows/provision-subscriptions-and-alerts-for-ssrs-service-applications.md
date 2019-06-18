---
title: Aprovisionar suscripciones y alertas para aplicaciones de servicio SSRS | Microsoft Docs
ms.date: 06/03/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Shared Service
- SharePoint Mode [Reporting Services]
- SharePoint Mode
- Reporting Services Service Application
- SSRS service application
ms.assetid: d0de3f1f-4887-47fb-bacf-46aaad74c4be
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: ef70b3430cc1028b7486bf663280cfcf740d9290
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62651957"
---
# <a name="provision-subscriptions-and-alerts-for-ssrs-service-applications"></a>Aprovisionar Subscripciones y alertas para aplicaciones de servicio SSRS
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] requieren el Agente SQL Server y la configuración de permisos del mismo. Si ve mensajes de error que indican que se requiere el Agente SQL Server y ha comprobado que se está ejecutando, actualice o compruebe los permisos. El ámbito de este tema es [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint y en él se describen tres formas de actualizar los permisos del Agente SQL Server con suscripciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Las credenciales que use para los pasos de este tema deben disponer de los permisos adecuados para conceder permisos de ejecución a RSExecRole para los objetos de la aplicación de servicio, msdb y las bases de datos maestras.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2016 &#124; SharePoint 2013|  
  
 ![Permisos de Agente SQL para bases de datos de aplicación de servicio](../../reporting-services/install-windows/media/rs-provisionsqlagent.gif "Permisos de Agente SQL para bases de datos de aplicación de servicio")  
  
||Descripción|  
|------|-----------------|  
|**1**|Instancia del Motor de base de datos de SQL Server que hospeda las bases de datos de aplicación de servicio de Reporting Services.|  
|**2**|Instancia del agente SQL Server para la instancia del motor de base de datos SQL.|  
|**3**|Bases de datos de aplicación de servicio de Reporting Services. Los nombres se basan en la información utilizada para crear la aplicación de servicio. A continuación se muestran los nombres de la base de datos de ejemplo:<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0_Alerting<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0TempDB|  
|**4**|Base de datos maestra y de MSDB de la instancia del motor de base de datos de SQL Server.|  
  
 Use uno de los tres métodos siguientes para actualizar los permisos:  
  
1.  En la página **Provisiones y Suscripciones y alertas** , escriba las credenciales y haga clic en **Aceptar**.  
  
2.  En la página Provisiones, suscripciones y alertas, haga clic en el botón **Descargar script** para descargar un script Transact-SQL que se puede usar para configurar los permisos.  
  
3.  Ejecute un cmdlet de PowerShell para compilar un script Transact-SQL que se pueda utilizar para configurar los permisos.  
  
### <a name="to-update-permissions-using-the-provision-page"></a>Para actualizar los permisos mediante la página de aprovisionamiento  
  
1.  En Administración central de SharePoint, en el grupo **Administración de aplicaciones** , haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Busque su aplicación de servicio en la lista y haga clic en el nombre de la aplicación o haga clic en la columna **Tipo** para seleccionar la aplicación de servicio y haga clic en el botón **Administrar** en la cinta de opciones de SharePoint.  
  
3.  En la página **Administrar la aplicación de Reporting Services** , haga clic en **Aprovisionar suscripciones y alertas**.  
  
4.  Si el administrador de SharePoint tiene privilegios suficientes para la base de datos maestra y las bases de datos de aplicación de servicio, escriba esas credenciales.  
  
5.  Haga clic en el botón **Aceptar** .  
  
##  <a name="bkmk_download"></a> Para descargar el script Transact-SQL  
  
1.  En Administración central de SharePoint, en el grupo **Administración de aplicaciones** , haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Busque su aplicación de servicio en la lista y haga clic en el nombre de la aplicación o haga clic en la columna **Tipo** para seleccionar la aplicación de servicio y haga clic en el botón **Administrar** en la cinta de opciones de SharePoint.  
  
3.  En la página **Administrar la aplicación de Reporting Services** , haga clic en **Aprovisionar suscripciones y alertas**.  
  
4.  En el área **Ver estado** , compruebe que el Agente SQL Server se está ejecutando.  
  
5.  Haga clic en **Descargar script** para descargar un script de Transact-SQL que puede ejecutar SQL Server Management Studio para conceder los permisos. El nombre del archivo de script que se cree contendrá el nombre de su nombre de aplicación de servicio de Reporting Services, por ejemplo, **[nombre de la aplicación de servicio] -GrantRights.sql**.  
  
### <a name="to-generate-the-transact-sql-statement-with-powershell"></a>Para generar la instrucción Transact-SQL con PowerShell  
  
1.  También puede usar un cmdlet de Windows PowerShell en el Shell de administración de SharePoint 2016 o SharePoint 2013 para crear el script Transact-SQL.  
  
2.  En el menú **Iniciar** , haga clic en **Todos los programas**.  
  
3.  Expanda **Productos Microsoft SharePoint 2016** y haga clic en **Consola de administración de SharePoint 2016**.
  
4.  Actualice el siguiente cmdlet de PowerShell reemplazando el nombre de la base de datos del servidor de informes, la cuenta del grupo de aplicaciones y la ruta de acceso de la instrucción.  
  
     **Sintaxis de cmdlet:** `Get-SPRSDatabaseRightsScript -DatabaseName <ReportingServices database name> -UserName <app pool account> -IsWindowsUser | Out-File <path of statement>`  
  
     **Cmdlet de prueba:** `Get-SPRSDatabaseRightsScript -DatabaseName ReportingService_46fd00359f894b828907b254e3f6257c -UserName "NT AUTHORITY\NETWORK SERVICE" -IsWindowsUser | Out-File c:\SQLServerAgentrights.sql`  
  
## <a name="using-the-transact-sql-script"></a>Usar el script Transact-SQL  
 Los siguientes procedimientos se pueden utilizar con los scripts descargados de la página de provisiones o con los scripts creados con PowerShell.  
  
#### <a name="to-load-the-transact-sql-script-in-sql-server-management-studio"></a>Para cargar el script Transact-SQL en SQL Server Management Studio  
  
1.  Para abrir SQL Server Management Studio, en el menú **Inicio** , haga clic en [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] y en **SQL Server Management Studio**.  
  
2.  En el cuadro de diálogo **Conectar con el servidor** establezca las opciones siguientes:  
  
    -   En la lista **Tipo de servidor** , seleccione **Motor de base de datos**.  
  
    -   En **Nombre del servidor**, escriba el nombre de la instancia de SQL Server en la que desea configurar el Agente SQL Server.  
  
    -   Seleccione un modo de autenticación.  
  
    -   Si se conecta con la Autenticación de SQL Server, proporcione un inicio de sesión y una contraseña.  
  
3.  Haga clic en **Conectar**.  
  
#### <a name="to-run-the-transact-sql-statement"></a>Para ejecutar la instrucción Transact-SQL  
  
1.  En la barra de herramientas de SQL Server Management Studio, haga clic en **Nueva consulta**.  
  
2.  En el menú **Archivo** , haga clic en **Abrir**y, a continuación, en **Archivo**.  
  
3.  Navegue a la carpeta donde guardó la instrucción Transact-SQL que generó en el Shell de administración de SharePoint 2016 o SharePoint 2013.  
  
4.  Haga clic en el archivo y, a continuación, haga clic en **Abrir**.  
  
     La instrucción se agrega a la ventana de consulta.  
  
5.  Haga clic en **Ejecutar**.  
  
  
