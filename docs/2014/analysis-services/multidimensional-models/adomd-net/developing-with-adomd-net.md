---
title: Desarrollar con ADOMD.NET | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ADOMD.NET
ms.assetid: abaf33aa-db55-43bf-8f30-15547559be1d
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1dfdd10ae488633812b61e2a0220f7c22e65e575
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113912"
---
# <a name="developing-with-adomdnet"></a>Desarrollar con ADOMD.NET
  ADOMD.NET es un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] proveedor de datos de .NET Framework que está diseñado para comunicarse con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. ADOMD.NET utiliza el protocolo XML for Analysis para comunicarse con orígenes de datos analíticos mediante conexiones TCP/IP o HTTP para transmitir y recibir solicitudes y respuestas SOAP compatibles con la especificación de XML for Analysis. Los comandos se pueden enviar en expresiones multidimensionales (MDX), extensiones de minería de datos (DMX), Analysis Services Scripting Language (ASSL) o incluso una sintaxis limitada de SQL y es posible que no devuelvan resultados. Los datos analíticos, los indicadores clave de rendimiento (KPI) y los modelos de minería de datos se pueden consultar y manipular mediante el modelo de objetos ADOMD.NET. Con ADOMD.NET, también puede ver metadatos y trabajar con ellos al recuperar conjuntos de filas de esquema compatibles con OLE DB o utilizar el modelo de objetos ADOMD.NET.  
  
 El proveedor de datos ADOMD.NET se representa mediante el `Microsoft.AnalysisServices.AdomdClient` espacio de nombres.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Programación del cliente de ADOMD.NET](../../multidimensional-models-adomd-net-client/adomd-net-client-programming.md)|Describe cómo utilizar los objetos de cliente de ADOMD.NET para recuperar datos y metadatos de orígenes de datos analíticos.|  
|[Programación del servidor ADOMD.NET](../../multidimensional-models-adomd-net-server/adomd-net-server-programming.md)|Describe cómo utilizar los objetos de servidor de ADOMD.NET para crear procedimientos almacenados y funciones definidas por el usuario.|  
|[Redistribución de ADOMD.NET](redistributing-adomd-net.md)|Describe el proceso de redistribución de ADOMD.NET.|  
|<xref:Microsoft.AnalysisServices.AdomdClient>|Especifica en detalle los objetos contenidos en el espacio de nombres `Microsoft.AnalysisServices.AdomdClient`.|  
  
## <a name="see-also"></a>Vea también  
 [Expresiones multidimensionales &#40;MDX&#41; referencia](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Conjuntos de filas de esquema de Analysis Services](../../schema-rowsets/analysis-services-schema-rowsets.md)   
 [Desarrollar aplicaciones con Analysis Services Scripting Language &#40;ASSL&#41;](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Acceso a datos de modelos multidimensionales &#40;Analysis Services - datos multidimensionales&#41;](../mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)  
  
  
