---
title: Definir procedimientos almacenados | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- stored procedures [Analysis Services]
- OLAP [Analysis Services], stored procedures
- external routines [Analysis Services]
- stored procedures [Analysis Services], about stored procedures
ms.assetid: f9c57d91-f60f-4f0e-8f7f-d87f4ba97b7c
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b70d20ea8ad3cc108076261b692129bf72ccb6ef
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="defining-stored-procedures"></a>Definir procedimientos almacenados
  Puede usar los procedimientos almacenados para llamar a rutinas externas desde [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Puede escribir una rutina externa llamada por un procedimiento almacenado en cualquier lenguaje de la biblioteca CLR (Common Language Runtime) como, por ejemplo C, C++, C#, Visual Basic o Visual Basic .NET. Un procedimiento almacenado se puede crear una vez y ser llamado desde muchos contextos como, por ejemplo, otros procedimientos almacenados, medidas calculadas o aplicaciones cliente. Los procedimientos almacenados simplifican el desarrollo y la implementación de las bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] al permitir que se desarrolle una sola vez el código común y se almacene en una sola ubicación. Los procedimientos almacenados se pueden utilizar para agregar funcionalidades de negocio a las aplicaciones que no sean suministradas por la funcionalidad nativa de MDX.  
  
 En esta sección se proporciona la información necesaria para comprender, diseñar e implementar procedimientos almacenados.  
  
|Tema|Description|  
|-----------|-----------------|  
|[Diseñar procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|Describe cómo diseñar ensamblados que se utilizarán con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Crear procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md)|Describe cómo crear ensamblados para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Llamar a procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)|Proporciona información acerca de cómo utilizar ensamblados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Al obtener acceso al contexto de la consulta en procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/accessing-query-context-in-stored-procedures.md)|Describe cómo tener acceso a la información de ámbito y contexto con ensamblados.|  
|[Configurar la seguridad para procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)|Describe cómo configurar la seguridad para ensamblados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Depurar procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)|Describe cómo depurar ensamblados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
  
## <a name="see-also"></a>Vea también  
 [Administración de ensamblados de modelos multidimensionales](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  

