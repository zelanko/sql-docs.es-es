---
title: Desarrollar con ADOMD.NET | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 49bfcc651b00f9d6afc5d2028e174062b0916515
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="developing-with-adomdnet"></a>Desarrollar con ADOMD.NET
  ADOMD.NET es un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] proveedor de datos de .NET Framework que está diseñado para comunicarse con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. ADOMD.NET utiliza el protocolo XML for Analysis para comunicarse con orígenes de datos analíticos mediante conexiones TCP/IP o HTTP para transmitir y recibir solicitudes y respuestas SOAP compatibles con la especificación de XML for Analysis. Los comandos se pueden enviar en expresiones multidimensionales (MDX), extensiones de minería de datos (DMX), Analysis Services Scripting Language (ASSL) o incluso una sintaxis limitada de SQL y es posible que no devuelvan resultados. Los datos analíticos, los indicadores clave de rendimiento (KPI) y los modelos de minería de datos se pueden consultar y manipular mediante el modelo de objetos ADOMD.NET. Con ADOMD.NET, también puede ver metadatos y trabajar con ellos al recuperar conjuntos de filas de esquema compatibles con OLE DB o utilizar el modelo de objetos ADOMD.NET.  
  
 El proveedor de datos de ADOMD.NET se representa mediante el espacio de nombres **Microsoft.AnalysisServices.AdomdClient** .  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Programación del cliente de ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)|Describe cómo utilizar los objetos de cliente de ADOMD.NET para recuperar datos y metadatos de orígenes de datos analíticos.|  
|[Programación del servidor ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)|Describe cómo utilizar los objetos de servidor de ADOMD.NET para crear procedimientos almacenados y funciones definidas por el usuario.|  
|[Redistribución de ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/redistributing-adomd-net.md)|Describe el proceso de redistribución de ADOMD.NET.|  
|<xref:Microsoft.AnalysisServices.AdomdClient>|Especifica en detalle los objetos contenidos en el espacio de nombres **Microsoft.AnalysisServices.AdomdClient** .|  
  
## <a name="see-also"></a>Vea también  
 [Expresiones multidimensionales & #40; MDX & #41; Referencia](../../../mdx/multidimensional-expressions-mdx-reference.md)   
 [Extensiones de minería de datos & #40; DMX & #41; Referencia](../../../dmx/data-mining-extensions-dmx-reference.md)   
 [Conjuntos de filas de esquema de Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [Desarrollar aplicaciones con Analysis Services Scripting Language &#40;ASSL&#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Acceso a datos de modelos multidimensionales &#40;Analysis Services - datos multidimensionales&#41;](../../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)  
  
  
