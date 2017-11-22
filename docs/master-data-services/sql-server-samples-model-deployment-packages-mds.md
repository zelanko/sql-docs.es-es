---
title: "Ejemplos de SQL Server: paquetes de implementación de modelos (MDS) | Microsoft Docs"
ms.custom: 
ms.date: 07/28/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- master data services
- sample
ms.assetid: 9b31b7b6-319b-4840-b67d-eb383e7762b1
caps.latest.revision: "21"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: acad2611056a873b3220c90862fd7ef4a158214b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sql-server-examples-model-deployment-packages-mds"></a>Ejemplos de SQL Server: paquetes de implementación de modelos (MDS)
  Los paquetes de modelo de ejemplo con datos se incluyen al instalar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. La ubicación predeterminada de estos archivos de paquete es \<unidad>\Archivos de programa\Microsoft SQL Server\130\Master Data Services\Samples\Packages.  
  
 Para obtener instrucciones sobre cómo implementar los paquetes de modelo de ejemplo, consulte [Implementar modelos y datos de ejemplo](../master-data-services/master-data-services-installation-and-configuration.md#deploySample). Implemente los paquetes de modelo de ejemplo con la [herramienta MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
> [!IMPORTANT]  
>  **Actualizaciones de ejemplo en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**  
>   
>  Los paquetes de ejemplo se han actualizado para admitir las siguientes funcionalidades nuevas.  
>   
>  -   Mostrar relaciones de varios a varios.  
>   
>      Para obtener más información, consulte [Relación de M2M en el modelo de ejemplo](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md#M2MSample).  

> -   Restringir valores permitidos para atributos basados en dominio  
>   
>      Para obtener más información, consulte [Crear un atributo basado en dominio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md).  
> -   Solicitar aprobación para los cambios de la entidad.  
>   
>      Para obtener más información, consulte [Aprobación necesaria &#40;Master Data Services&#41;](../master-data-services/approval-required-master-data-services.md).  
> -   Usar los operadores Not y Else en reglas de negocios  
>   
>      Para obtener más información, consulte [Ejemplos de reglas de negocios](../master-data-services/business-rule-examples-master-data-services.md).  
> -   Implementar índice personalizado  
>   
>      Para obtener más información, consulte [Índice personalizado &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md).  
 

 
 En Master Data Services, un paquete es un archivo XML que contiene una estructura del modelo implementable y, opcionalmente, los datos del modelo. Use los paquetes del modelo para mover las copias de modelos desde un entorno de MDS a otro, o para crear nuevos modelos en el entorno de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] existente.  
  
## <a name="see-also"></a>Vea también  
 [Implementar un paquete de implementación de modelo mediante MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  
