---
title: "Página de configuración (Administrador de configuración de Master Data Services) de la base de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.mds.configmanager.dbpg.f1
ms.assetid: dd72220e-a599-465d-8b84-9bb6a7433216
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 212031f92de47da41ad2716b81740c6a42487e59
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="database-configuration-page-master-data-services-configuration-manager"></a>Página Configuración de base de datos (Administrador de configuración de Master Data Services)
  Use la página **Configuración de base de datos** para modificar la configuración del sistema de una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . La configuración del sistema afecta a todas las aplicaciones web y servicios web asociados a la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] seleccionada. Debe seleccionar o crear una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] antes de que se habiliten los valores del sistema y estén disponibles para su configuración.  
  
## <a name="current-database"></a>Base de datos actual  
 Seleccione una base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] existente o cree una base de datos nueva para la que se va a modificar la configuración del sistema. La nueva base de datos estará seleccionada una vez se haya creado.  
  
|Nombre del control|Description|  
|------------------|-----------------|  
|**Instancia de SQL Server**|Muestra el nombre de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] seleccionada. Estará en blanco hasta que se conecte a una instancia y, posteriormente, seleccione o cree una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**Base de datos de Master Data Services**|Muestra el nombre de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] seleccionada. Estará en blanco hasta que se conecte a una instancia y, posteriormente, seleccione o cree una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**Versión de la base de datos de Master Data Services**|La versión del esquema de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**Crear la base de datos**|Abre el asistente para **Crear base de datos** , desde el que se puede conectar a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y crear una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para esa instancia.|  
|**Seleccionar base de datos**|Abre el cuadro de diálogo **Conectar con base de datos** desde el que se puede conectar a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y seleccionar una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**Actualizar base de datos**|Abre un asistente desde el que puede actualizar una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] especificada. Este botón solo se habilita cuando la base de datos especificada tiene que actualizarse.|  
|**Reparar la base de datos**|Haga clic en este botón para asegurarse de que la base de datos de MDS está instalada correctamente. Esto puede resultar útil si hace una copia de seguridad de una base de datos de MDS y la restaura en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que nunca ha hospedado una base de datos de MDS.|  
  
## <a name="system-settings"></a>Configuración del sistema  
 Modifique la configuración del sistema para todas las aplicaciones web y servicios web asociados a la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] seleccionada.  
  
 Estas opciones están disponibles en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] y están almacenadas en la base de datos, en la tabla de configuración del sistema (mdm.tblSystemSetting). Para obtener más información, consulte [Configuración del sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
## <a name="see-also"></a>Vea también  
[Instalación de Master Data Services y la configuración](../master-data-services/master-data-services-installation-and-configuration.md) [requisitos &#40; de la base de datos Master Data Services &#41;](../master-data-services/install-windows/database-requirements-master-data-services.md)  
  
  
