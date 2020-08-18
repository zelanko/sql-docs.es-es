---
description: Grupos de atributos (Master Data Services)
title: Grupos de atributos
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services]
- attribute groups [Master Data Services], about attribute groups
ms.assetid: 648b3d0b-e15a-45f9-8292-3a54a072e62c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e6ef092efb1133d5067f9f3959765017f695acc5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413441"
---
# <a name="attribute-groups-master-data-services"></a>Grupos de atributos (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

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
 Cuando se crea un grupo de atributos, se oculta automáticamente para todos los usuarios excepto para la persona que lo creó. Para obtener más información sobre cómo hacer visible el grupo, consulte [Hacer que un grupo de atributos sea visible para los usuarios &#40;Master Data Services&#41;](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md).  
  
 Si desea ocultar un atributo específico dentro de un grupo, puede asignar permisos **Denegar** al atributo. Para más información, vea [Permisos de hoja &#40;Master Data Services&#41;](../master-data-services/leaf-permissions-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear un nuevo grupo de atributos y agregarle atributos.|[Crear un grupo de atributos &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)|  
|Hacer que un grupo de atributos sea visible para los usuarios.|[Hacer que un grupo de atributos sea visible para los usuarios &#40;Master Data Services&#41;](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)|  
|Cambiar el nombre de un grupo de atributos existente.|[Cambiar el nombre de un grupo de atributos &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-group-name-master-data-services.md)|  
|Eliminar un grupo de atributos existente.|[Eliminar un grupo de atributos &#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-group-master-data-services.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
