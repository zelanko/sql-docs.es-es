---
title: "Opciones de la implementación de modelos (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf1b17b4-47d5-4eba-83f9-fb0555806867
caps.latest.revision: "6"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f7d6a35f51ae80dea9ddc8ff87de5d38b499b82
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="model-deployment-options-master-data-services"></a>Opciones de la implementación de modelos (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], al implementar un archivo de modelo del paquete, debe decidir si implementar un modelo nuevo o clonado, o actualizar un modelo que se clonó previamente.  
  
## <a name="workflows"></a>Flujos de trabajo  
 Al trabajar con paquetes de modelos, hay dos flujos de trabajo principales.  
  
-   Cree un paquete de un modelo en un entorno de pruebas e implemente un clon del modelo en un entorno de producción. Con el tiempo, implemente las actualizaciones del entorno de prueba en el entorno de producción.  
  
-   Cree un paquete de un modelo e impleméntelo como modelo en el mismo entorno. En este caso, debe proporcionar al modelo un nuevo nombre.  
  
## <a name="options"></a>Opciones  
 En la base de datos MDS, cada objeto de modelo tiene un identificador único (ID). Estos identificadores se incluyen en los paquetes de implementación de modelos. Al implementar el paquete, debe elegir qué hacer con estos identificadores.  
  
 La tabla siguiente puede ayudarle a determinar qué opción realizar cuando implemente un modelo usando el Asistente para la implementación de modelo de administración del sistema o la herramienta MDSModelDeploy.  
  
|Opción|Description|Notas|  
|------------|-----------------|-----------|  
|Nuevo|Cree un nuevo modelo con un nombre único. Se crean identificadores nuevos para todos los objetos del modelo.|Si crea un nuevo modelo con identificadores nuevos, no puede usar las herramientas de implementación de modelos para aplicar las actualizaciones al modelo posteriormente. Cuando utilice el asistente en la aplicación web para implementar un paquete de modelo, tiene la opción de crear un modelo nuevo solo si existe un modelo con el mismo nombre o identificador previamente.|  
|Clonar|Cree un nuevo modelo que es un clon exacto del modelo del paquete. Esto solo funciona si el modelo no existe (por nombre o identificador) en el entorno de destino. Use “clonar” si desea tener el mismo modelo en varios entornos y actualizar el modelo clonado a lo largo del tiempo.|Este es el comportamiento predeterminado del asistente en la aplicación web. Si aún existe un modelo con el mismo nombre o identificador, se le preguntará si desea crear un nuevo modelo en su lugar.|  
|Update|Actualizar un modelo existente con el modelo del paquete. Los identificadores deben ser iguales en ambos modelos. Se utiliza para actualizar un modelo que se clonó previamente.|Puede actualizar solo los modelos que se clonaron previamente. (Los nombres e identificadores deben coincidir).|  
  
## <a name="see-also"></a>Vea también  
 [Implementar un paquete de implementación de modelo mediante MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)   
 [Implementar un paquete de implementación de modelo mediante el asistente](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)   
 [Implementar modelos &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  
