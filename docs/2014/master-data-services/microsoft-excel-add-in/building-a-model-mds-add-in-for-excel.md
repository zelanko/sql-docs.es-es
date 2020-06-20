---
title: Generar un modelo (complemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8ae26ec3-c5d5-4c4f-a810-2951a7454439
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 74f7e3a13e28b0cd6e9e6e539992e0430f64753f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84961475"
---
# <a name="building-a-model-mds-add-in-for-excel"></a>Generar un modelo (complemento MDS para Excel)
  En [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], los administradores pueden realizar un subconjunto de las funciones administrativas disponibles en la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
 Las tareas de generación de modelos que los administradores pueden realizar en [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] son:  
  
-   Crear entidades. Para obtener más información sobre las entidades, consulte [Entidades &#40;Master Data Services&#41;](../entities-master-data-services.md).  
  
-   Crear atributos de todos los tipos, incluidos los atributos basados en dominios. Para obtener más información sobre los atributos, consulte [Atributos &#40;Master Data Services&#41;](../attributes-master-data-services.md) y [Atributos basados en dominios &#40;Master Data Services&#41;](../domain-based-attributes-master-data-services.md).  
  
 Como administrador, debe crear el modelo con el servicio Web o la aplicación Web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . Puede usar [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] para crear entidades y atributos dentro del modelo. Para obtener más información sobre los objetos de modelo, consulte [Modelos &#40;Master Data Services&#41;](../models-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 La mayoría de las tareas administrativas se deben realizar en la aplicación Web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] o utilizando el servicio Web. En la siguiente tabla se muestran las herramientas que los administradores pueden usar para completar las tareas en MDS.  
  
|Descripción de la tarea|Herramienta|Tema|  
|----------------------|----------|-----------|  
|Crear modelos.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] o aplicación web|[Crear un modelo &#40;Master Data Services&#41;](../create-a-model-master-data-services.md)|  
|Crear una entidad.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicación web, servicio web o [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[Crear una entidad &#40;Complemento MDS para Excel&#41;](create-an-entity-mds-add-in-for-excel.md)|  
|Crear un atributo basado en dominio.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicación web, servicio web o [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[Crear un atributo basado en dominio &#40;complemento MDS para Excel&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|Crear grupos de atributos.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] o aplicación web|[Crear un grupo de atributos &#40;Master Data Services&#41;](../create-an-attribute-group-master-data-services.md)|  
|Crear reglas de negocios.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] o aplicación web|[Crear y publicar una regla de negocios &#40;Master Data Services&#41;](../create-and-publish-a-business-rule-master-data-services.md)|  
|Crear vistas de suscripción.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] o aplicación web|[Cree una vista de suscripciones &#40;Master Data Services&#41;](../create-a-subscription-view-to-export-data-master-data-services.md)|  
|Crear jerarquías.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] o aplicación web|[Crear una jerarquía derivada &#40;Master Data Services&#41;](../create-a-derived-hierarchy-master-data-services.md)<br /><br /> [Crear una jerarquía explícita &#40;Master Data Services&#41;](../create-an-explicit-hierarchy-master-data-services.md)|  
|Crear colecciones.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] o aplicación web|[Crear una colección &#40;Master Data Services&#41;](../create-a-collection-master-data-services.md)|  
|Crear versiones de datos.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] o aplicación web|[Bloquear una versión &#40;Master Data Services&#41;](../lock-a-version-master-data-services.md)|  
|Implementar modelos.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , servicio web o herramienta MDSModelDeploy.|[Crear un paquete de implementación de modelo mediante MDSModelDeploy](../create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Modelos &#40;Master Data Services&#41;](../models-master-data-services.md)  
  
-   [Entidades &#40;Master Data Services&#41;](../entities-master-data-services.md)  
  
-   [Atributos &#40;Master Data Services&#41;](../attributes-master-data-services.md)  
  
-   [Atributos basados en dominios &#40;Master Data Services&#41;](../domain-based-attributes-master-data-services.md)  
  
-   [Grupos de atributos &#40;Master Data Services&#41;](../attribute-groups-master-data-services.md)  
  
-   [Reglas de negocios &#40;Master Data Services&#41;](../business-rules-master-data-services.md)  
  
-   [Exportar datos &#40;Master Data Services&#41;](../overview-exporting-data-master-data-services.md)  
  
-   [Jerarquías &#40;Master Data Services&#41;](../hierarchies-master-data-services.md)  
  
-   [Colecciones &#40;Master Data Services&#41;](../collections-master-data-services.md)  
  
-   [Versiones &#40;Master Data Services&#41;](../versions-master-data-services.md)  
  
-   [Seguridad &#40;Master Data Services&#41;](../security-master-data-services.md)  
  
-   [Implementar modelos &#40;Master Data Services&#41;](../deploying-models-master-data-services.md)  
  
  
