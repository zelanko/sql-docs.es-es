---
title: Permisos de objeto de modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], model objects
- models [Master Data Services], object permissions
ms.assetid: fab6335b-4cae-47de-ae7c-6c4743e0680f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 754920cac0a832ac5ae1ff8959e710815d68fd70
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971195"
---
# <a name="model-object-permissions-master-data-services"></a>Permisos de objeto del modelo (Master Data Services)
  Los permisos del objeto de modelo son obligatorios. Determinan los atributos a los que un usuario puede tener acceso en el área funcional del **Explorador** de la interfaz de usuario.  
  
 Por ejemplo, si asigna a un usuario el permiso **Actualizar** para la entidad Product, el usuario puede actualizar todos los atributos de la entidad Product. Si asigna el permiso **Actualizar** a un único atributo, el usuario solo podrá actualizar el atributo.  
  
 Para determinar la seguridad asignada en cada valor de atributo individual, los permisos de objeto de modelo se combinan con los permisos de miembros de jerarquía, que determinan los miembros a los que un usuario puede tener acceso.  
  
 Para conceder a un usuario acceso a un área funcional que no sea el **Explorador**, el usuario debe ser un administrador del modelo, lo que implica también la asignación de permisos de objeto de modelo. Para obtener más información, vea [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
 Los permisos del objeto de modelo se asignan en la [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] interfaz de usuario (UI), en el área funcional **permisos de usuario y de grupo** de la pestaña **modelos** . En esta pestaña, el modelo se representa como una estructura de árbol. Cuando asigne un permiso a un objeto en el árbol, todos los objetos subordinados heredan ese permiso. Para invalidar esa herencia asignando el permiso a objetos individuales.  
  
 Puede asignar el permiso de **solo lectura**, **Actualizar**o **denegar** a los objetos de modelo. Si no asigna permisos en la pestaña **Modelos** , el usuario no podrá ver ningún modelo ni ningún dato en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="best-practice"></a>Procedimiento recomendado  
 En general, debe asignar el permiso **Actualizar** al objeto de modelo y, a continuación, asignar explícitamente el permiso a los objetos situados debajo de. Si no asigna permisos en objetos subordinados, los permisos se heredan y el usuario es un administrador.  
  
## <a name="see-also"></a>Consulte también  
 [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permisos de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-permissions-master-data-services.md)   
 [&#40;Master Data Services permisos de área funcional&#41;](../../2014/master-data-services/functional-area-permissions-master-data-services.md)   
 [Permisos de miembros de la jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Cómo se determinan los permisos &#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
