---
description: Permisos de colección (Master Data Services)
title: Permisos de colección
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services], permissions
- permissions [Master Data Services], collections
ms.assetid: 703e1bf5-4b4b-4830-8a5b-f979b09f677d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 04ffb34b92aa43c521a9a454a8068e74cf4fd615
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88390291"
---
# <a name="collection-permissions-master-data-services"></a>Permisos de colección (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Los permisos de colección se aplican a todas las colecciones de una entidad. No puede conceder permisos a una colección específica; los permisos se aplican a todas las colecciones.  
  
> [!NOTE]  
>  Estos permisos solo se aplican al área funcional del **Explorador** de la interfaz de usuario.  
  
|Permiso|Descripción|  
|----------------|-----------------|  
|**Lectura**|El usuario puede leer los miembros de las colecciones y los atributos de los miembros.|  
|**Crear**|El usuario puede crear miembros de colecciones y asignar valores de atributos.|  
|**Actualizar**|El usuario puede actualizar los miembros de las colecciones, así como los atributos y relaciones.|  
|**Eliminar**|El usuario puede eliminar miembros de colecciones.|  
|**Deny**|Denegar todo el acceso a los miembros de las colecciones.|  
  
 Los permisos de lectura, creación, actualización y eliminación se pueden combinar. Cuando se asignan Crear, Actualizar y Eliminar, el permiso de lectura se asigna automáticamente.  
  
## <a name="see-also"></a>Consulte también  
 [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Colecciones &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)   
 [Permisos de objeto del modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)  
  
  
