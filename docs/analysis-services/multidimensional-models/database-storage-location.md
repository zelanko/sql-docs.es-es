---
title: "Ubicación de almacenamiento de base de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [Analysis Services], storage location
ms.assetid: cf88c62e-581e-42f2-846f-a9bf1d7c3292
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fb6c9aa4728cf355d0c974501fc36fd71a233a83
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="database-storage-location"></a>Ubicación de almacenamiento de las bases de datos
  Con frecuencia se producen situaciones en las que un administrador de bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] desea que una base de datos determinada resida fuera de la carpeta de datos del servidor. Estas situaciones suelen responder a necesidades empresariales, como mejorar el rendimiento o ampliar la capacidad de almacenamiento. Para estas situaciones, la propiedad de base de datos **DbStorageLocation** permite al administrador de bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificar la ubicación de la base de datos en un disco local o un dispositivo de red.  
  
## <a name="dbstoragelocation-database-property"></a>Propiedad de base de datos DbStorageLocation  
 La propiedad de base de datos **DbStorageLocation** especifica la carpeta en la que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea y administra todos los datos y los archivos de metadatos de la base de datos. Todos los archivos de metadatos se almacenan en la carpeta **DbStorageLocation** , con la excepción del archivo de metadatos de la base de datos, que se almacena en la carpeta de datos del servidor. Debe tener en cuenta dos consideraciones importantes al establecer el valor de propiedad de base de datos **DbStorageLocation** :  
  
-   La propiedad de base de datos **DbStorageLocation** se debe establecer en una ruta UNC de carpeta existente o en una cadena vacía. De manera predeterminada, la carpeta de datos del servidor es una cadena vacía. Si la carpeta no existe, se producirá un error al ejecutar un comando **Create**, **Attach**o **Alter** .  
  
-   La propiedad de la base de datos **DbStorageLocation** no se puede establecer para que apunte a la carpeta de datos del servidor ni a ninguna de sus subcarpetas. Si la ubicación apunta a la carpeta de datos del servidor o a cualquiera de sus subcarpetas, se producirá un error al ejecutar un comando **Create**, **Attach**o **Alter** .  
  
> [!IMPORTANT]  
>  Se recomienda que establezca la ruta UNC para utilizar una red SAN, una red basada en iSCSI o un disco local adjunto. Cualquier ruta UNC a un recurso compartido de red o a una solución de almacenamiento remoto de latencia conduce a una instalación no compatible.  
  
### <a name="dbstoragelocation-compared-to-storagelocation"></a>Comparación entre DbStorageLocation y StorageLocation  
 **DbStorageLocation** especifica la carpeta en que residen todos los archivos de datos y de metadatos de la base de datos, mientras que **StorageLocation** especifica la carpeta en que residen una o varias particiones de un cubo. **StorageLocation** se puede establecer independientemente de **DbStorageLocation**. La decisión al respecto la toma el administrador de bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] basándose en los resultados esperados, y muchas veces se usarán ambas propiedades de forma simultánea.  
  
## <a name="dbstoragelocation-usage"></a>Uso de DbStorageLocation  
 La propiedad de base de datos **DbStorageLocation** se usa como parte de un comando de base de datos **Create** en una secuencia de comandos de base de datos **Detach**/**Attach** , en una secuencia de comandos de base de datos **Backup**/**Restore** o en un comando de base de datos **Synchronize** . El cambio de la propiedad de base de datos **DbStorageLocation** se considera un cambio estructural en el objeto de base de datos. Esto significa que deben crearse de nuevo todos los metadatos y volverse a procesar los datos.  
  
> [!IMPORTANT]  
>  No debe cambiar la ubicación de almacenamiento de las bases de datos con un comando **Alter** . En su lugar, se recomienda que use una secuencia de comandos de base de datos **Detach**/**Attach** (vea [Mover una base de datos de Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)y [Adjuntar y separar bases de datos de Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)).  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Adjuntar y separar bases de datos de Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Mover una base de datos de Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Elemento DbStorageLocation](../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)   
 [Crear elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)   
 [Elemento Attach](../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Sincronizar el elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)  
  
  

