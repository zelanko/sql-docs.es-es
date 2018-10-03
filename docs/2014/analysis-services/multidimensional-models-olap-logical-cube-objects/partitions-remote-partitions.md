---
title: Las particiones remotas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- archiving remote partitions [Analysis Services]
- partitions [Analysis Services], remote
- restoring remote partitions [Analysis Services]
- backing up remote partitions [Analysis Services]
- partitions [Analysis Services], storage
- storing data [Analysis Services], partitions
- MasterDataSourceID property
- remote partitions [Analysis Services]
ms.assetid: 63f5d9f5-c6b6-4ceb-94fe-7b6c396d10bb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 09231b03e784c142ab8b99ed31c2c4c88f6e72d7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051926"
---
# <a name="remote-partitions"></a>Particiones remotas
  Los datos de una partición remota se almacenan en una instancia diferente de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a la instancia que contiene las definiciones (metadatos) de la partición y su cubo primario. Una partición remota se administra en la misma instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] donde se definen la partición y su cubo primario.  
  
> [!NOTE]  
>  Para almacenar una partición remota, el equipo debe tener una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instalado y se ejecuta el mismo nivel de service pack que la instancia donde se ha definido la partición. No se admiten particiones remotas en instancias de versiones anteriores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Cuando se incluyen particiones remotas en un grupo de medida, se distribuye la utilización de la CPU y la memoria del cubo entre todas las particiones del grupo de medida. Por ejemplo, al procesar una partición remota, sola o como parte del procesamiento del cubo primario, la mayor parte de la utilización de la CPU y la memoria de esa partición tiene lugar en la instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Un cubo que contenga particiones remotas puede contener dimensiones habilitadas para escritura; sin embargo, esto puede afectar al rendimiento del cubo. Para obtener más información acerca de las dimensiones habilitadas para escritura, consulte [dimensiones habilitadas para escritura](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
## <a name="storage-modes-for-remote-partitions"></a>Modos de almacenamiento para particiones remotas  
 Las particiones remotas pueden usar cualquiera de los tipos de almacenamiento utilizados por las particiones locales: OLAP multidimensional (MOLAP), OLAP híbrido (HOLAP) u OLAP relacional (ROLAP). Las particiones remotas también pueden usar almacenamiento en caché automático. En función del modo de almacenamiento de una partición remota, en la instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se almacenan los datos siguientes.  
  
|||  
|-|-|  
|Tipo de almacenamiento|data|  
|MOLAP|Las agregaciones de la partición y una copia de los datos de origen de la partición|  
|HOLAP|Las agregaciones de la partición|  
|ROLAP|Ningún dato de partición|  
  
 Si un grupo de medida contiene varias particiones MOLAP u HOLAP almacenadas en varias instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el cubo distribuye los datos del grupo de medida entre esas instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="merging-remote-partitions"></a>Combinar particiones remotas  
 Las particiones remotas solo se pueden mezclar con otras particiones remotas que se almacenen en la misma instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obtener más información acerca de cómo combinar particiones, consulte [mezclar particiones en Analysis Services &#40;SSAS - multidimensionales&#41;](../multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md).  
  
## <a name="archiving-and-restoring-remote-partitions"></a>Archivar y restaurar particiones remotas  
 Los datos de particiones remotas se pueden archivar o restaurar cuando la base de datos que almacena la partición remota se archiva o restaura. Si se restaura una base de datos sin restaurar una partición remota, se debe procesar la partición remota para poder utilizar los datos de la partición. Para obtener más información sobre cómo archivar y restaurar bases de datos, vea [copias de seguridad y restauración de Analysis Services Databases](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar una partición remota &#40;Analysis Services&#41;](../multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)   
 [Objetos de procesamiento de Analysis Services](../multidimensional-models/processing-analysis-services-objects.md)  
  
  
