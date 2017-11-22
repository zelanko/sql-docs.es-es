---
title: "Implementar un paquete de implementación de modelo mediante el asistente | Microsoft Docs"
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
- deployment packages [Master Data Services], deploying
- models [Master Data Services], deploying a package
ms.assetid: 4f65dc60-0ff8-46e6-9988-5bc5b9603ad0
caps.latest.revision: "16"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9ceecdbdafa9675ffd78178fee26fa3069fca669
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="deploy-a-model-deployment-package-by-using-the-wizard"></a>Implementar un paquete de implementación de modelo mediante el asistente
  Use el asistente para la implementación de modelos de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para implementar paquetes que solo contengan objetos del modelo. Si necesita implementar un paquete con datos, consulte [Implementar un paquete de implementación de modelo mediante MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
> [!IMPORTANT]  
>  Los paquetes solamente se pueden implementar en la edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en la que se crearon. Esto significa que los paquetes que se hayan creado en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] no se pueden implementar en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Administración del sistema** en el entorno de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] de destino.  
  
-   Debe existir un paquete de implementación de modelo. Para obtener más información, consulte [Crear un paquete de implementación de modelo mediante el asistente](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md).  
  
-   Debe ser administrador en el entorno donde va a implementar el modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-deploy-a-model-deployment-package-of-model-objects-only"></a>Para implementar solo un paquete de implementación de objetos del modelo  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Vista de modelo** , en la barra de menús, seleccione **Sistema** y haga clic en **Implementación**.  
  
3.  En el **Asistente para la implementación de modelos**, haga clic en **Implementar**.  
  
4.  Haga clic en **Examinar**.  
  
5.  Busque el paquete de implementación (archivo .pkg) y haga clic en **Abrir**.  
  
6.  Haga clic en **Siguiente**.  
  
7.  Una vez cargado el paquete, haga clic en **Siguiente**.  
  
8.  Si el modelo ya existe, puede seleccionar **Actualizar el modelo existente**para actualizarlo. Para crear un nuevo modelo, seleccione **Crear un nuevo modelo** y, después de hacer clic en **Siguiente** , puede escribir un nombre para el nuevo modelo.  
  
9. Haga clic en **Finalizar** para salir del asistente.  
  
 **Comentarios:**  
  
-   Si una vista de suscripciones del paquete tiene el mismo nombre que una vista de suscripciones de un modelo existente, se muestra esta advertencia: **se ha cambiado el nombre de la vista de suscripción del implementador**. Además, se crea la vista como *modelname.subscriptionviewname*. Si este nombre ya se está usando, no se crea la vista de suscripciones.  
  
-   El proceso de implementación tiene cuatro pasos:  
  
    1.  Se crean los objetos del modelo.  
  
    2.  Se crean vistas de suscripción.  
  
    3.  Se crean las reglas de negocios.  
  
-   Al crear un modelo nuevo o clonado, si el proceso sufre un error en algún paso, el modelo se elimina.  
  
     Al actualizar un modelo, si el proceso produce un error durante alguno de los tres primeros pasos, no pasa al siguiente paso; sin embargo, los cambios ya realizados no se revierten.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Los atributos de archivo y los permisos de usuario y de grupo no están incluidos en los paquetes de implementación de modelos. Después de implementar un modelo, debe actualizarlos manualmente. Para obtener más información, vea:  
  
-   [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Implementar modelos &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  
