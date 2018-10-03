---
title: Permisos de objeto de modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], model objects
- models [Master Data Services], object permissions
ms.assetid: fab6335b-4cae-47de-ae7c-6c4743e0680f
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 90259662ab909bc6ea47e7be851a9550df9edb86
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48206795"
---
# <a name="model-object-permissions-master-data-services"></a>Permisos de objeto del modelo (Master Data Services)
  Los permisos del objeto de modelo son obligatorios. Determinan los atributos a los que un usuario puede tener acceso en el área funcional del **Explorador** de la interfaz de usuario.  
  
 Por ejemplo, si asigna a un usuario el permiso **Actualizar** para la entidad Product, el usuario puede actualizar todos los atributos de la entidad Product. Si asigna el permiso **Actualizar** a un único atributo, el usuario solo podrá actualizar el atributo.  
  
 Para determinar la seguridad asignada en cada valor de atributo individual, los permisos de objeto de modelo se combinan con los permisos de miembros de jerarquía, que determinan los miembros a los que un usuario puede tener acceso.  
  
 Para conceder a un usuario acceso a un área funcional no sea **Explorer**, el usuario debe ser un administrador de modelo, lo que implica también la asignación de permisos de objeto de modelo. Para obtener más información, vea [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
 Los permisos del objeto de modelo se asignan en la interfaz de usuario de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], en el área funcional **Permisos de grupos y usuarios** de la pestaña **Modelos**. En esta pestaña, el modelo se representa como una estructura de árbol. Cuando asigne un permiso a un objeto en el árbol, todos los objetos subordinados heredan ese permiso. Para invalidar esa herencia asignando el permiso a objetos individuales.  
  
 Puede asignar **de sólo lectura**, **actualización**, o **Deny** permiso a objetos del modelo. Si no asigna permisos en la pestaña **Modelos** , el usuario no podrá ver ningún modelo ni ningún dato en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="best-practice"></a>Práctica recomendada  
 En general, debe asignar **actualización** permiso para el objeto de modelo y, a continuación, asignar explícitamente permisos a objetos subordinados. Si no asigna permisos en objetos subordinados, los permisos se heredan y el usuario es un administrador.  
  
## <a name="see-also"></a>Vea también  
 [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permisos de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-permissions-master-data-services.md)   
 [Permisos del área funcional &#40;Master Data Services&#41;](../../2014/master-data-services/functional-area-permissions-master-data-services.md)   
 [Permisos de miembros de jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [¿Cómo se determinan los permisos &#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
