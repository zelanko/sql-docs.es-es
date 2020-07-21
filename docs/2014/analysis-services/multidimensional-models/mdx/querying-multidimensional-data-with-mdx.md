---
title: Consultar datos multidimensionales con MDX | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [Analysis Services], querying
ms.assetid: e0a5dd60-35a3-4a4f-b36f-52ecea814886
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7b7589a98636e56e8c592cef213785544e18f4ea
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546207"
---
# <a name="querying-multidimensional-data-with-mdx"></a>Consultar datos multidimensionales con MDX
  Expresiones multidimensionales (MDX) es el lenguaje de consulta que se usa para trabajar con datos multidimensionales y recuperarlos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . MDX se basa en la especificación de XML for Analysis (XMLA), con extensiones específicas para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . MDX usa expresiones compuestas de identificadores, valores, instrucciones, funciones y operadores que [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] puede evaluar para recuperar un objeto (por ejemplo, un conjunto o un miembro) o un valor escalar (por ejemplo, una cadena o un número).  
  
 Las consultas y expresiones MDX de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se utilizan para hacer lo siguiente:  
  
-   Devolver datos a una aplicación cliente desde un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cubo.  
  
-   Aplicar formato a los resultados de las consultas.  
  
-   Realizar tareas de diseño de cubos, como la definición de miembros calculados, conjuntos con nombre, asignaciones con ámbito e indicadores clave de rendimiento (KPI).  
  
-   Realizar tareas administrativas, incluida la seguridad de dimensión y de celda.  
  
 MDX es superficialmente similar en muchos aspectos a la sintaxis SQL, que se suele utilizar con bases de datos relacionales. Sin embargo, MDX no es una extensión del lenguaje SQL y es diferente de SQL en muchos aspectos. Para crear expresiones MDX utilizadas para diseñar o proteger cubos, o para crear consultas MDX que devuelvan y apliquen formato a los datos multidimensionales, debe comprender los conceptos básicos de MDX y el modelado dimensional, los elementos de sintaxis MDX, los operadores MDX, las instrucciones MDX y las funciones MDX.  
  
> [!NOTE]  
>  Para obtener más información, consulte la sección recursos adicionales en la página [SQL Server 2005-Analysis Services](https://go.microsoft.com/fwlink/?LinkId=80853) en el sitio web de Microsoft TechNet. Para obtener más información acerca de los problemas de rendimiento relacionados con las consultas y los cálculos de MDX, vea la sección sobre escritura de MDX eficaz en la [Guía de rendimiento de SQL Server 2005 Analysis Services](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Conceptos clave de MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)|Puede utilizar expresiones multidimensionales (MDX) para consultar datos multidimensionales o para crear expresiones MDX para usarlas en un cubo, pero primero debe comprender los [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] conceptos y la terminología de las dimensiones.|  
|[Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)|Las expresiones multidimensionales (MDX) permiten consultar objetos multidimensionales, como los cubos, y devolver conjuntos de celdas multidimensionales que contengan los datos del cubo. Este tema y los temas secundarios proporcionan información general sobre las consultas MDX.|  
|[Aspectos básicos de scripting MDX &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)|En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], un script de expresiones multidimensionales (MDX) se compone de una o más expresiones o instrucciones MDX que llenan un cubo con cálculos.<br /><br /> Un script MDX define el proceso de cálculo del cubo. Los scripts MDX también se consideran parte del cubo. Por lo tanto, si se cambia un script MDX asociado a un cubo, también se cambia de forma inmediata el proceso de cálculo del cubo.<br /><br /> Para crear scripts MDX, puede utilizar el Diseñador de cubos de [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].|  
  
## <a name="see-also"></a>Consulte también  
 [Elementos de sintaxis MDX &#40;MDX&#41;](/sql/mdx/mdx-syntax-elements-mdx)   
 [Referencia del lenguaje MDX &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)  
  
  
