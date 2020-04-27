---
title: Arquitectura lógica (Analysis Services de datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services, architecture
- logical architecture [Analysis Services Multidimensional Data]
ms.assetid: 1b9cae0a-8990-4194-af5f-a1ea5f2aff06
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 074659d42e1960c5f24cf4afa20668a3d8c823b0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62725489"
---
# <a name="logical-architecture-analysis-services---multidimensional-data"></a>Arquitectura lógica (Analysis Services - Datos multidimensionales)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa los componentes de servidor y cliente para proporcionar funciones de procesamiento analítico en línea (OLAP) y minería de datos para aplicaciones de Business [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Intelligence:  
  
-   El componente de servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se implementa como servicio de Microsoft Windows. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite varias instancias en el mismo equipo, con cada instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] implementada como una instancia independiente del servicio de Windows.  
  
-   Los clientes se comunican con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] mediante el estándar público XML for Analysis (XMLA), protocolo basado en SOAP para emitir comandos y recibir respuestas, que se expone como servicio web. Además, se proporcionan modelos de objetos de cliente en XMLA, a los que se puede obtener acceso mediante un proveedor administrado, como ADOMD.NET, o un proveedor OLE DB nativo.  
  
-   Pueden emitirse comandos de consulta mediante los siguientes lenguajes: SQL; MDX (Expresiones multidimensionales), un lenguaje de consulta estándar para el análisis; o Extensiones de minería de datos (DMX), un lenguaje de consulta estándar orientado a la minería de datos. También se puede usar el lenguaje de script de Analysis Services (ASSL) para administrar objetos de base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] también admite un motor de cubo local que permite a las aplicaciones en clientes desconectados examinar datos multidimensionales almacenados localmente. Para obtener más información, consulte [requisitos de la arquitectura de cliente para el desarrollo de Analysis Services](../olap-physical/client-architecture-requirements-for-analysis-services-development.md)  
  
## <a name="in-this-section"></a>En esta sección  
 **Información general de arquitectura lógica**  
 [Información general sobre la arquitectura lógica &#40;Analysis Services-datos multidimensionales&#41;](logical-architecture-overview-analysis-services-multidimensional-data.md)  
  
 **Objetos Server**  
 [Objetos de servidor &#40;Analysis Services de datos multidimensionales&#41;](server-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de base de datos**  
 [Objetos de base de datos &#40;Analysis Services - Datos multidimensionales&#41;](database-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos Dimension**  
 [Objetos de dimensión &#40;Analysis Services de datos multidimensionales&#41;](../../multidimensional-models-olap-logical-dimension-objects/dimension-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de cubo**  
 [Objetos de cubo &#40;Analysis Services de datos multidimensionales&#41;](../../multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
 **Seguridad de acceso de usuario**  
 [Arquitectura de seguridad para el acceso de los usuarios](understanding-microsoft-olap-logical-architecture.md)  
  
## <a name="see-also"></a>Consulte también  
 [Descripción de la arquitectura OLAP de Microsoft](../olap-physical/understanding-microsoft-olap-architecture.md)   
 [Arquitectura física &#40;Analysis Services - Datos multidimensionales&#41;](../olap-physical/understanding-microsoft-olap-physical-architecture.md)  
  
  
