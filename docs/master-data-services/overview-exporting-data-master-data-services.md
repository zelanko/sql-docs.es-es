---
title: "Información general: Exportar datos (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exporting data [Master Data Services]
- subscription views [Master Data Services]
- subscription views [Master Data Services], about subscription views
ms.assetid: 8b74409a-ea70-45f8-84c7-da6905e4901a
caps.latest.revision: "12"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd6016f2daf818d5a7038925c77eaaff91789f8b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="overview-exporting-data-master-data-services"></a>Información general: exportar datos (Master Data Services)
  En este artículo se presentan los tipos de formatos de vistas de suscripciones y cómo determinar cuándo hay que editar las vistas debido a cambios en los objetos del modelo.  
  
 Cree una vista de suscripciones para exportar datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a un sistema de suscripción como [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Use el sistema de suscripción para ver los datos de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  Para obtener información sobre cómo crear la vista de suscripciones, consulte [Crear una vista de suscripciones para exportar datos &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)  
  
 Para obtener más información sobre las vistas, consulte [Vistas](../relational-databases/views/views.md).  
  
## <a name="subscription-view-formats"></a>Formatos de vista de suscripciones  
 Al crear una vista en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], elige entre un conjunto de formatos de vistas estándar proporcionados por [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Puede utilizar estos formatos para crear vistas que muestren:  
  
-   Todos los miembros hoja y sus atributos.  
  
-   Todos los miembros consolidados y sus atributos.  
  
-   Todas las colecciones y sus atributos.  
  
-   Los miembros agregados explícitamente a una colección.  
  
-   Los miembros de una jerarquía derivada, en formato de nivel o de elemento secundario primario.  
  
-   Los miembros de todas las jerarquías explícitas de una entidad, en formato de nivel o de elemento secundario primario.  
  
## <a name="subscription-views-can-become-out-of-date"></a>Las vistas de suscripción pueden quedarse obsoletas  
 Después de crear una vista de suscripción para una entidad o una jerarquía, los cambios en los objetos de modelo asociados no se reflejan automáticamente en la vista. Puede que también necesite volver a generar una vista de suscripción en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para reflejar los cambios en los objetos de modelo. La columna **Cambiado** en la página **Exportar** se actualiza a **True** cuando los objetos de modelo cambian. **True** indica que debería modificar la vista de suscripción y guardarla, con lo que la vista se regenera.  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear una vista de suscripción de los datos maestros.|[Crear una vista de suscripciones para exportar datos &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|Eliminar una vista de suscripción existente.|[Eliminar una vista de suscripciones &#40;Master Data Services&#41;](../master-data-services/delete-a-subscription-view-master-data-services.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Formatos de vista de suscripciones &#40;Master Data Services&#41;](../master-data-services/subscription-view-formats-master-data-services.md)  
  
-   [Vistas](../relational-databases/views/views.md)  
  
  
