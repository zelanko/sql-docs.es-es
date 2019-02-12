---
title: Cambios de comportamiento en SQL Server Reporting Services en SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- rows [Reporting Services], heights
- leading blanks
- installing Reporting Services, behavior changes with release
- cryptography [Reporting Services]
- Setup [Reporting Services], behavior changes with release
- DefaultValueQueryBased property
- encryption [Reporting Services]
- decryption [Reporting Services]
- blank characters [SQL Server]
- initializing installations [Reporting Services]
- behavior changes [Reporting Services]
ms.assetid: 2a767f0f-84f2-4099-8784-1e37790f858e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: b845480863facf66ff33c5d976531118edb2d4a9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56033196"
---
# <a name="behavior-changes-to-sql-server-reporting-services--in-sql-server-2014"></a>Cambios de comportamiento de SQL Server Reporting Services en SQL Server 2014
  En este tema se describen los cambios de comportamiento en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Los cambios de comportamiento afectan al modo en que las características funcionan o interactúan en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] en comparación con las versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 En este tema:  
  
-   [Los cambios de comportamiento de SQL Server 2014 Reporting Services](#bkmk_sql14)  
  
-   [Los cambios de comportamiento de SQL Server 2012 Reporting Services](#bkmk_rc0)  
  
-   [Los cambios de comportamiento de SQL Server 2008 R2 Reporting Services](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Cambios de comportamiento de Reporting Services  
 No hay cambios de comportamiento en las características de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Cambios de comportamiento de Reporting Services  
 En esta sección se describen los cambios de comportamiento en el modo de SharePoint de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
### <a name="view-items-permission-will-not-download-shared-datasets-sharepoint-mode"></a>El permiso Ver elementos no descargará conjuntos de datos compartidos (modo de SharePoint)  
 **Nuevo comportamiento:** Los usuarios con el permiso de SharePoint "Ver elementos" ya no pueden descargar el contenido de conjuntos de datos compartidos de Reporting Services. Este cambio de comportamiento ahora es coherente con los permisos "Ver elementos" para los informes, orígenes de datos y modelos. Los usuarios con permiso "Ver elementos" pueden ver y ejecutar informes, orígenes de datos y modelos, pero no pueden descargar su contenido.  
  
 **Comportamiento anterior:** Los usuarios con el permiso de SharePoint "Ver elementos" podían descargar el contenido de conjuntos de datos compartidos de Reporting Services.  
  
 Para obtener más información acerca de los niveles de permisos de SharePoint, vea [Permisos de usuario y niveles de permisos](https://technet.microsoft.com/library/cc721640.aspx)  
  
### <a name="report-server-trace-logs-are-in-a-new-location-for-sharepoint-mode-sharepoint-mode"></a>Los registros de seguimiento del Servidor de informes se encuentran en una nueva ubicación para el modo de SharePoint (Modo de SharePoint)  
 **Nuevo comportamiento:** Para un servidor de informes instalado en modo de SharePoint, los registros de seguimiento del servidor de informes estarán en %Programfiles%\Common Files\Microsoft Shared\Web Server Extensions\14\Web Services\ReportServer\LogFiles.  
  
 **Comportamiento anterior:** Se encontraron registros de seguimiento del servidor de informes en una ruta similar al siguiente: %Programfilesdir%\Microsoft SQL Server\\\Reporting Services\LogFiles < instancia_rs >  
  
### <a name="getserverconfiginfo-soap-api-is-no-longer-supported-sharepoint-mode"></a>La API SOAP GetServerConfigInfo ya no se admite (Modo de SharePoint)  
 **Nuevo comportamiento**: Use el cmdlet de PowerShell "Get-SPRSServiceApplicationServers"  
  
 **Comportamiento anterior:** Los clientes podían desarrollar código de cliente SOAP para comunicarse directamente con el extremo de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y llamar a GetReportServerConfigInfo ().  
  
### <a name="report-server-configuration-and-management-tools"></a>Herramientas de administración y Configuración del servidor de informes  
  
#### <a name="configuration-manager-is-not-used-for-sharepoint-mode"></a>El Administrador de configuración no se usa en modo de SharePoint  
 **Nuevo comportamiento:** El Administrador de configuración de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ya no admite servidores de informes en modo de SharePoint. La configuración del modo de SharePoint de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ahora se puede completar con Administración central de SharePoint; por tanto, el Administrador de configuración de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ya no admite el modo de SharePoint. Ahora el Administrador de configuración se utiliza solo con los servidores de informes en modo nativo.  
  
#### <a name="you-cannot-change-the-server-from-one-mode-to-another"></a>No se puede cambiar el servidor de un modo a otro  
 **Nuevo comportamiento:** No puede cambiar los modos de servidor. Si se instala un servidor de informes en modo nativo, no podrá cambiarlo o volver a configurarlo para estar en modo de SharePoint. Si lo instala en modo de SharePoint, no podrá cambiarlo al modo nativo.  
  
 **Comportamiento anterior:** El cliente instala un servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en modo de SharePoint. Si el cliente desea cambiar el servidor de informes al modo nativo, puede abrir el administrador de configuración de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y cambiar al modo nativo creando una base de datos nueva o conectándose a una existente en modo nativo. El cliente puede utilizar también el Administrador de configuración de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para cambiar desde el modo de SharePoint al modo nativo.  
  
##  <a name="bkmk_kj"></a> Los cambios de comportamiento de SQL Server 2008 R2 Reporting Services  
 En esta sección se describen los cambios de comportamiento en [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  Dado que SQL Server 2008 R2 es una actualización de versión menor de SQL Server 2008, recomendamos también revisar el contenido en la sección de SQL Server 2008.  
  
### <a name="secureconnectionlevel-property-in-the-reporting-services-wmi-provider-library"></a>Propiedad SecureConnectionLevel en la biblioteca de proveedores WMI de Reporting Services  
 En la biblioteca del proveedor WMI para [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], **SecureConnectionLevel** permite que los valores de propiedad `0`,`1`,`2`,`3`, con `0` que indica que capa de sockets seguros (SSL) no se requiere para ninguno de los métodos de servicio Web, `3` que indica que SSL se requiere para todos los métodos de servicio Web, y `1` y `2` indicar subconjuntos de métodos de servicio Web que requieren SSL. En [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], estos valores tendrán solo dos significados posibles:  
  
-   `0` indica que SSL no se requiere para cualquiera de los métodos de servicio web.  
  
-   Un número entero positivo indica que SSL se requiere para todos los métodos de servicio web.  
  
 Este cambio afecta al modo en que el servidor de informes responde a las llamadas del servicio web. Por ejemplo, <xref:ReportService2005.ReportingService2005.ListSecureMethods%2A> ahora devuelve nothing si **SecureConnectionLevel** se establece en 0 y todos los métodos de <xref:ReportService2005.ReportingService2005> si **SecureConnectionLevel** está establecido en `1`, `2`, o `3`.  
  
## <a name="see-also"></a>Vea también  
 [¿Qué novedades &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [Características desusadas en SQL Server Reporting Services en SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md)   
 [Funcionalidad no incluida en SQL Server Reporting Services en SQL Server 2014](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)   
 [Cambios importantes de SQL Server Reporting Services en SQL Server 2014](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)  
  
  
