---
title: Utilidades del símbolo del sistema del servidor de informes (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsconfig utility
- components [Reporting Services], command line utilities
- rs utility
- command prompt utilities [Reporting Services]
- rskeymgmt utility
ms.assetid: 68f2f9f4-f894-40ff-a71c-f9756bf4b68c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 07da79ea46ca0e9e23abb7197730821d8c31bfa8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66100001"
---
# <a name="report-server-command-prompt-utilities-ssrs"></a>Utilidades del símbolo del sistema del servidor de informes (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye varias utilidades de línea de comandos que puede usar para administrar un servidor de informes. Estas utilidades se instalan automáticamente cuando se instala el servidor de informes.  
  
|Nombre|Archivo de comandos|Modo de implementación admitido|Descripción|  
|----------|------------------|-------------------------------|-----------------|  
|Utilidad RSS|rs.exe|Modo nativo y modo de SharePoint. La compatibilidad con el modo de SharePoint se introdujo con la versión [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .|La [utilidad rs](rs-exe-utility-ssrs.md) es un host de script que se puede utilizar para llevar a cabo operaciones de script. Use esta herramienta para ejecutar scripts de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que copian datos entre distintas bases de datos del servidor de informes, publican informes, crean elementos en una base de datos del servidor de informes, etc. Para más información sobre cómo usar scripts para administrar un servidor, vea [Script para tareas administrativas y de implementación](script-deployment-and-administrative-tasks.md).|  
|Cmdlets de Powershell||Solo SharePoint|Para consultar una lista de los cmdlets de PowerShell, vea [Cmdlets de PowerShell para el modo de SharePoint de Reporting Services](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md).|  
|rsconfig, utilidad|rsconfig.exe|Solo nativo|La utilidad [rsconfig](rsconfig-utility-ssrs.md) se utiliza para configurar y administrar una conexión del servidor de informes con la base de datos del servidor de informes. También puede utilizarla para especificar la cuenta de usuario que se va a utilizar para el procesamiento de informes desatendidos. Para más información, vea [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../report-server/reporting-services-report-server-native-mode.md). Para más información sobre la configuración de la conexión, vea [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).|  
|Utilidad Rskeymgmt|rskeymgmt.exe|Solo nativo|La utilidad [rskeymgmt](rskeymgmt-utility-ssrs.md) es una herramienta de administración de claves de cifrado. Puede utilizarla para realizar copias de seguridad, aplicar y volver a crear claves simétricas. También puede utilizar esta herramienta para adjuntar una instancia del servidor de informes a una base de datos compartida del servidor de informes. Rskeymgmt puede utilizarse en operaciones de recuperación de base de datos. Para volver a utilizar una base de datos existente en una nueva instalación, aplique una copia de seguridad de la clave simétrica. Si las claves no se pueden recuperar, esta herramienta proporciona un método para eliminar el contenido cifrado que ya no utilice. Para más información sobre la administración de claves y el almacenamiento de información confidencial, vea [Almacenar datos cifrados del servidor de informes &#40;SSRS Configuration Manager&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md) y [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
  
> [!NOTE]  
>  Si prefiere utilizar una herramienta que tenga una interfaz gráfica de usuario, puede utilizar el Administrador de configuración de Reporting Services en lugar de `rsconfig` y `rskeymgmt`.  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Herramientas de Reporting Services](reporting-services-tools.md)   
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../report-server/reporting-services-report-server-native-mode.md)  
  
  
