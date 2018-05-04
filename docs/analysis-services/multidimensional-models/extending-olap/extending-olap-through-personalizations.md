---
title: Extender OLAP mediante personalizaciones | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 72c3be76e49d91e2410f98d3ea721712ee6aba03
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="extending-olap-through-personalizations"></a>Extender OLAP mediante personalizaciones
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services proporciona numerosas funciones intrínsecas para su uso con los lenguajes de expresiones multidimensionales (MDX) y extensiones de minería de datos (DMX). Estas funciones están diseñadas para realizar multitud de tareas, desde cálculos estadísticos estándar hasta recorridos por los miembros de una jerarquía. No obstante, al igual que sucede con cualquier otro producto de gran complejidad y solidez, existe siempre la necesidad de ampliar su funcionalidad en el futuro.  
  
 Por lo tanto, Analysis Services proporciona la posibilidad de agregar ensamblados y extensiones personalizadas a una instancia del servicio para completar las necesidades empresariales cuando la funcionalidad estándar deja de ser suficiente.  
  
## <a name="assemblies"></a>Ensamblados  
 Los ensamblados permiten ampliar la funcionalidad empresarial de MDX y DMX. Se puede crear la funcionalidad que se desee en una biblioteca, como por ejemplo una biblioteca de vínculos dinámicos (DLL), y agregar la biblioteca como un ensamblado a una instancia o una base de datos de Analysis Services. Los métodos públicos de la biblioteca se ofrecerán como funciones definidas por el usuario a procedimientos, cálculos, acciones, aplicaciones cliente y expresiones de MDX y DMX.  
  
## <a name="personalized-extensions"></a>Extensiones personalizadas  
 Las extensiones de personalización de SQL Server Analysis Services constituyen el fundamento de la idea de implementar una arquitectura de complemento. Las extensiones de personalización de Analysis Services son una modificación simple y elegante de la arquitectura de ensamblado administrado existente y se exponen en el modelo de objetos <xref:Microsoft.AnalysisServices.AdomdServer>, la sintaxis de Expresiones multidimensionales (MDX) y los conjuntos de filas de esquema de Analysis Services.  
  
## <a name="see-also"></a>Vea también  
 [Administración de ensamblados de modelos multidimensionales](../../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Las extensiones de personalización de Analysis Services](../../../analysis-services/multidimensional-models/extending-olap/analysis-services-personalization-extensions.md)  
  
  
