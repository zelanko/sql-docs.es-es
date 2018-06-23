---
title: No incluye funcionalidad de Analysis Services en SQL Server 2014 | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Analysis Services, backward compatibility
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
- discontinued functionality [Analysis Services]
- unsupported features [Analysis Services]
ms.assetid: 39406be1-9819-4629-9c29-b32fb20bab2e
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 52b6dbe4ed746b151a6d9bae3a606c2f0e117df4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199224"
---
# <a name="discontinued-analysis-services-functionality-in-sql-server-2014"></a>Funcionalidad de Analysis Services no incluida en SQL Server 2014
  Este tema describe las características de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que ya no están disponibles en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## <a name="discontinued-features-in-includesssql14includessssql14-mdmd"></a>Características no incluidas en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
  
|Categoría|Característica desusada|Sustituta|  
|--------------|------------------------|-----------------|  
|Cubos locales|Propiedad de la cadena de conexión InsertInto|La sintaxis original de la cadena de conexión para rellenar cubos locales se sustituye por la instrucción Create Global Cube. Para obtener más información, consulte [instrucción CREATE GLOBAL CUBE &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-global-cube).|  
|Cubos locales|Propiedad de la cadena de conexión CreateCube|La sintaxis original de la cadena de conexión para rellenar cubos locales se sustituye por la instrucción Create Global Cube. Para obtener más información, consulte [instrucción CREATE GLOBAL CUBE &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-global-cube).|  
|Minería de datos|SQL Server 2000 PMML|La característica de SQL Server 2000 PMML creaba una forma de PMML que tenía extensiones propias para admitir las características únicas que proporcionan los algoritmos de minería de datos que no estaban disponibles en la especificación PMML. En SQL Server 2005, Analysis Services actualizó la característica PMML al estándar PMML 2.1 más reciente. Como resultado, las extensiones propias agregadas en SQL Server 2000 ya no se necesitan, aunque todavía se admiten en esta versión.|  
|Instrucción MDX|Instrucción Create Action|Esta instrucción se incluye por compatibilidad con versiones anteriores. Se reemplaza por el objeto Action. Para obtener más información sobre cómo crear acciones en las versiones recientes de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], consulte [acciones &#40;Analysis Services - datos multidimensionales&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md).|  
  
## <a name="discontinued-features-in-previous-releases"></a>Características descontinuadas en versiones anteriores  
 El Asistente para la migración, que se usaba para migrar las bases de datos de SQL Server 2000  Analysis Services a versiones más recientes, se deja de usar porque SQL Server 2000 ya no se admite.  
  
 La biblioteca Objetos de ayuda para la toma de decisiones (DSO) que proporcionaba compatibilidad con las bases de datos de SQL Server 2000 Analysis Services también ha dejado de usarse y ya no forma parte de SQL Server.  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con versiones anteriores de Analysis Services](analysis-services-backward-compatibility.md)  
  
  
