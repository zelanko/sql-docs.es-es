---
title: Permisos de carpetas y archivos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- security [Master Data Services], file and folder
- folders [Master Data Services]
- files [Master Data Services]
ms.assetid: 6402d81d-7349-47b1-95ca-99b0c0f4f373
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: e2d6833165def5c73ebe15ec77cf23cffb1c1a3d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717383"
---
# <a name="folder-and-file-permissions-master-data-services"></a>Permisos de carpetas y archivos (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Al instalar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], las carpetas y archivos se instalan en el sistema de archivos en la ruta de instalación que especifica para las características compartidas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Si usa la ruta de instalación predeterminada para las características compartidas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , la ruta de instalación de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] es *unidad*:\Archivos de programa\Microsoft SQL Server\130\Master Data Services. Aunque puede cambiar la ruta de instalación de las características compartidas, sea consciente de los permisos que se heredan de la carpeta primaria y de los que se establecen explícitamente para [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
## <a name="inherited-permissions"></a>Permisos heredados  
 La carpeta **Microsoft SQL Server** , la carpeta **Master Data Services** y la mayoría de las subcarpetas y archivos heredan los permisos de la carpeta primaria especificada en el programa de instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Si elige la ubicación de instalación predeterminada, la carpeta principal de la que se heredan los permisos es *unidad*:\Archivos de programa. En la siguiente tabla se describen los permisos predeterminado para **Archivos de programa**.  
  
> [!NOTE]  
>  Si modifica los permisos predeterminados para **Archivos de programa**o elige una ubicación de instalación diferente, los permisos de las carpetas y archivos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] heredados de la carpeta principal y los permisos generales pueden diferir de los descritos en la tabla siguiente.  
  
###### <a name="program-files-default-permissions"></a>Permisos predeterminados de Archivos de programas  
  
|Nombre de grupo o cuenta|Permisos|  
|---------------------------|-----------------|  
|CREATOR OWNER|Permisos especiales|  
|SYSTEM|Permisos especiales|  
|Administradores de|Permisos especiales|  
|Usuarios|Lectura y ejecución, mostrar contenido de carpetas, lectura|  
|TrustedInstaller|Mostrar contenido de carpetas, permisos especiales|  
  
## <a name="explicit-permissions"></a>Permisos explícitos  
 La carpeta **MDSTempDir** y el archivo Web.config de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (en la carpeta **WebApplication** ) no heredan permisos. Tienen permisos que se establecen explícitamente al instalar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], sin tener en cuenta la ruta de instalación que elija. No modifique estos permisos.  
  
###### <a name="mdstempdir-permissions"></a>Permisos de MDSTempDir  
  
|Nombre de grupo o cuenta|Permisos|  
|---------------------------|-----------------|  
|SYSTEM|Modificar, lectura y ejecución, mostrar contenido de carpetas, lectura, escritura|  
|Administradores de|Modificar, lectura y ejecución, mostrar contenido de carpetas, lectura, escritura|  
|MDS_ServiceAccounts|Modificar, lectura y ejecución, mostrar contenido de carpetas, lectura, escritura|  
  
###### <a name="webconfig-permissions"></a>Permisos de Web.config  
  
|Nombre de grupo o cuenta|Permisos|  
|---------------------------|-----------------|  
|SYSTEM|Control total, modificar, lectura y ejecución, lectura, escritura|  
|Administradores de|Control total, modificar, lectura y ejecución, lectura, escritura|  
|MDS_ServiceAccounts|Lectura y ejecutar, lectura|  
  
 Para obtener más información sobre el contenido del archivo Web.config de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], consulte [Referencia de la configuración web &#40;Master Data Services&#41;](../master-data-services/web-configuration-reference-master-data-services.md).  
  
## <a name="see-also"></a>Ver también  
 [Instalar Master Data Services](../master-data-services/install-windows/install-master-data-services.md)  
  
  
