---
title: Desinstalar y quitar Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: efc2431c-588b-42e7-b23b-c875145a33f6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e9bac4dba698af6e7f3dc57904da66a7fb15a08b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62989048"
---
# <a name="uninstall-and-remove-master-data-services"></a>Desinstalar y quitar Master Data Services
  Para desinstalar la característica [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], siga los pasos de [Desinstalar una instancia existente de SQL Server &#40;programa de instalación&#41;](../../../2014/sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md) y especifique [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] como característica para la operación de quitar en la página de **Seleccionar características**. El proceso de desinstalación quita las carpetas y archivos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], y desinstala [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] del equipo local.  
  
 Para evitar una pérdida de datos y que se vean afectados otros equipos del sistema, algunos elementos no se quitan ni se cambian durante el proceso de desinstalación. Revise la siguiente tabla para determinar si se dejan o quitan elementos.  
  
|Elemento|Descripción|  
|----------|-----------------|  
|Archivos y carpetas|El proceso de desinstalación quita la mayoría de las carpetas y archivos de la ruta de acceso de instalación.<br /><br /> Este proceso no quita las carpetas Master Data Services ni MDSTempDir de la ubicación de instalación. Después de completarse el proceso de desinstalación, puede eliminar manualmente estas carpetas del sistema de archivos. Para obtener más información, vea [Permisos de carpetas y archivos&#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md).|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] ensamblados|El proceso de desinstalación quita los ensamblados de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] de la memoria caché global de ensamblados (GAC).|  
|Base de datos|El proceso de desinstalación no afecta a la base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] . La base de datos permanece intacta en la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que no pierda datos, incluidos los datos maestros, los objetos del modelo, los permisos de usuario y grupo, las reglas de negocios, etc.<br /><br /> Si no necesita la base de datos y no prevé conectarla a otro sitio web ni a otra aplicación de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] en el futuro, puede eliminar la base de datos de la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que la hospeda. Para obtener más información, vea [Eliminar una base de datos](../../relational-databases/databases/delete-a-database.md).|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] y Web.config|El proceso de desinstalación quita la carpeta WebApplication del sistema de archivos. Esta carpeta contiene los archivos de la aplicación web y el archivo Web.config de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].<br /><br /> **\*\* Importante \*\*** Antes de la desinstalación, quizá quiera copiar el archivo Web.config en otra ubicación para conservar la configuración personalizada u otra información del archivo. Después de completarse el proceso de desinstalación, el archivo Web.config no se puede recuperar.|  
|Elementos de Internet Information Services (IIS)|El proceso de desinstalación no afecta a los grupos de aplicaciones, a los sitios web ni a las aplicaciones web de IIS en el equipo local. Puesto que el proceso de desinstalación quita la carpeta WebApplication y el archivo Web.config de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], las aplicaciones web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] que necesiten esos archivos ya no entregarán contenido. Si los usuarios intentan tener acceso a la aplicación web, recibirá un HTTP Error 500.19-Internal Server Error: "No se puede tener acceso la página solicitada porque los datos de configuración de la página no están válidos."<br /><br /> Si ya no necesita el sitio o la aplicación web, ni el grupo de aplicaciones que atienden el sitio o la aplicación, puede usar una herramienta de IIS para eliminarlos. Para obtener más información, vea [IIS 7.0: Guía de operaciones](https://go.microsoft.com/fwlink/?LinkId=184885) en TechNet de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .|  
|Grupo**MDS_ServiceAccounts** |Después de completarse el proceso de desinstalación, se conservan el grupo de Windows **MDS_ServiceAccounts** y las cuentas de servicio agregadas al grupo. Si ya no necesita el grupo ni las cuentas, puede quitarlos.|  
|Registro|El proceso de desinstalación quita todas las claves del Registro de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] del Registro de Windows.|  
  
## <a name="see-also"></a>Vea también  
 [Instalar Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
