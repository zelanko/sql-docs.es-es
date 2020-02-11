---
title: Aspectos básicos de scripting de MDX (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], scripts
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [MDX]
- cubes [Analysis Services], calculations
- Multidimensional Expressions [Analysis Services], scripts
ms.assetid: fdecb3ce-7c87-4bab-8000-532ba7a29f96
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 17cb2b326ed510a952249da6a73693b6be6ab252
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073858"
---
# <a name="mdx-scripting-fundamentals-analysis-services"></a>Aspectos básicos de scripting MDX (Analysis Services)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] En [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], un script de expresiones multidimensionales (MDX) se compone de una o más expresiones o instrucciones MDX que rellenan un cubo con cálculos.  
  
 Un script MDX define el proceso de cálculo del cubo. Los scripts MDX también se consideran parte del cubo. Por lo tanto, si se cambia un script MDX asociado a un cubo, también se cambia de forma inmediata el proceso de cálculo del cubo.  
  
 Para crear scripts MDX, puede utilizar el Diseñador de cubos de [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Para más información, vea [Definir asignaciones y otros comandos de script](../define-assignments-and-other-script-commands.md) e [Introduction to MDX Scripting in Microsoft SQL Server 2005 (Introducción a la creación de scripts en Microsoft SQL Server 2005)](https://go.microsoft.com/fwlink/?LinkId=81892).  
  
 Encontrará información acerca de los problemas de rendimiento relacionados con los cálculos y las consultas MDX en la sección dedicada a la optimización de MDX de la [guía de rendimiento de SQL Server Analysis Services](https://go.microsoft.com/fwlink/p/?LinkId=399050).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Script MDX básico &#40;MDX&#41;](the-basic-mdx-script-mdx.md)|Incluye información detallada sobre el script MDX básico, incluido el script MDX predeterminado proporcionado en cada cubo, así como información sobre el funcionamiento general de los scripts MDX en los cubos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Administrar el ámbito y el contexto &#40;MDX&#41;](managing-scope-and-context-mdx.md)|Describe cómo utilizar la instrucción [CALCULATE](/sql/mdx/mdx-scripting-calculate) , la instrucción [SCOPE](/sql/mdx/mdx-scripting-scope) y la función [This](/sql/mdx/this-mdx) para administrar el contexto y el ámbito de un script MDX.|  
|[Usar variables y parámetros &#40;&#41;MDX](using-variables-and-parameters-mdx.md)|Describe cómo utilizar las variables y los parámetros en un script MDX.|  
|[Control de errores &#40;&#41;MDX](error-handling-mdx.md)|Explica cómo administrar los errores en un script MDX.|  
|[&#41;MDX &#40;MDX compatible](supported-mdx-mdx.md)|Proporciona una lista de operadores, instrucciones y funciones MDX admitidos en un script MDX.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del lenguaje MDX &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)  
  
  
