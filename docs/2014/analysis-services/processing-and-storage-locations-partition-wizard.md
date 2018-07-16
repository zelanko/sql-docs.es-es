---
title: Ubicaciones de procesamiento y almacenamiento (Asistente para particiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.specifyprocessingandstorage.f1
ms.assetid: dda2dc57-923d-4db9-93a7-38e95770f3df
caps.latest.revision: 24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eae2e7c380b7b0de69047079edac87d273f07d52
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286061"
---
# <a name="processing-and-storage-locations-partition-wizard"></a>Ubicaciones de procesamiento y almacenamiento (Asistente para particiones)
  Use la página **Ubicaciones de procesamiento y almacenamiento** para especificar la instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] del cubo propietario de la partición, así como la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que almacena los datos para la partición. Puede definir una partición como remota si especifica una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] remota o una ubicación de almacenamiento distinta de la ubicación de almacenamiento predeterminada. Para más información sobre las particiones remotas, vea [Particiones remotas](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md).  
  
## <a name="processing-location-options"></a>Opciones de ubicación de procesamiento  
 **Instancia del servidor actual**  
 Hace a la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] actual responsable de procesar la partición.  
  
 **Origen de datos de Analysis Services remoto**  
 Convierte a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] remota responsable de procesar esta partición.  
  
 En la lista desplegable, seleccione el origen de datos que representa la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] remota responsable de procesar la partición.  
  
> [!NOTE]  
>  Se producirá un error si selecciona un origen de datos en el que la propiedad de la cadena de conexión del `Initial Catalog` no está definida para una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] válida, o si la base de datos especificada en la propiedad de la cadena de conexión del `Initial Catalog` no admite particiones remotas (en otras palabras, la propiedad `MasterDatasourceID` de la base de datos especificada no se ha configurado con un valor válido).  
  
 **Nueva**  
 Crea un nuevo origen de datos que representa la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] remota responsable de procesar la partición.  
  
## <a name="storage-location-options"></a>Opciones de ubicación de almacenamiento  
 **Ubicación predeterminada del servidor**  
 Convierte la carpeta de datos de la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] actual en la ubicación de almacenamiento de los datos de indización y agregación de la partición.  
  
 **Carpeta especificada**  
 Especifica la ubicación de almacenamiento de los datos de agregación e indización de la partición.  
  
 **...**  
 Muestra el cuadro de diálogo **Buscar carpeta remota** en el que se puede seleccionar una carpeta para **Carpeta especificada**.  
  
## <a name="see-also"></a>Vea también  
 [Partición de la Ayuda F1 del Asistente para &#40;Analysis Services - datos multidimensionales&#41;](partition-wizard-f1-help-analysis-services-multidimensional-data.md)   
 [Las particiones &#40;Analysis Services - datos multidimensionales&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Busque el cuadro de diálogo de la carpeta remota &#40;Analysis Services - datos multidimensionales&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)  
  
  
