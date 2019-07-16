---
title: Almacenamiento de dimensiones | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3d739bd19cd5be1f9b6167acbf104f569fc517ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209250"
---
# <a name="dimensions---storage"></a>Dimensiones: almacenamiento
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Las dimensiones en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admiten dos modos de almacenamiento:  
  
-   OLAP relacional (ROLAP)  
  
-   OLAP multidimensional (MOLAP)  
  
 El modo de almacenamiento determina la ubicación y la forma de los datos de una dimensión. El modo de almacenamiento predeterminado para las dimensiones es MOLAP. **Temas relacionados:** [procesamiento y modos de almacenamiento de partición](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
## <a name="molap"></a>MOLAP  
 Los datos de una dimensión que utiliza MOLAP se almacenan en una estructura multidimensional en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Esta estructura multidimensional se crea y se llena al procesarse la dimensión. Las dimensiones MOLAP proporcionan un mejor rendimiento de las consultas que las dimensiones ROLAP.  
  
## <a name="rolap"></a>ROLAP  
 Los datos de una dimensión que utiliza ROLAP se almacenan en las tablas utilizadas para definir la dimensión. Se puede utilizar el modo de almacenamiento ROLAP para admitir grandes dimensiones sin duplicar grandes cantidades de datos, pero a expensas del rendimiento de las consultas. Puesto que la dimensión depende directamente de las tablas de la vista del origen de datos utilizadas para definir la dimensión, el modo de almacenamiento ROLAP también admite OLAP en tiempo real.  
  
> [!IMPORTANT]  
>  Si una dimensión utiliza el modo de almacenamiento ROLAP y la dimensión se incluye en un cubo que use el almacenamiento MOLAP, el cubo deberá procesarse de inmediato si se realiza algún cambio en el esquema de su tabla de origen. Si no se hace de esta manera, pueden producirse resultados incoherentes al realizar consultas al cubo. **Tema relacionado:** [automatizar Analysis Services Administrative Tasks with SSIS](../../analysis-services/instances/automate-analysis-services-administrative-tasks-with-ssis.md).  
  
## <a name="see-also"></a>Vea también  
 [Procesamiento y modos de almacenamiento de particiones](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
  
