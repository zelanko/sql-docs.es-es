---
title: Administradores (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], about administrators
- administrators [Master Data Services]
- models [Master Data Services], administrators
ms.assetid: d330aa4e-6ade-4b09-b376-1b15d6c78f7d
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: fcad38283e902b305afc5db3e47671b12e91b41f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304125"
---
# <a name="administrators-master-data-services"></a>Administradores (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], hay dos tipos de administradores: los administradores de modelo y el administrador del sistema de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
## <a name="model-administrators"></a>Administradores de modelos  
 En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], un administrador de modelo es un usuario que tiene **actualización** permiso asignado al objeto de modelo de nivel superior en el **objetos del modelo** pestaña y ningún otro asignan permisos.  
  
-   Si el usuario tiene acceso al área funcional del **Explorador** , podrá agregar, eliminar y actualizar todos los datos maestros de esta área.  
  
-   Si el usuario tiene acceso a otras áreas funcionales, puede realizar todas las tareas administrativas disponibles en el área funcional.  
  
 Cada modelo puede tener varios administradores. Cada usuario puede ser administrador de modelo para uno, varios o todos los modelos de la implementación de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
 Un usuario se puede configurar como administrador de modelo en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] o mediante programación. Para obtener más información, consulte [Create a Model Administrator &#40;Master Data Services&#41;](create-a-model-administrator-master-data-services.md).  
  
## <a name="master-data-services-system-administrator"></a>Administrador del sistema de Master Data Services  
 Solo hay un administrador del sistema [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. El administrador del sistema es el usuario especificado para el **cuenta de administrador** cuando se crea el [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] base de datos.  
  
 El administrador del sistema de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]:  
  
-   Tiene acceso a todas las áreas funcionales automáticamente.  
  
-   Puede agregar, eliminar y actualizar todos los datos maestros de todos los modelos en el **Explorer** área funcional.  
  
 Puede cambiar el usuario que está asignado como administrador del sistema. Para obtener más información, consulte [cambiar la cuenta de administrador del sistema &#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
## <a name="comparing-administrator-types"></a>Comparar los tipos de administradores  
  
|Tipo de administrador|Descripción|  
|------------------------|-----------------|  
|Administrador del sistema de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|Los permisos asignados en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] no tienen ningún efecto sobre el acceso del administrador.<br /><br /> Tiene automáticamente **actualización** permiso a todos los modelos.<br /><br /> Tiene acceso a todas las áreas funcionales automáticamente.<br /><br /> En mdm.tblUser, el valor de la **ID** columna es **1**.|  
|Administrador de modelo|Los permisos asignados en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] determinan si el usuario es o no un administrador de modelo.<br /><br /> Puede ser administrador de modelo según los permisos que se le asignen explícitamente o los permisos heredados de un grupo.<br /><br /> Es un administrador solo para los modelos que tienen **actualización** permiso asignado al objeto de modelo de nivel superior y ningún otro permiso.<br /><br /> Solo tiene acceso a áreas funcionales a las que se permita el acceso.<br /><br /> En mdm.tblUser, el valor de la **ID** columna no es **1**.|  
  
## <a name="see-also"></a>Vea también  
 [Crear un administrador de modelo &#40;Master Data Services&#41;](create-a-model-administrator-master-data-services.md)   
 [Cambiar la cuenta de administrador del sistema &#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md)   
 [Crear una base de datos de Master Data Services](install-windows/create-a-master-data-services-database.md)   
 [Las notificaciones &#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)  
  
  
