---
title: Definir procedimientos almacenados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54b14cd5ee54edab4508c06c55e5815bfeab934f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209381"
---
# <a name="defining-stored-procedures"></a>Definir procedimientos almacenados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Puede usar los procedimientos almacenados para llamar a rutinas externas desde [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Puede escribir una rutina externa llamada por un procedimiento almacenado en cualquier lenguaje de la biblioteca CLR (Common Language Runtime) como, por ejemplo C, C++, C#, Visual Basic o Visual Basic .NET. Un procedimiento almacenado se puede crear una vez y ser llamado desde muchos contextos como, por ejemplo, otros procedimientos almacenados, medidas calculadas o aplicaciones cliente. Los procedimientos almacenados simplifican el desarrollo y la implementación de las bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] al permitir que se desarrolle una sola vez el código común y se almacene en una sola ubicación. Los procedimientos almacenados se pueden utilizar para agregar funcionalidades de negocio a las aplicaciones que no sean suministradas por la funcionalidad nativa de MDX.  
  
 En esta sección se proporciona la información necesaria para comprender, diseñar e implementar procedimientos almacenados.  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Diseño de procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|Describe cómo diseñar ensamblados que se utilizarán con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Creación de procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md)|Describe cómo crear ensamblados para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Llamada a procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)|Proporciona información acerca de cómo utilizar ensamblados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Acceso al contexto de la consulta en los procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/accessing-query-context-in-stored-procedures.md)|Describe cómo tener acceso a la información de ámbito y contexto con ensamblados.|  
|[Configuración de la seguridad para procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)|Describe cómo configurar la seguridad para ensamblados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Depuración de procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)|Describe cómo depurar ensamblados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
  
## <a name="see-also"></a>Vea también  
 [Administración de ensamblados de modelos multidimensionales](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
