---
title: Almacenamiento de dimensiones | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- dimensions [Analysis Services], storage
- storing data [Analysis Services]
- storage [Analysis Services], dimensions
- relational OLAP
- multidimensional OLAP
- MOLAP
- storing data [Analysis Services], dimensions
- ROLAP
ms.assetid: 8d74b932-2174-4e1f-8414-636455880b6a
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b45ab57b151c2cdab5ae7aa133befd06893037bd
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dimensions---storage"></a>Dimensiones - almacenamiento
  Las dimensiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admiten dos modos de almacenamiento:  
  
-   OLAP relacional (ROLAP)  
  
-   OLAP multidimensional (MOLAP)  
  
 El modo de almacenamiento determina la ubicación y la forma de los datos de una dimensión. El modo de almacenamiento predeterminado para las dimensiones es MOLAP. **Temas relacionados:**[procesamiento y modos de almacenamiento de partición](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
## <a name="molap"></a>MOLAP  
 Los datos de una dimensión que utiliza MOLAP se almacenan en una estructura multidimensional en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Esta estructura multidimensional se crea y se llena al procesarse la dimensión. Las dimensiones MOLAP proporcionan un mejor rendimiento de las consultas que las dimensiones ROLAP.  
  
## <a name="rolap"></a>ROLAP  
 Los datos de una dimensión que utiliza ROLAP se almacenan en las tablas utilizadas para definir la dimensión. Se puede utilizar el modo de almacenamiento ROLAP para admitir grandes dimensiones sin duplicar grandes cantidades de datos, pero a expensas del rendimiento de las consultas. Puesto que la dimensión depende directamente de las tablas de la vista del origen de datos utilizadas para definir la dimensión, el modo de almacenamiento ROLAP también admite OLAP en tiempo real.  
  
> [!IMPORTANT]  
>  Si una dimensión utiliza el modo de almacenamiento ROLAP y la dimensión se incluye en un cubo que use el almacenamiento MOLAP, el cubo deberá procesarse de inmediato si se realiza algún cambio en el esquema de su tabla de origen. Si no se hace de esta manera, pueden producirse resultados incoherentes al realizar consultas al cubo. **Tema relacionado:**[automatizar Analysis Services tareas administrativas con SSIS](../../analysis-services/instances/automate-analysis-services-administrative-tasks-with-ssis.md).  
  
## <a name="see-also"></a>Vea también  
 [Procesamiento y modos de almacenamiento de particiones](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
  

