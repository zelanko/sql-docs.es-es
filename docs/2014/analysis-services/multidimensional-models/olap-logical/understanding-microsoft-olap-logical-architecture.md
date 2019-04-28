---
title: Arquitectura lógica (Analysis Services - datos multidimensionales) | Microsoft Docs
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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725489"
---
# <a name="logical-architecture-analysis-services---multidimensional-data"></a>Arquitectura lógica (Analysis Services - Datos multidimensionales)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usa componentes de servidor y cliente para proporcionar procesamiento analítico en línea (OLAP) y funcionalidad de minería de datos para aplicaciones de inteligencia empresarial:  
  
-   El componente de servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se implementa como servicio de Microsoft Windows. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite varias instancias en el mismo equipo, con cada instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] implementada como instancia independiente del servicio de Windows.  
  
-   Los clientes se comunican con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] mediante el estándar público XML for Analysis (XMLA), protocolo basado en SOAP para emitir comandos y recibir respuestas, que se expone como servicio web. Además, se proporcionan modelos de objetos de cliente en XMLA, a los que se puede obtener acceso mediante un proveedor administrado, como ADOMD.NET, o un proveedor OLE DB nativo.  
  
-   Los comandos de consulta se pueden emitir mediante los siguientes idiomas: SQL; Expresiones multidimensionales (MDX), un lenguaje de consulta estándar del sector para el análisis; o las extensiones de minería de datos (DMX), un lenguaje de consulta estándar del sector orientado hacia la minería de datos. También se puede usar el lenguaje de script de Analysis Services (ASSL) para administrar objetos de base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] también admite un motor de cubo local que permite a las aplicaciones en clientes desconectados examinar datos multidimensionales almacenados localmente. Para obtener más información, consulte [requisitos de arquitectura de cliente para el desarrollo de Analysis Services](../olap-physical/client-architecture-requirements-for-analysis-services-development.md)  
  
## <a name="in-this-section"></a>En esta sección  
 **Información general de arquitectura lógica**  
 [Introducción a la arquitectura lógica &#40;Analysis Services - datos multidimensionales&#41;](logical-architecture-overview-analysis-services-multidimensional-data.md)  
  
 **Objetos de servidor**  
 [Objetos de servidor &#40;Analysis Services - datos multidimensionales&#41;](server-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de base de datos**  
 [Objetos de base de datos &#40;Analysis Services - Datos multidimensionales&#41;](database-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de dimensión**  
 [Objetos de dimensión &#40;Analysis Services - datos multidimensionales&#41;](../../multidimensional-models-olap-logical-dimension-objects/dimension-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de cubo**  
 [Objetos de cubo &#40;Analysis Services - datos multidimensionales&#41;](../../multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
 **Seguridad de acceso del usuario**  
 [Arquitectura de seguridad de acceso de usuario](understanding-microsoft-olap-logical-architecture.md)  
  
## <a name="see-also"></a>Vea también  
 [Descripción de la arquitectura OLAP de Microsoft](../olap-physical/understanding-microsoft-olap-architecture.md)   
 [Arquitectura física &#40;Analysis Services - datos multidimensionales&#41;](../olap-physical/understanding-microsoft-olap-physical-architecture.md)  
  
  
