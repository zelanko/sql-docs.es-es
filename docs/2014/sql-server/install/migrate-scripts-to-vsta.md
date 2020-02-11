---
title: Migrar scripts a VSTA | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SSIS Script task, converting scripts
- Script component [Integration Services], converting scripts
- Script task [Integration Services], converting scripts
- SSIS Script component, converting scripts
ms.assetid: d685098b-86a1-46bf-939a-63d56951e009
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: cb44a7b635e24c0c2e3266c1cca98a9c4f6a347c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093985"
---
# <a name="migrate-scripts-to-vsta"></a>Migrar scripts a VSTA
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Al actualizar paquetes a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] migra los scripts de las tareas script o los componentes script a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA). VSTA es el entorno de script que [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usa. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], el entorno de scripting [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] es para aplicaciones (VSA).  
  
 Si los scripts en las tareas Script o los componentes Script hacen referencia a las interfaces, podría tener que modificar esas referencias antes de actualizar el paquete. De lo contrario, el paquete no se podrá actualizar o los scripts no se podrán validar, dependiendo del método de actualización que use. Para modificar estas referencias, reemplace las referencias a las interfaces IDTS*xxx*90 por referencias a las interfaces IDTS*XXX*100 correspondientes.  
  
 Para obtener más información sobre cómo migrar scripts y actualizar paquetes, vea [actualizar paquetes de Integration Services](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
## <a name="understanding-migration-failures"></a>Descripción de los errores de migración  
 Al migrar los scripts, se puede producir un error en la migración debido a una de las razones siguientes:  
  
-   Se cambió el nombre del punto de entrada para el script de VSA.  
  
     El punto de entrada especifica el método en la clase `ScriptMain` en el proyecto de VSTA que el tiempo de ejecución de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] llama como punto de entrada al código de la tarea Script. La clase `ScriptMain` es la clase predeterminada que las plantillas de script generan.  
  
-   No hay ningún punto de entrada o hay varios en el script de VSA.  
  
-   No se pudieron agregar referencias de ensamblado.  
  
-   Se modificó la clase `ScriptMain` para heredar de otras clases además de la clase `ScriptObjectModelSSIS`. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] no admite la herencia múltiple.  
  
 No se puede convertir un script de VSA [!INCLUDE[vbprvblong](../../includes/vbprvblong-md.md)] que use en un script de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)]VSTA que use. Sin embargo, puede crear un nuevo script de VSTA que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)]use. Para obtener más información, consulte [Codificar y depurar la tarea Script](../../integration-services/control-flow/script-task.md) y [Codificar y depurar el componente de script](../../integration-services/data-flow/transformations/script-component.md).  
  
## <a name="see-also"></a>Consulte también  
 [Ampliar paquetes con scripting](../../relational-databases/server-management-objects-smo/tasks/scripting.md)  
  
  
