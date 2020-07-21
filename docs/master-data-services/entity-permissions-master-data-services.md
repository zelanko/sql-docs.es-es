---
title: Permisos de entidad
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], permissions
- permissions [Master Data Services], entities
ms.assetid: 22785062-4faf-46ee-bffa-01cbd6d5a5b3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 3a0ca2773d513137adeb9e803b66930536e3a28a
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85811957"
---
# <a name="entity-permissions-master-data-services"></a>Permisos de entidad (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Los permisos de entidad se aplican a:  
  
-   Todos los atributos de la entidad, incluidos **Nombre** y **Código**, para los miembros hoja y consolidados.  
  
-   Todas las colecciones de la entidad.  
  
-   Pertenencia y relaciones de jerarquía explícita.  
  
 Cuando disponga de permisos para una entidad, podrá agregar y quitar miembros de la misma, de sus jerarquías explícitas y de sus colecciones.  
  
> [!NOTE]  
>  Estos permisos solo se aplican al área funcional del **Explorador** de la interfaz de usuario.  
  
|Permiso|Descripción|  
|----------------|-----------------|  
|**Lectura**|El usuario puede leer miembros, atributos, pertenencias a la jerarquía o pertenencias a la colección.|  
|**Creación**|El usuario puede crear miembros hoja y asignar valores de atributo durante la creación.|  
|**Update**|El usuario puede actualizar miembros, atributos, pertenencias a la jerarquía o pertenencias a la colección.|  
|**Eliminar**|El usuario puede eliminar miembros.|  
|**Deny**|Denegar todo acceso a la entidad.|  
  
 Los permisos de lectura, creación, actualización y eliminación se pueden combinar. Cuando se asignan permisos de Crear, Actualizar y Eliminar, el permiso de lectura se asigna automáticamente.  
  
## <a name="see-also"></a>Consulte también  
 [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permisos del objeto de modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Entidades &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  
