---
title: Arquitectura física (Analysis Services minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- server architecture [Analysis Services]
- architecture [Analysis Services]
ms.assetid: 25eeecf0-6e85-4527-b94d-5503d27edaed
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81c9ee3db0a05107913d3b75fba20ebe8607f941
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66083198"
---
# <a name="physical-architecture-analysis-services---data-mining"></a>Arquitectura física (Analysis Services - Minería de datos)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa los componentes de servidor y cliente para proporcionar la funcionalidad de minería de datos para aplicaciones de Business Intelligence:  
  
-   El componente de servidor se implementa como servicio de Microsoft Windows. Puede tener varias instancias en el mismo equipo, con cada instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementada como instancia independiente del servicio de Windows.  
  
-   Los clientes se comunican con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante el estándar público XML for Analysis (XMLA), protocolo basado en SOAP para emitir comandos y recibir respuestas, que se expone como servicio web. Además, se proporcionan modelos de objetos de cliente en XMLA, a los que se puede obtener acceso mediante un proveedor administrado, como ADOMD.NET, o un proveedor OLE DB nativo.  
  
-   Los comandos de consulta se pueden emitir mediante Extensiones de minería de datos (DMX), un lenguaje de consulta estándar del sector orientado hacia la minería de datos. También se puede usar el lenguaje de script de Analysis Services (ASSL) para administrar objetos de base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="architectural-diagram"></a>Diagrama de la arquitectura  
 Las instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se ejecutan como un servicio independiente y la comunicación con el servicio se produce a través de XML for Analysis (XMLA), mediante HTTP o TCP.  
  
 AMO es un nivel entre la aplicación de usuario y la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que proporciona acceso a los objetos administrativos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . AMO es una biblioteca de clases que toma los comandos de una aplicación cliente y los convierte en mensajes XMLA para la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . AMO muestra los objetos de instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a la aplicación de usuario final como clases, con miembros de método que ejecutan comandos y miembros de propiedad que contienen los datos de los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 La siguiente ilustración muestra la arquitectura de componentes de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , incluidos todos los servicios dentro de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y todos los componentes de usuario que interactúan con ella.  
  
 La ilustración muestra que la única manera de tener acceso a la instancia es utilizando el agente de escucha de XML for Analysis (XMLA), ya sea mediante HTTP o TCP.  
  
> [!WARNING]  
>  DSO está en desuso. No debe utilizar DSO para desarrollar soluciones.  
  
 ![Diagrama de la arquitectura del sistema Analysis Services](../dev-guide/media/analysisservicessystemarchitecture.gif "Diagrama de la arquitectura del sistema Analysis Services")  
  
## <a name="server-configuration"></a>Configuración del servidor  
 Una instancia del servidor puede admitir varias bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , cada una con su propia instancia del servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que responde a las solicitudes de cliente y procesa los objetos.  
  
 Las instancias independientes deben estar instaladas si desea trabajar tanto con modelos de minería de datos tabulares (TDS) como con modelos multidimensionales. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite la instalación en paralelo de las instancias que se ejecutan en el modo tabular, que usa el motor de almacenamiento analítico en memoria xVelocity (VertiPaq), y de las instancias que se ejecutan en una de las configuraciones convencionales OLAP, MOLAP o ROLAP. Para obtener más información, vea [Determinar el modo de servidor de una instancia de Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 Todas las comunicaciones entre un cliente y el servidor de Analysis Services usan XMLA, que es un protocolo independiente de la plataforma y del lenguaje. Cuando se recibe una solicitud de un cliente, Analysis Services determina si está relacionada con OLAP o con la minería de datos, y la enruta apropiadamente. Para obtener más información, vea [Componentes de servidor del motor OLAP](../multidimensional-models/olap-physical/olap-engine-server-components.md).  
  
## <a name="see-also"></a>Consulte también  
 [Arquitectura lógica &#40;Analysis Services:&#41;de minería de datos](logical-architecture-analysis-services-data-mining.md)  
  
  
