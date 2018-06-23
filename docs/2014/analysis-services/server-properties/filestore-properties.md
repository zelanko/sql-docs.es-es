---
title: Propiedades de FILESTORE | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Income property
- InitialBonus property
- PercentScanPerPrice property
- FileStore properties
- BackgroundTrimCost property
- Tax property
- PerformanceTrace property
- MinimumBalance property
- UnbufferedThreshold property
- BackgroundTrimAmount property
- MaximumBalance property
- MemoryLimitMin property
- MemoryLimit property
ms.assetid: 580cf0aa-7425-4d48-aa8d-128f5b488fcd
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4bff551f29c7d16fc068bb0f41d2b17917e2145c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108421"
---
# <a name="filestore-properties"></a>Filestore, propiedades
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades del servidor de almacén de archivos que aparecen en las tablas siguientes. Todas son propiedades avanzadas que no se deben cambiar, salvo bajo la orientación de soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obtener más información sobre las propiedades de servidor adicionales y cómo establecerlas, vea [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md).  
  
 **Se aplica a:** modo de servidor multidimensional y tabular  
  
## <a name="properties"></a>Propiedades  
 `MemoryLimit`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MemoryLimitMin`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `PercentScanPerPrice`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `PerformanceTrace`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `RandomFileAccessMode`  
 Una propiedad booleana que indica si se tiene acceso a los archivos de base de datos y a los archivos almacenados en memoria caché en modo de acceso a archivos aleatorio. Esta propiedad está desactivada de forma predeterminada. De forma predeterminada, Analysis Services no establece la marca de acceso a archivos aleatorio al abrir los archivos de datos de partición para el acceso de lectura.  
  
 En sistemas de tecnología avanzada, especialmente en aquellos con grandes recursos de memoria y varios nodos NUMA, puede ser ventajoso utilizar el acceso a archivos aleatorio. En modo de acceso aleatorio, Windows omite las operaciones de asignación de páginas que leen datos del disco en la memoria caché de archivos del sistema, con lo que reduce la contención en la memoria caché.  
  
 Tendrá que ejecutar pruebas comparativas para determinar si el rendimiento de las consultas mejora al cambiar esta propiedad. Para obtener las prácticas recomendadas para realizar pruebas comparativas, como es borrar la memoria caché y evitar errores comunes, vea la [Guía de operaciones de SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539). Para obtener información adicional sobre los inconvenientes del uso de esta propiedad, vea [ http://support.microsoft.com/kb/2549369 ](http://support.microsoft.com/kb/2549369).  
  
 Para ver o modificar esta propiedad en Management Studio, habilite la lista de propiedades avanzadas en la página de propiedades del servidor. También puede cambiar la propiedad en el archivo msmdsrv.ini. Se recomienda reiniciar el servidor después de establecer esta propiedad; en caso contrario, se seguirá accediendo a los archivos que ya estén abiertos en el modo anterior.  
  
 `UnbufferedThreshold`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="memory-model-category"></a>Categoría de modelo de memoria  
 `MemoryModel\Tax`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MemoryModel\Income`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MemoryModel\MaximumBalance`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MemoryModel\MinimumBalance`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MemoryModel\InitialBonus`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Configurar propiedades del servidor de Analysis Services](server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  