---
title: Crear un paquete de implementación de modelo mediante MDSModelDeploy | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: c2687e39-dc20-494f-a707-2aa29f4c329e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 37c7d590b58c5591a7ce441e8b9a3f202454f3f3
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65487402"
---
# <a name="create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>Crear un paquete de implementación de modelo mediante MDSModelDeploy

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], utilice la herramienta MDSModelDeploy para crear un paquete. Dependiendo de los comandos que especifique, el paquete puede contener:  
  
-   Solo objetos de modelo.  
  
-   Objetos de modelo y datos.  
  
 Si desea implementar un paquete que solo contiene objetos de modelo, puede usar en su lugar el Asistente para la implementación de modelos en la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Para obtener más información, consulte [Crear un paquete de implementación de modelo mediante el asistente](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md).  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
1.  Los permisos básicos necesarios para ejecutar la herramienta de MDSModelDeploy son los siguientes:  
  
    -   El mismo permiso de Windows que para el administrador de configuración de MDS (administrador de Windows)  
  
    -   Permiso DBA en la base de datos de MDS.  
  
2.  Los permisos necesarios para crear el paquete mediante la herramienta MDSModelDeploy son los siguientes:  
  
    -   Permiso de administrador de modelo MDS en el modelo de datos.  
  
    -   Permiso de área funcional ImportExport de MDS.  
  
3.  Los permisos necesarios para implementar un modelo mediante la herramienta MDSModelDeploy son los siguientes:  
  
    -   Permiso de la función de explorador de MDS  
  
    -   Permiso de la función de administración del sistema de MDS.  
  
4.  Los permisos necesarios para mostrar modelos mediante la herramienta MDSModelDeploy son los siguientes:  
  
    -   Permiso de la función de explorador de MDS  
  
    -   Permiso de administrador de modelos de MDS en el modelo de datos en orden para ver el modelo en la lista.  
  
 Debe existir un modelo para que se pueda crear un paquete del mismo. Para obtener más información, consulte [Crear un modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md).  
  
 Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>Para crear un paquete de implementación de modelo mediante MDSModelDeploy  
  
1.  Abra un símbolo del sistema de administrador.  
  
2.  Navegue a la ubicación de MDSModelDeploy.exe.  
  
    -   Si MDS se ha instalado en la ubicación predeterminada, el archivo se encuentra en *unidad*:\Archivos de programa\Microsoft SQL Server\130\Master Data Services\Configuration.  
  
    -   Si MDS no se instaló en la ubicación predeterminada, busque en el equipo local MDSModelDeploy.exe.  
  
3.  Opcional. Vea las opciones y la Ayuda.  
  
    -   Para mostrar todas las opciones disponibles, escriba `MDSModelDeploy` y presione Entrar.  
  
    -   Para mostrar la ayuda de una opción, escriba lo siguiente, donde *OptionName* es el nombre de la opción: `MDSModelDeploy help OptionName`.  
  
4.  Opcional. Si tiene varias aplicaciones web, determine el nombre del servicio en el que vaya a hacer las implementaciones; para ello, escriba este comando y presione ENTRAR:  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     Se devuelve una lista de valores, por ejemplo `MDS1, Default Web Site, MDS`. El primer valor de esta lista (en este caso, `MDS1`) es necesario para implementar el modelo.  
  
5.  Para crear un paquete que contenga objetos de modelo y datos, escriba lo siguiente, donde *ModelName*, *VersionName*, *ServiceName*y *PackageName* son los nombres del modelo, la versión, el servicio y el archivo de salida .pkg, respectivamente:  
  
    ```  
    MDSModelDeploy createpackage -model ModelName -version VersionName -service ServiceName -package PackageName -includedata  
    ```  
  
     Si no desea incluir datos, no utilice los modificadores `-version` y `-includedata` .  
  
6.  Presione ENTRAR. Cuando el paquete se crea correctamente, se muestra un mensaje que indica que "la operación de MDSModelDeploy se ha completado correctamente".  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Implementar un paquete de implementación de modelo mediante MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
## <a name="see-also"></a>Vea también  
 [Opciones de la implementación de modelos &#40;Master Data Services&#41;](../master-data-services/model-deployment-options-master-data-services.md)   
 [Implementar modelos &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  
