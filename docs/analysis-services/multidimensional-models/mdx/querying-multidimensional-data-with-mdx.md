---
title: Consultar datos multidimensionales con MDX | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: multidimensional data [Analysis Services], querying
ms.assetid: e0a5dd60-35a3-4a4f-b36f-52ecea814886
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 1c7afc85473545c4801973c3fdf8b19a95141917
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="querying-multidimensional-data-with-mdx"></a>Consultar datos multidimensionales con MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Expresiones multidimensionales (MDX) es el lenguaje de consulta que usa para trabajar con y recuperar datos multidimensionales en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. MDX está basado en la especificación XML for Analysis (XMLA), con extensiones específicas para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. MDX usa expresiones compuestas de identificadores, valores, instrucciones, funciones y operadores que [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] puede evaluar para recuperar un objeto (por ejemplo, un conjunto o un miembro) o un valor escalar (por ejemplo, una cadena o un número).  
  
 Las consultas y expresiones MDX de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se utilizan para lo siguiente:  
  
-   Devolver datos a una aplicación cliente desde un cubo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
-   Aplicar formato a los resultados de las consultas.  
  
-   Realizar tareas de diseño de cubos, como la definición de miembros calculados, conjuntos con nombre, asignaciones con ámbito e indicadores clave de rendimiento (KPI).  
  
-   Realizar tareas administrativas, incluida la seguridad de dimensión y de celda.  
  
 MDX es superficialmente similar en muchos aspectos a la sintaxis SQL, que se suele utilizar con bases de datos relacionales. Sin embargo, MDX no es una extensión del lenguaje SQL y es diferente de SQL en muchos aspectos. Para crear expresiones MDX utilizadas para diseñar o proteger cubos, o para crear consultas MDX que devuelvan y apliquen formato a los datos multidimensionales, debe comprender los conceptos básicos de MDX y el modelado dimensional, los elementos de sintaxis MDX, los operadores MDX, las instrucciones MDX y las funciones MDX.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Conceptos clave de MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)|Puede usar MDX (Expresiones multidimensionales) para consultar datos multidimensionales o para crear expresiones MDX para usarlas en un cubo, aunque primero necesita entender los conceptos y la terminología de dimensión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|  
|[Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)|Las expresiones multidimensionales (MDX) permiten consultar objetos multidimensionales, como los cubos, y devolver conjuntos de celdas multidimensionales que contengan los datos del cubo. Este tema y los temas secundarios proporcionan información general sobre las consultas MDX.|  
|[Aspectos básicos de scripting MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)|En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], un script de expresiones multidimensionales (MDX) se compone de una o más expresiones o instrucciones MDX que rellenan un cubo con cálculos.<br /><br /> Un script MDX define el proceso de cálculo del cubo. Los scripts MDX también se consideran parte del cubo. Por lo tanto, si se cambia un script MDX asociado a un cubo, también se cambia de forma inmediata el proceso de cálculo del cubo.<br /><br /> Para crear scripts MDX, puede utilizar el Diseñador de cubos de [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].|  
  
## <a name="see-also"></a>Ver también  
 [Elementos de la sintaxis de MDX &#40;MDX&#41;](../../../mdx/mdx-syntax-elements-mdx.md)   
 [Referencia del lenguaje MDX &#40;MDX&#41;](../../../mdx/mdx-language-reference-mdx.md)  
  
  
