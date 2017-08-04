---
title: "Ejemplos SQL Server: Modelo de implementación de paquetes (MDS) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- master data services
- sample
ms.assetid: 9b31b7b6-319b-4840-b67d-eb383e7762b1
caps.latest.revision: 21
author: sabotta
ms.author: carlasab
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d7a031ba18c6782cdd73ae31ef395bc2ecdcf102
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="sql-server-examples-model-deployment-packages-mds"></a>Ejemplos SQL Server: Paquetes de implementación de modelos (MDS)
  Los paquetes de modelo de ejemplo con datos se incluyen al instalar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. La ubicación predeterminada de estos archivos de paquetes es \<unidad > \Program SQL Server\130\Master Data Services\Samples\Packages.  
  
 Para obtener instrucciones sobre cómo implementar los paquetes de modelo de ejemplo, consulte [Implementar modelos y datos de ejemplo](../master-data-services/master-data-services-installation-and-configuration.md#deploySample). Implemente los paquetes de modelo de ejemplo con la [herramienta MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
> [!IMPORTANT]  
>  **Actualizaciones de ejemplo en[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**  
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
 

 
 En Master Data Services, un paquete es un archivo XML que contiene una estructura del modelo implementable y, si lo desea, los datos del modelo. Use los paquetes del modelo para mover las copias de modelos desde un entorno de MDS a otro, o para crear nuevos modelos en el entorno de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] existente.  
  
## <a name="see-also"></a>Vea también  
 [Implementar un paquete de implementación de modelo mediante MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  

