---
title: Atributo grupos (Master Data Services) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attribute groups [Master Data Services]
- attribute groups [Master Data Services], about attribute groups
ms.assetid: 648b3d0b-e15a-45f9-8292-3a54a072e62c
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b5c90f2a2df358af81f563f5740450ba130d24e5
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="attribute-groups-master-data-services"></a>Grupos de atributos (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], los grupos de atributos ayudan a organizar los atributos de una entidad. Cuando una entidad tiene muchos atributos, los grupos de atributos mejoran la forma en que se muestra una entidad en la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
## <a name="how-attribute-groups-change-the-display"></a>Cómo cambian la presentación los grupos de atributos  
 Los grupos de atributos se muestran como pestañas encima de la cuadrícula en el área funcional **Explorador** de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Cuando una entidad tiene un gran número de atributos y ve esa entidad en una cuadrícula en el **Explorador**, debe desplazar hacia la derecha para ver todos los atributos. Para evitar este desplazamiento, puede crear grupos de atributos.  
  
-   Los grupos de atributos siempre incluyen los atributos Name y Code.  
  
-   Cada atributo de una entidad puede pertenecer a uno o más grupos de atributos.  
  
-   Todos los atributos se incluyen automáticamente en la pestaña **Todos los atributos** en el **Explorador**.  
  
-   La pestaña **Todos los atributos** no se puede ocultar.  
  
 Los grupos de atributos se administran en el área funcional **Administración del sistema** de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="show-or-hide-attribute-groups"></a>Mostrar u ocultar grupos de atributos  
 Cuando se crea un grupo de atributos, se oculta automáticamente para todos los usuarios excepto para la persona que lo creó. Para obtener más información sobre cómo hacer visible el grupo, consulte [Make an Attribute Group Visible to Users &#40;Master Data Services&#41;](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md).  
  
 Si desea ocultar un atributo específico dentro de un grupo, puede asignar permisos **Denegar** al atributo. Para obtener más información, vea [permisos de hoja &#40; Master Data Services &#41; ](../master-data-services/leaf-permissions-master-data-services.md).  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear un nuevo grupo de atributos y agregarle atributos.|[Crear un grupo de atributos &#40; Master Data Services &#41;](../master-data-services/create-an-attribute-group-master-data-services.md)|  
|Hacer que un grupo de atributos sea visible para los usuarios.|[Hacer que un grupo de atributos sea Visible para los usuarios &#40; Master Data Services &#41;](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)|  
|Cambiar el nombre de un grupo de atributos existente.|[Cambiar un nombre de grupo de atributos &#40; Master Data Services &#41;](../master-data-services/change-an-attribute-group-name-master-data-services.md)|  
|Eliminar un grupo de atributos existente.|[Eliminar un grupo de atributos &#40; Master Data Services &#41;](../master-data-services/delete-an-attribute-group-master-data-services.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Atributos &#40; Master Data Services &#41;](../master-data-services/attributes-master-data-services.md)  
  
  
