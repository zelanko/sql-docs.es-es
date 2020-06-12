---
title: Ubicación de almacenamiento de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], storage location
ms.assetid: cf88c62e-581e-42f2-846f-a9bf1d7c3292
author: minewiskan
ms.author: owend
ms.openlocfilehash: e904333dc25e7ae58d8eae29ba00279d7e599033
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547107"
---
# <a name="database-storage-location"></a>Ubicación de almacenamiento de las bases de datos
  Con frecuencia se producen situaciones en las que un administrador de bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] desea que una base de datos determinada resida fuera de la carpeta de datos del servidor. Estas situaciones suelen responder a necesidades empresariales, como mejorar el rendimiento o ampliar la capacidad de almacenamiento. En estas situaciones, la `DbStorageLocation` propiedad de base de datos permite al [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DBA especificar la ubicación de la base de datos en un disco local o en un dispositivo de red.  
  
## <a name="dbstoragelocation-database-property"></a>Propiedad de base de datos DbStorageLocation  
 La propiedad de base de datos `DbStorageLocation` especifica la carpeta en la que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea y administra todos los datos y los archivos de metadatos de la base de datos. Todos los archivos de metadatos se almacenan en la carpeta `DbStorageLocation`, con la excepción del archivo de metadatos de la base de datos, que se almacena en la carpeta de datos del servidor. Debe tener en cuenta dos consideraciones importantes al establecer el valor de propiedad de base de datos `DbStorageLocation`:  
  
-   La propiedad de base de datos `DbStorageLocation` se debe establecer en una ruta UNC de carpeta existente o en una cadena vacía. De manera predeterminada, la carpeta de datos del servidor es una cadena vacía. Si la carpeta no existe, se producirá un error al ejecutar un `Create` `Attach` comando, o `Alter` .  
  
-   La propiedad de la base de datos `DbStorageLocation` no se puede establecer para que apunte a la carpeta de datos del servidor ni a ninguna de sus subcarpetas. Si la ubicación apunta a la carpeta de datos del servidor o a cualquiera de sus subcarpetas, se producirá un error al ejecutar un comando `Create`, `Attach` o `Alter`.  
  
> [!IMPORTANT]  
>  Se recomienda que establezca la ruta UNC para utilizar una red SAN, una red basada en iSCSI o un disco local adjunto. Cualquier ruta UNC a un recurso compartido de red o a una solución de almacenamiento remoto de latencia conduce a una instalación no compatible.  
  
### <a name="dbstoragelocation-compared-to-storagelocation"></a>Comparación entre DbStorageLocation y StorageLocation  
 `DbStorageLocation` especifica la carpeta en que residen todos los archivos de datos y de metadatos de la base de datos, mientras que `StorageLocation` especifica la carpeta en que residen una o varias particiones de un cubo. `StorageLocation` se puede establecer independientemente de `DbStorageLocation`. La decisión al respecto la toma el administrador de bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] basándose en los resultados esperados, y muchas veces se usarán ambas propiedades de forma simultánea.  
  
## <a name="dbstoragelocation-usage"></a>Uso de DbStorageLocation  
 La `DbStorageLocation` propiedad de base de datos se usa como parte de un `Create` comando de base de datos en una secuencia de comandos de base de datos `Detach` / `Attach` , en una secuencia de comandos de base de datos `Backup` / `Restore` o en un `Synchronize` comando de base de datos. El cambio de la propiedad de base de datos `DbStorageLocation` se considera un cambio estructural en el objeto de base de datos. Esto significa que deben crearse de nuevo todos los metadatos y volverse a procesar los datos.  
  
> [!IMPORTANT]  
>  No debe cambiar la ubicación de almacenamiento de las bases de datos con un comando `Alter`. En su lugar, se recomienda usar una secuencia de `Detach` / `Attach` comandos de base de datos (vea [movimiento de una base](move-an-analysis-services-database.md)de datos Analysis Services, [adjuntar y separar bases de datos Analysis Services](attach-and-detach-analysis-services-databases.md)).  
  
## <a name="see-also"></a>Consulte también  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Adjuntar y separar bases de datos de Analysis Services](attach-and-detach-analysis-services-databases.md)   
 [Traslado de una base de datos de Analysis Services](move-an-analysis-services-database.md)   
 [Elemento DbStorageLocation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)   
 [Elemento Create &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)   
 [Elemento Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Elemento Synchronize &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)  
  
  
