---
title: Definir procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services]
- OLAP [Analysis Services], stored procedures
- external routines [Analysis Services]
- stored procedures [Analysis Services], about stored procedures
ms.assetid: f9c57d91-f60f-4f0e-8f7f-d87f4ba97b7c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 69daca3a13cf5318e102002f0edfcb98b80ff9d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62702769"
---
# <a name="defining-stored-procedures"></a>Definir procedimientos almacenados
  Puede usar los procedimientos almacenados para llamar a rutinas externas desde [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Puede escribir una rutina externa llamada por un procedimiento almacenado en cualquier lenguaje de la biblioteca CLR (Common Language Runtime) como, por ejemplo C, C++, C#, Visual Basic o Visual Basic .NET. Un procedimiento almacenado se puede crear una vez y ser llamado desde muchos contextos como, por ejemplo, otros procedimientos almacenados, medidas calculadas o aplicaciones cliente. Los procedimientos almacenados simplifican el desarrollo y la implementación de las bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] al permitir que se desarrolle una sola vez el código común y se almacene en una sola ubicación. Los procedimientos almacenados se pueden utilizar para agregar funcionalidades de negocio a las aplicaciones que no sean suministradas por la funcionalidad nativa de MDX.  
  
 En esta sección se proporciona la información necesaria para comprender, diseñar e implementar procedimientos almacenados.  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Diseño de procedimientos almacenados](../multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|Describe cómo diseñar ensamblados que se utilizarán con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Creación de procedimientos almacenados](creating-stored-procedures.md)|Describe cómo crear ensamblados para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Llamada a procedimientos almacenados](calling-stored-procedures.md)|Proporciona información acerca de cómo utilizar ensamblados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Acceso al contexto de la consulta en los procedimientos almacenados](accessing-query-context-in-stored-procedures.md)|Describe cómo tener acceso a la información de ámbito y contexto con ensamblados.|  
|[Configuración de la seguridad para procedimientos almacenados](setting-security-for-stored-procedures.md)|Describe cómo configurar la seguridad para ensamblados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Depuración de procedimientos almacenados](debugging-stored-procedures.md)|Describe cómo depurar ensamblados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
  
## <a name="see-also"></a>Vea también  
 [Administración de ensamblados de modelos multidimensionales](../multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
