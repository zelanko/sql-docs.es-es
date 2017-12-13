---
title: Desarrollar con ADOMD.NET | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: ADOMD.NET
ms.assetid: abaf33aa-db55-43bf-8f30-15547559be1d
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8040113b399c1866b7324961f11c90ff44b7962f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="developing-with-adomdnet"></a>Desarrollar con ADOMD.NET
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]ADOMD.NET es un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] proveedor de datos de .NET Framework que está diseñado para comunicarse con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. ADOMD.NET utiliza el protocolo XML for Analysis para comunicarse con orígenes de datos analíticos mediante conexiones TCP/IP o HTTP para transmitir y recibir solicitudes y respuestas SOAP compatibles con la especificación de XML for Analysis. Los comandos se pueden enviar en expresiones multidimensionales (MDX), extensiones de minería de datos (DMX), Analysis Services Scripting Language (ASSL) o incluso una sintaxis limitada de SQL y es posible que no devuelvan resultados. Los datos analíticos, los indicadores clave de rendimiento (KPI) y los modelos de minería de datos se pueden consultar y manipular mediante el modelo de objetos ADOMD.NET. Con ADOMD.NET, también puede ver metadatos y trabajar con ellos al recuperar conjuntos de filas de esquema compatibles con OLE DB o utilizar el modelo de objetos ADOMD.NET.  
  
 El proveedor de datos de ADOMD.NET se representa mediante el espacio de nombres **Microsoft.AnalysisServices.AdomdClient** .  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Programación del cliente de ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)|Describe cómo utilizar los objetos de cliente de ADOMD.NET para recuperar datos y metadatos de orígenes de datos analíticos.|  
|[Programación del servidor ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)|Describe cómo utilizar los objetos de servidor de ADOMD.NET para crear procedimientos almacenados y funciones definidas por el usuario.|  
|[Redistribución de ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/redistributing-adomd-net.md)|Describe el proceso de redistribución de ADOMD.NET.|  
|<xref:Microsoft.AnalysisServices.AdomdClient>|Especifica en detalle los objetos contenidos en el espacio de nombres **Microsoft.AnalysisServices.AdomdClient** .|  
  
## <a name="see-also"></a>Vea también  
 [Expresiones multidimensionales &#40; MDX &#41; Referencia](../../../mdx/multidimensional-expressions-mdx-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia](../../../dmx/data-mining-extensions-dmx-reference.md)   
 [Conjuntos de filas de esquema de Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [Desarrollar con Analysis Services Scripting Language &#40; ASSL &#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Acceso a datos de modelo multidimensional &#40; Analysis Services - datos multidimensionales &#41;](../../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)  
  
  
