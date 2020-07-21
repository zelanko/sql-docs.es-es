---
title: Extender OLAP mediante personalizaciones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services, extensibility
ms.assetid: 348e49fc-4390-43c1-9b6c-61b386ff4373
author: minewiskan
ms.author: owend
ms.openlocfilehash: 93669980e989b1cb11673f45c111de3609bbe920
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468950"
---
# <a name="extending-olap-through-personalizations"></a>Extender OLAP mediante personalizaciones
  Microsoft [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] proporciona numerosas funciones intrínsecas para su uso con los lenguajes MDX (Expresiones multidimensionales) y DMX (Extensiones de minería de datos). Estas funciones están diseñadas para realizar multitud de tareas, desde cálculos estadísticos estándar hasta recorridos por los miembros de una jerarquía. No obstante, al igual que sucede con cualquier otro producto de gran complejidad y solidez, existe siempre la necesidad de ampliar su funcionalidad en el futuro.  
  
 Por lo tanto, Analysis Services proporciona la posibilidad de agregar ensamblados y extensiones personalizadas a una instancia del servicio para completar las necesidades empresariales cuando la funcionalidad estándar deja de ser suficiente.  
  
## <a name="assemblies"></a>Ensamblados  
 Los ensamblados permiten ampliar la funcionalidad empresarial de MDX y DMX. Se puede crear la funcionalidad que se desee en una biblioteca, como por ejemplo una biblioteca de vínculos dinámicos (DLL), y agregar la biblioteca como un ensamblado a una instancia o una base de datos de Analysis Services. Los métodos públicos de la biblioteca se ofrecerán como funciones definidas por el usuario a procedimientos, cálculos, acciones, aplicaciones cliente y expresiones de MDX y DMX.  
  
## <a name="personalized-extensions"></a>Extensiones personalizadas  
 Las extensiones de personalización de SQL Server Analysis Services constituyen el fundamento de la idea de implementar una arquitectura de complemento. Analysis Services las extensiones de personalización son una modificación simple y elegante de la arquitectura de ensamblado administrado existente y se exponen en Analysis Services el modelo de objetos de [Microsoft. AnalysisServices. AdomdServer](/previous-versions/sql/sql-server-2014/ms131779(v=sql.120)) , sintaxis de expresiones multidimensionales (MDX) y conjuntos de filas de esquema.  
  
## <a name="see-also"></a>Consulte también  
 [Administración de ensamblados de modelos multidimensionales](../multidimensional-model-assemblies-management.md)   
 [Extensiones de personalización de Analysis Services](analysis-services-personalization-extensions.md)  
  
  
