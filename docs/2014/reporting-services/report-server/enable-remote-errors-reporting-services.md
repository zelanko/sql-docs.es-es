---
title: Habilitar los errores remotos (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- remote data source [Reporting Services]
- EnableRemoteError server property
ms.assetid: 5f05022b-d557-43e0-b50a-f5e2a1846b83
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 78a1d77440242eb96ca3ced08518829b2913a3a1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159876"
---
# <a name="enable-remote-errors-reporting-services"></a>Habilitar los errores remotos (Reporting Services)
  Es posible establecer propiedades de servidor en un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para devolver información adicional sobre condiciones de error que se produzcan en servidores remotos. Si un mensaje de error incluye el texto "Para obtener más información acerca de este error, navegue hasta el servidor de informes en el equipo del servidor local o habilite los errores remotos", puede establecer la propiedad `EnableRemoteErrors` para obtener información adicional que pueda ayudarle a solucionar el problema. Para obtener más información, consulte [Report Server System Properties](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
 **En este tema:**  
  
-   [Habilitar errores remotos para el modo de SharePoint](#bkmk_sharepoint)  
  
-   [Habilitar los errores remotos a través de SQL Server Management Studio (modo nativo)](#bkmk_mgtStudio)  
  
-   [Habilitar errores remotos mediante scripts (modo nativo)](#bkmk_script)  
  
-   [Modificar la tabla ConfigurationInfo (modo nativo)](#bkmk_ConfigurationInfo)  
  
##  <a name="bkmk_sharepoint"></a> Habilitar errores remotos para el modo de SharePoint  
 Hay diferentes procedimientos para habilitar errores remotos para el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . El procedimiento es distinto para las dos arquitecturas diferentes del servidor de informes. El servicio de SharePoint más reciente basado en la arquitectura que se introdujo en la versión de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] usa un valor que se puede configurar para cada aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . La arquitectura más antigua utiliza un solo valor de nivel de sitio.  
  
#### <a name="enable-remote-errors-for-a-reporting-services-service-application"></a>Habilitar errores remotos para una aplicación de servicio de Reporting Services  
  
1.  Para un servidor de informes en modo de SharePoint instalado con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o una versión más reciente de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], habilite la configuración de aplicación de servicio **Habilitar los errores remotos**. El valor se puede configurar para cada aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
2.  En Administración central de SharePoint, en el grupo **Administrar aplicaciones de servicio** , haga clic en **Administración de aplicaciones** .  
  
3.  Encuentre su aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y haga clic en el nombre.  
  
4.  Haga clic en **Configuración del sistema**.  
  
5.  Haga clic en **Habilitar errores remotos** en la sección **Seguridad** .  
  
6.  Haga clic en **Aceptar**.  
  
#### <a name="enable-remote-errors-for-a-sharepoint-site"></a>Habilitar errores remotos para un sitio de SharePoint  
  
1.  Para un servidor de informes en modo de SharePoint instalado con una versión de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anterior a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], habilite la configuración del sitio **Habilitar los errores remotos en modo local**.  
  
2.  En **Acciones de sitio** , haga clic en **Configuración del sitio** para el sitio desea modificar.  
  
3.  Haga clic en **Configuración del sitio de Reporting Services** en el grupo **Reporting Services** .  
  
4.  Haga clic en **Habilitar los errores remotos en modo local**.  
  
5.  Haga clic en **Aceptar**.  
  
##  <a name="bkmk_mgtStudio"></a> Habilitar los errores remotos a través de SQL Server Management Studio (modo nativo)  
  
1.  Inicie Management Studio y conéctese a una instancia del servidor de informes. Para obtener más información, consulte [conectarse a un servidor de informes en Management Studio](../tools/connect-to-a-report-server-in-management-studio.md) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
2.  Haga clic con el botón derecho en el nodo del servidor de informes y seleccione **Propiedades**.  
  
3.  Haga clic en **Avanzadas** para abrir la página de propiedades. Para más información, vea [Propiedades del servidor &#40;página Avanzadas&#41;](../tools/server-properties-advanced-page-reporting-services.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  En `EnableRemoteErrors`, seleccione `True`.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="bkmk_script"></a> Habilitar errores remotos mediante scripts (modo nativo)  
  
1.  Cree un archivo de texto y copie en él el script siguiente.  
  
    ```  
    Public Sub Main()  
      Dim P As New [Property]()  
      P.Name = "EnableRemoteErrors"  
      P.Value = True  
      Dim Properties(0) As [Property]  
      Properties(0) = P  
      Try  
        rs.SetSystemProperties(Properties)  
        Console.WriteLine("Remote errors enabled.")  
      Catch SE As SoapException  
        Console.WriteLine(SE.Detail.OuterXml)  
      End Try  
    End Sub  
    ```  
  
2.  Guarde el archivo como EnableRemoteErrors.rss.  
  
3.  Haga clic en **Inicio**, seleccione **Ejecutar**, escriba **cmd**y haga clic en **Aceptar** para abrir una ventana del símbolo del sistema.  
  
4.  Navegue hasta el directorio en el que se encuentra el archivo .rss que acaba de crear.  
  
5.  Escriba la línea de comandos siguiente sustituyendo *servername* por el nombre real del servidor:  
  
    ```  
    rs -i EnableRemoteErrors.rss -s http://servername/ReportServer  
    ```  
  
6.  Para obtener más información, vea [Utilidad RS.exe &#40;SSRS&#41;](../tools/rs-exe-utility-ssrs.md).  
  
##  <a name="bkmk_ConfigurationInfo"></a> Modificar la tabla ConfigurationInfo (modo nativo)  
  
1.  > [!NOTE]  
    >  Puede editar el **ConfigurationInfo** tabla en la base de datos del servidor de informes para establecer `EnableRemoteErrors` a `True`, pero si se utiliza el servidor de informes, debe usar SQL Server Management Studio o un script para modificar la configuración. Si modifica el valor de la base de datos, debe reiniciar el servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para que los cambios surtan efecto.  
  
  
