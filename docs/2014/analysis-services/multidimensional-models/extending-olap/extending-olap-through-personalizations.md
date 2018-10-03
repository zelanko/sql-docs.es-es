---
title: Extender OLAP mediante personalizaciones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- Analysis Services, extensibility
ms.assetid: 348e49fc-4390-43c1-9b6c-61b386ff4373
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 67e1af257dcdb9700fcdfa6643a50000f9dc845f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48092195"
---
# <a name="extending-olap-through-personalizations"></a>Extender OLAP mediante personalizaciones
  Microsoft [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] proporciona numerosas funciones intrínsecas para su uso con los lenguajes MDX (Expresiones multidimensionales) y DMX (Extensiones de minería de datos). Estas funciones están diseñadas para realizar multitud de tareas, desde cálculos estadísticos estándar hasta recorridos por los miembros de una jerarquía. No obstante, al igual que sucede con cualquier otro producto de gran complejidad y solidez, existe siempre la necesidad de ampliar su funcionalidad en el futuro.  
  
 Por lo tanto, Analysis Services proporciona la posibilidad de agregar ensamblados y extensiones personalizadas a una instancia del servicio para completar las necesidades empresariales cuando la funcionalidad estándar deja de ser suficiente.  
  
## <a name="assemblies"></a>Ensamblados  
 Los ensamblados permiten ampliar la funcionalidad empresarial de MDX y DMX. Se puede crear la funcionalidad que se desee en una biblioteca, como por ejemplo una biblioteca de vínculos dinámicos (DLL), y agregar la biblioteca como un ensamblado a una instancia o una base de datos de Analysis Services. Los métodos públicos de la biblioteca se ofrecerán como funciones definidas por el usuario a procedimientos, cálculos, acciones, aplicaciones cliente y expresiones de MDX y DMX.  
  
## <a name="personalized-extensions"></a>Extensiones personalizadas  
 Las extensiones de personalización de SQL Server Analysis Services constituyen el fundamento de la idea de implementar una arquitectura de complemento. Las extensiones de personalización de Analysis Services son una modificación simple y elegante de la arquitectura de ensamblado administrado existente y se exponen en el modelo de objetos <xref:Microsoft.AnalysisServices.AdomdServer>, la sintaxis de Expresiones multidimensionales (MDX) y los conjuntos de filas de esquema de Analysis Services.  
  
## <a name="see-also"></a>Vea también  
 [Administración de los ensamblados de modelos multidimensionales](../multidimensional-model-assemblies-management.md)   
 [Extensiones de personalización de Analysis Services](analysis-services-personalization-extensions.md)  
  
  
