---
title: Modelos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], about models
- models [Master Data Services]
ms.assetid: 9f862a3d-25ab-41e9-b833-1db99959e825
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d202c04a41553b934c175edb7c0afcd907e846e5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65482547"
---
# <a name="models-master-data-services"></a>Modelos (Master Data Services)
  Los modelos son el nivel superior de organización de datos en [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Un modelo define la estructura de datos de la solución de administración de datos maestros. Un modelo contiene los siguientes objetos:  
  
-   Entidades  
  
-   Atributos y grupos de atributos  
  
-   Jerarquías derivadas y explícitas  
  
-   Colecciones  
  
 Los modelos organizan la estructura de los datos maestros. Su implementación de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] puede tener uno o varios modelos que agrupan tipos de datos similares. En general, los datos maestros se pueden clasificar en una de estas cuatro categorías: personas, lugares, cosas o conceptos. Por ejemplo, puede crear un modelo Producto que vaya a contener datos relacionados con productos o un modelo Cliente para que contenga datos relacionados con clientes.  
  
 Puede asignar a usuarios y grupos el permiso para ver y actualizar los objetos dentro del modelo. Si no concede permisos al modelo, no se mostrará.  
  
 En un momento determinado, podrá crear copias de los datos maestros dentro de un modelo. Estas copias se denominan versiones.  
  
 Una vez haya definido un modelo en un entorno de prueba, puede implementarlo, con o sin los datos correspondientes, desde el entorno de prueba hasta un entorno de producción. Esto elimina la necesidad de volver a crear los modelos en el entorno de producción.  
  
## <a name="how-models-relate-to-other-objects"></a>Cómo se relacionan los modelos con otros objetos  
 Un modelo contiene entidades. Las entidades contienen atributos, jerarquías explícitas y colecciones. Los atributos pueden estar contenidos en grupos de atributos. Los atributos basados en dominios existen cuando se usa una entidad como atributo para otra entidad.  
  
 Esta imagen muestra las relaciones existentes entre los objetos de un modelo.  
  
 ![Objetos de un modelo de Master Data Services](../../2014/master-data-services/media/mds-conc-model-circles.gif "Objetos de un modelo de Master Data Services")  
  
> [!NOTE]  
>  Las jerarquías derivadas también son objetos de modelo, pero no se muestran en la imagen. Las jerarquías derivadas se derivan de las relaciones de atributo basadas en dominios que existen entre las entidades. Vea [Jerarquías derivadas &#40;Master Data Services&#41;](derived-hierarchies-master-data-services.md) para más información.  
  
 Los datos maestros son los datos contenidos en los objetos de modelo. En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], los datos maestros se almacenan como miembros de una entidad.  
  
 Los objetos de modelo se mantienen en el área funcional de **Administración del sistema** de la interfaz de usuario de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
## <a name="model-example"></a>Ejemplo de modelo  
 En el ejemplo siguiente, los objetos del modelo Product agrupan lógicamente los datos relacionados con los productos.  
  
 ![Ejemplo de datos maestros de modelo de producto](../../2014/master-data-services/media/mds-conc-model.gif "Ejemplo de datos maestros de modelo de producto")  
  
 Otros modelos comunes son:  
  
-   Accounts: podrían incluir entidades como cuentas de balance, cuentas de balance de resultados, estadísticas y tipos de cuenta.  
  
-   Customer: podría incluir entidades como género, educación, ocupación y estado civil.  
  
-   Geography: podría incluir entidades como códigos postales, ciudades, municipios, estados, provincias, regiones, territorios, países y continentes.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear un modelo para organizar los datos maestros.|[Crear un modelo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-model-master-data-services.md)|  
|Cambiar el nombre de un modelo existente.|[Cambiar el nombre de un modelo &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-model-name-master-data-services.md)|  
|Eliminar un modelo existente.|[Eliminar un modelo &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-model-master-data-services.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Introducción a Master Data Services](master-data-services-overview-mds.md)  
  
-   [Entidades &#40;Master Data Services&#41;](../../2014/master-data-services/entities-master-data-services.md)  
  
-   [Atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
-   [Implementar modelos &#40;Master Data Services&#41;](../../2014/master-data-services/deploying-models-master-data-services.md)  
  
-   [Permisos de objeto del modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)  
  
  
