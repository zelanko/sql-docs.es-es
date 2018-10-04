---
title: Scripting y PowerShell con Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services]
- Reporting Services, scripting
- scripting [Reporting Services]
ms.assetid: 1ac2646d-ed5a-4436-b18f-2150c33f3d87
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 949ceb6b2aff0dd393cfa0c58e91355f20f4c741
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166525"
---
# <a name="scripting-and-powershell-with-reporting-services"></a>Secuencias de comandos y PowerShell con Reporting Services
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] admite una amplia gama de escenarios de desarrollo y administración a través de la secuencia de comandos, incluida la utilidad de línea de comandos rs.exe, cmdlets de PowerShell para servidores de informes de modo de SharePoint y aprovechando el [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] modelo de objeto de PowerShell para ambos nativo y Modo de SharePoint.  
  
-   Los administradores pueden escribir el script en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] para automatizar la manera de implementar y administrar una instalación del servidor de informes. Los administradores también pueden generar y ejecutar scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] que crean, configurar y actualizan una base de datos del servidor de informes. Los administradores también pueden usar las características de script de reproducción y registro en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para automatizar las tareas de mantenimiento rutinarias.  
  
-   Los programadores pueden crear aplicaciones personalizadas que incluyen el script. Puede ejecutar un script que realiza llamadas al servicio web del servidor de informes. Casi cualquier operación que puede escribir en código administrado también se puede escribir en script.  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] admite [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] secuencia de comandos de .NET como lenguaje de script que puede procesarse mediante la utilidad RS.exe, un host de script que se ejecuta en el servidor de informes.  
  
## <a name="reporting-services-sharepoint-mode-powershell-cmdlets-and-samples"></a>Ejemplos y cmdlets de PowerShell del modo SharePoint de Reporting Services  
 ![Contenido relacionado con PowerShell](../media/rs-powershellicon.jpg "Contenido relacionado con PowerShell")  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Modo de SharePoint incluye [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] cmdlets para la administración de servidor de informes.  
  
-   [PowerShell cmdlets for Reporting Services SharePoint Mode](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md) Incluye los ejemplos siguientes:  
  
    -   Crear una aplicación de servicio y un proxy  
  
    -   Revisar y actualizar una extensión de entrega  
  
    -   Obtener y establecer propiedades de la base de datos de la aplicación Reporting Services; por ejemplo, el tiempo de espera de la base de datos  
  
    -   Extensiones de datos de lista  
  
## <a name="reporting-services-object-model-and-powershell-samples"></a>Ejemplos de Powershell y modelo de objetos de Reporting Services  
 ![Contenido relacionado con PowerShell](../media/rs-powershellicon.jpg "Contenido relacionado con PowerShell")  
  
 PowerShell realiza la llamada al núcleo del modelo de objetos y para la mayor parte válida para los modos SharePoint y nativo; por ejemplo, el trabajo de migración, el trabajo de suscripción y más ejemplos relacionados para las suscripciones funcionan en SQL15.  
  
-   [Use PowerShell para cambiar y enumerar propietarios de suscripciones de Reporting Services y ejecutar una suscripción](../subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
-   [Usar PowerShell para crear una máquina virtual de Azure con un servidor de informes en modo nativo](http://msdn.microsoft.com/library/azure/dn449661.aspx).  
  
-   Vea la sección "Obtener acceso a las clases WMI mediante PowerShell" en [Obtener acceso al proveedor WMI de Reporting Services](access-the-reporting-services-wmi-provider.md).  
  
-   [Cómo administrar SSRS con PowerShell](http://curah.microsoft.com/13107/how-to-administer-ssrs-using-powershell).scriptin  
  
## <a name="rsexe-scripting-samples"></a>Ejemplos de secuencias de comandos de RS.exe  
  
-   [Ejemplo de Reporting Services rs.exe Script para migrar contenido entre servidores de informes](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
-   Consulte [Muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889)para obtener más ejemplos de secuencias de comandos, aplicaciones y extensiones.  
  
## <a name="see-also"></a>Vea también  
 [Utilidad RS.exe &#40;SSRS&#41;](rs-exe-utility-ssrs.md)   
 [Script para tareas administrativas y de implementación](script-deployment-and-administrative-tasks.md)   
 [Script con la utilidad rs.exe y el servicio web](script-with-the-rs-exe-utility-and-the-web-service.md)  
  
  
