---
title: Exportar datos (Master Data Services) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- exporting data [Master Data Services]
- subscription views [Master Data Services]
- subscription views [Master Data Services], about subscription views
ms.assetid: 8b74409a-ea70-45f8-84c7-da6905e4901a
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 656578a35e70b8371056330e0edec69073816687
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111584"
---
# <a name="exporting-data-master-data-services"></a>Exportar datos (Master Data Services)
  Puede exportar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] datos a sistemas de suscripción creando vistas de suscripciones. Cualquier sistema de suscripción podrá ver los datos publicados en la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Para obtener más información sobre las vistas, consulte [Vistas](../relational-databases/views/views.md).  
  
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
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear una vista de suscripción de los datos maestros.|[Crear una vista de suscripción &#40;Master Data Services&#41;](create-a-subscription-view-to-export-data-master-data-services.md)|  
|Eliminar una vista de suscripción existente.|[Eliminar una vista de suscripción &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-subscription-view-master-data-services.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Formatos de vista de suscripción &#40;Master Data Services&#41;](../../2014/master-data-services/subscription-view-formats-master-data-services.md)  
  
-   [Vistas](../relational-databases/views/views.md)  
  
  