---
title: Implementar un paquete de implementación de modelo mediante MDSModelDeploy | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fb2a4df4-5e0d-4b34-818f-383dbde1b15c
caps.latest.revision: 16
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 2d4a77889ad5042349fc4fd9e1e6ff20379a5384
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-a-model-deployment-package-by-using-mdsmodeldeploy"></a>Implementar un paquete de implementación de modelo mediante MDSModelDeploy

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], utilice la herramienta MDSModelDeploy para implementar un paquete que contiene:  
  
-   Solo objetos de modelo.  
  
-   Objetos de modelo y datos.  
  
 Si desea implementar un paquete que solo contiene objetos de modelo, puede usar en su lugar el Asistente para la implementación de modelos en la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Para más información, consulte [Deploy a Model Deployment Package by Using the Wizard](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md).  
  
> [!IMPORTANT]  
>  Los paquetes solamente se pueden implementar en la edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en la que se crearon. Esto significa que los paquetes que se hayan creado en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] no se pueden implementar en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] o posterior.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Administración del sistema** en el entorno de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] de destino.  
  
-   Debe existir un paquete de implementación de modelo. Para más información, consulte  [Create a Model Deployment Package by Using MDSModelDeploy](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
-   Debe ser administrador en el entorno donde va a implementar el modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Si va a actualizar un modelo con datos, la versión que vaya a implementar no puede tener los valores **Bloqueado** o **Confirmado**.  
  
### <a name="to-deploy-a-model-deployment-package"></a>Para implementar un paquete de implementación de modelos  
  
1.  Determine si está implementando un nuevo modelo, un clon de un modelo o actualizando un modelo clonado anteriormente. Para obtener más información, consulte [Opciones de la implementación de modelos &#40;Master Data Services&#41;](../master-data-services/model-deployment-options-master-data-services.md).  
  
2.  Abra un símbolo del sistema de administrador y navegue a MDSModelDeploy.exe.  
  
    -   Si MDS se ha instalado en la ubicación predeterminada, la herramienta está disponible en *unidad*:\Archivos de programa\Microsoft SQL Server\130\Master Data Services\Configuration  
  
    -   Si MDS no se ha instalado en la ubicación predeterminada, busque en el equipo local MDSModelDeploy.exe.  
  
3.  Opcional. Vea las opciones y la Ayuda.  
  
    -   Para mostrar todas las opciones disponibles, escriba `MDSModelDeploy` y presione Entrar.  
  
    -   Para mostrar la ayuda de una opción, escriba lo siguiente, donde *OptionName* es el nombre de la opción: `MDSModelDeploy help OptionName`.  
  
4.  Opcional. Si tiene varias aplicaciones web, determine el nombre del servicio en el que vaya a hacer las implementaciones; para ello, escriba este comando y presione ENTRAR:  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     Se devuelve una lista de valores, por ejemplo `MDS1, Default Web Site, MDS`. El primer valor de esta lista (en este caso, `MDS1`) es necesario para implementar el modelo.  
  
5.  Dependiendo de si se crea un modelo, se clona un modelo o se actualiza un modelo, en el símbolo del sistema, escriba lo siguiente y presione Entrar.  
  
    -   Para crear un modelo:  
  
        ```  
        MDSModelDeploy deploynew -package PackageName -model ModelName -service ServiceName  
        ```  
  
    -   Para crear un clon de un modelo:  
  
        ```  
        MDSModelDeploy deployclone -package PackageName  
        ```  
  
    -   Para actualizar un modelo existente y sus datos:  
  
        ```  
        MDSModelDeploy deployupdate -package PackageName -version VersionName  
        ```  
  
    > [!IMPORTANT]  
    >  Si usa la herramienta MDSModelDeploy para actualizar un modelo existente y sus datos, y el paquete no contiene una entidad, un atributo o un miembro que exista en el modelo de destino, MDSModelDeploy no eliminará dicha entidad, atributo o miembro del modelo.  
  
     Donde *PackageName* es el nombre del archivo de paquete (.pkg), *ModelName* es el nombre del nuevo modelo, *VersionName* es el nombre de la versión y *ServiceName* es el nombre del servicio devuelto en el paso anterior. Asegúrese de que los nombres del modelo y de la versión se correspondan exactamente con los nombres con distinción de mayúsculas y minúsculas.  
  
6.  Cuando el paquete se implementa correctamente, se muestra un mensaje que indica que “la operación de MDSModelDeploy se completó correctamente”.  
  
 **Notas:**  
  
-   Si una vista de suscripciones del paquete tiene el mismo nombre que una vista de suscripciones de un modelo existente, esta advertencia se muestra como que **se ha cambiado el nombre de la vista de suscripción del implementador** y la vista se crea como *modelname.subscriptionviewname*. Si este nombre ya se está usando, no se crea la vista de suscripciones.  
  
-   El proceso de implementación tiene cuatro pasos:  
  
    1.  Se crean los objetos del modelo.  
  
    2.  Se crean las reglas de negocios.  
  
    3.  Se crean vistas de suscripción.  
  
    4.  Se rellenan los datos maestros.  
  
-   Al crear un modelo nuevo o clonado, si el proceso sufre un error en algún paso, el modelo se elimina.  
  
     Al actualizar un modelo, si el proceso sufre un error durante los tres primeros pasos, no continúa; sin embargo, los cambios ya realizados no se revierten. Si el proceso sufre un error en el paso 4, los miembros que se pueden actualizar se actualizan.  
  
## <a name="next-steps"></a>Next Steps  
 Los atributos de archivo y los permisos de usuario y de grupo no están incluidos en los paquetes de implementación de modelos. Después de implementar un modelo, debe actualizarlos manualmente. Para obtener más información, vea:  
  
-   [Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>Ver también  
 [Implementar modelos &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  
