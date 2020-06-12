---
title: Conceder permisos para procedimientos almacenados (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 01793166-a3e5-4856-8302-21b82d494e69
author: minewiskan
ms.author: owend
ms.openlocfilehash: 960b0ef3f050b780998a0f86dcd7b7edf121676d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544317"
---
# <a name="grant-permissions-on-stored-procedures-analysis-services"></a>Conceder permisos para procedimientos almacenados (Analysis Services)
  Los procedimientos almacenados, o ensamblados, en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] son rutinas externas escritas en lenguaje de programación [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET que amplían las capacidades de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Los ensamblados permiten a los programadores beneficiarse de la integración entre lenguajes, el tratamiento de excepciones, la compatibilidad de control de versiones, la compatibilidad de implementación y la compatibilidad de depuración.  
  
 Debe ser un administrador del servidor para registrar un ensamblado. Vea [conceder permisos de administrador de servidor &#40;Analysis Services&#41;](instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
## <a name="security-context-for-stored-procedure-execution"></a>Contexto de seguridad para la ejecución del procedimiento almacenado  
 Cualquier usuarios puede llamar a un procedimiento almacenado. Dependiendo de la configuración del procedimiento almacenado, el procedimiento puede ejecutarse en el contexto del usuario que llama al procedimiento o en el contexto de un usuario anónimo. Puesto que un usuario anónimo no tiene contexto de seguridad, puede combinar esta capacidad con la configuración de la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para permitir el acceso anónimo.  
  
 Después de que el usuario haya llamado a un procedimiento almacenado pero antes de que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] haya ejecutado el procedimiento almacenado, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] evalúa las acciones dentro del procedimiento almacenado. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] evalúa las acciones en un procedimiento almacenado en función de la intersección de los permisos concedidos al usuario y el conjunto de permisos utilizado para ejecutar el procedimiento. Si el procedimiento almacenado contiene alguna acción que el rol de la base de datos no puede realizar para el usuario, esa acción no se llevará a cabo.  
  
 A continuación se enumeran los conjuntos de permisos utilizados para ejecutar procedimientos almacenados:  
  
-   **Safe** Con el conjunto de permisos Safe, un procedimiento almacenado no puede tener acceso a los recursos protegidos en el [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework. Este conjunto de permisos solamente permite realizar cálculos. Se trata del conjunto de permisos más seguro, puesto que impide cualquier pérdida de información en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], los permisos no pueden elevarse y el riesgo de ataques que dañan los datos es mínimo.  
  
-   **Acceso externo** Con el conjunto de permisos de acceso externo, un procedimiento almacenado puede tener acceso a recursos externos mediante código administrado. Cuando se establece un procedimiento almacenado en este conjunto de permisos, no se producen errores de programación que podrían dar como resultado un funcionamiento inestable del servidor. Sin embargo, al utilizar este conjunto de permisos puede producirse alguna pérdida de información del servidor y existe la posibilidad de una elevación de los permisos y ataques que pueden dañar los datos.  
  
-   **Sin restricciones** Con el permiso Unrestricted establecido, un procedimiento almacenado puede tener acceso a recursos externos mediante cualquier código. Con este permiso establecido, no puede garantizarse la seguridad ni la confiabilidad de los procedimientos almacenados.  
  
## <a name="see-also"></a>Consulte también  
 [Administración de ensamblados de modelos multidimensionales](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
