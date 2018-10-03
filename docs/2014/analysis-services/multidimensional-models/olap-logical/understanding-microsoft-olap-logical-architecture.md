---
title: Arquitectura lógica (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- Analysis Services, architecture
- logical architecture [Analysis Services Multidimensional Data]
ms.assetid: 1b9cae0a-8990-4194-af5f-a1ea5f2aff06
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3ef5ebb45a1b07470add62eed720547e16cdffab
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091055"
---
# <a name="logical-architecture-analysis-services---multidimensional-data"></a>Arquitectura lógica (Analysis Services - Datos multidimensionales)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usa componentes de servidor y cliente para proporcionar procesamiento analítico en línea (OLAP) y funcionalidad de minería de datos para aplicaciones de inteligencia empresarial:  
  
-   El componente de servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se implementa como servicio de Microsoft Windows. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite varias instancias en el mismo equipo, con cada instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] implementada como instancia independiente del servicio de Windows.  
  
-   Los clientes se comunican con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] mediante el estándar público XML for Analysis (XMLA), protocolo basado en SOAP para emitir comandos y recibir respuestas, que se expone como servicio web. Además, se proporcionan modelos de objetos de cliente en XMLA, a los que se puede obtener acceso mediante un proveedor administrado, como ADOMD.NET, o un proveedor OLE DB nativo.  
  
-   Pueden emitirse comandos de consulta mediante los siguientes lenguajes: SQL; MDX (Expresiones multidimensionales), un lenguaje de consulta estándar para el análisis; o Extensiones de minería de datos (DMX), un lenguaje de consulta estándar orientado a la minería de datos. También se puede usar el lenguaje de script de Analysis Services (ASSL) para administrar objetos de base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] también admite un motor de cubo local que permite a las aplicaciones en clientes desconectados examinar datos multidimensionales almacenados localmente. Para obtener más información, consulte [requisitos de arquitectura de cliente para el desarrollo de Analysis Services](../olap-physical/client-architecture-requirements-for-analysis-services-development.md)  
  
## <a name="in-this-section"></a>En esta sección  
 **Información general de arquitectura lógica**  
 [Introducción a la arquitectura lógica &#40;Analysis Services - datos multidimensionales&#41;](logical-architecture-overview-analysis-services-multidimensional-data.md)  
  
 **Objetos de servidor**  
 [Objetos de servidor &#40;Analysis Services - datos multidimensionales&#41;](server-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de base de datos**  
 [Objetos de base de datos &#40;Analysis Services - datos multidimensionales&#41;](database-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de dimensión**  
 [Objetos de dimensión &#40;Analysis Services - datos multidimensionales&#41;](../../multidimensional-models-olap-logical-dimension-objects/dimension-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de cubo**  
 [Objetos de cubo &#40;Analysis Services - datos multidimensionales&#41;](../../multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
 **Seguridad de acceso del usuario**  
 [Arquitectura de seguridad de acceso de usuario](understanding-microsoft-olap-logical-architecture.md)  
  
## <a name="see-also"></a>Vea también  
 [Descripción de la arquitectura OLAP de Microsoft](../olap-physical/understanding-microsoft-olap-architecture.md)   
 [Arquitectura física &#40;Analysis Services - datos multidimensionales&#41;](../olap-physical/understanding-microsoft-olap-physical-architecture.md)  
  
  
