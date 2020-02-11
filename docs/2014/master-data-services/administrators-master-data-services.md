---
title: Administradores (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], about administrators
- administrators [Master Data Services]
- models [Master Data Services], administrators
ms.assetid: d330aa4e-6ade-4b09-b376-1b15d6c78f7d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 146834648164e49632a62352d684a6da66a09e12
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65480015"
---
# <a name="administrators-master-data-services"></a>Administradores (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], hay dos tipos de administradores: los administradores de modelo y el administrador del sistema de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
## <a name="model-administrators"></a>Administradores de modelos  
 En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], un administrador de modelo es un usuario que tiene el permiso **Actualizar** asignado al objeto de modelo de nivel superior en la pestaña **objetos de modelo** y ningún otro permiso asignado.  
  
-   Si el usuario tiene acceso al área funcional del **Explorador** , podrá agregar, eliminar y actualizar todos los datos maestros de esta área.  
  
-   Si el usuario tiene acceso a otras áreas funcionales, puede realizar todas las tareas administrativas disponibles en el área funcional.  
  
 Cada modelo puede tener varios administradores. Cada usuario puede ser administrador de modelo para uno, varios o todos los modelos de la implementación de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
 Un usuario se puede configurar como administrador de modelo en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] o mediante programación. Para obtener más información, consulte [Crear un administrador de modelo &#40;Master Data Services&#41;](create-a-model-administrator-master-data-services.md).  
  
## <a name="master-data-services-system-administrator"></a>Administrador del sistema de Master Data Services  
 Solo hay un administrador del sistema [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. El administrador del sistema es el usuario especificado para la **cuenta de administrador** al crear [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] la base de datos.  
  
 El administrador del sistema de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]:  
  
-   Tiene acceso a todas las áreas funcionales automáticamente.  
  
-   Puede Agregar, eliminar y actualizar todos los datos maestros de todos los modelos en el área funcional del **Explorador** .  
  
 Puede cambiar el usuario que está asignado como administrador del sistema. Para obtener más información, vea [cambiar la cuenta de administrador del sistema &#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
## <a name="comparing-administrator-types"></a>Comparar los tipos de administradores  
  
|Tipo de administrador|Descripción|  
|------------------------|-----------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]Administrador del sistema|Los permisos asignados en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] no tienen ningún efecto sobre el acceso del administrador.<br /><br /> Tiene automáticamente el permiso **Actualizar** para todos los modelos.<br /><br /> Tiene acceso a todas las áreas funcionales automáticamente.<br /><br /> En MDM. tblUser, el valor de la columna **ID** es **1**.|  
|Administrador de modelo|Los permisos asignados en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] determinan si el usuario es o no un administrador de modelo.<br /><br /> Puede ser administrador de modelo según los permisos que se le asignen explícitamente o los permisos heredados de un grupo.<br /><br /> Es un administrador solo para los modelos que tienen el permiso **Actualizar** asignado al objeto de modelo de nivel superior y ningún otro permiso.<br /><br /> Solo tiene acceso a áreas funcionales a las que se permita el acceso.<br /><br /> En MDM. tblUser, el valor de la columna **ID** no es **1**.|  
  
## <a name="see-also"></a>Consulte también  
 [Cree un administrador de modelos &#40;Master Data Services&#41;](create-a-model-administrator-master-data-services.md)   
 [Cambie la cuenta de administrador del sistema &#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md)   
 [Crear una base de datos de Master Data Services](install-windows/create-a-master-data-services-database.md)   
 [Notificaciones &#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)  
  
  
