---
title: Desarrollo de los requisitos de arquitectura de cliente para Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- local mining models [Analysis Services]
- Analysis Services, architecture
- providers [Analysis Services]
- data pumps [Analysis Services]
- client architecture [Analysis Services]
- local cubes [Analysis Services]
ms.assetid: 03a8eb6b-159f-4a0a-afbe-06a2424b6090
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a372b5c0b89088a7054606e76138906f83598e5d
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158881"
---
# <a name="client-architecture-requirements-for-analysis-services-development"></a>Requisitos de la arquitectura de cliente para el desarrollo de Analysis Services
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite una arquitectura de cliente ligero. El [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] motor de cálculo es completamente basada en servidor, por lo que se resuelven todas las consultas en el servidor. En consecuencia, para cada consulta solo se necesita realizar un viaje de ida y vuelta entre el cliente y el servidor, lo que produce un rendimiento escalable a medida que las consultas aumenten en complejidad.   
  
 El protocolo nativo para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] es XML for analysis (XML/A). [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] proporciona varias interfaces de acceso a datos para aplicaciones cliente, pero todos estos componentes se comunican con una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usando XML for analysis.  
  
 Se proporcionan varios proveedores distintos en [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para admitir diferentes lenguajes de programación. Un proveedor se comunica con un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] enviando y recibiendo XML for Analysis en paquetes SOAP sobre TCP/IP o sobre HTTP a través de Internet Information Services (IIS). La conexión HTTP utiliza un objeto COM, denominado bombeo de datos y cuya instancia ha sido creada por IIS, que actúa como conducto para los datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. El bombeo de datos no examina de ningún modo los datos subyacentes contenidos en el flujo HTTP, ni ninguna de las estructuras de datos subyacentes está disponible para el código en la propia biblioteca de datos.  
  
 ![Arquitectura lógica de cliente de Analysis Services](../../../analysis-services/dev-guide/media/as-clientarch9.gif "arquitectura lógica de cliente de Analysis Services")  
  
 Las aplicaciones cliente de Win32 pueden conectarse con un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] mediante interfaces OLE DB para OLAP o mediante el modelo de objetos Microsoft® ActiveX® Data Objects (ADO) para lenguajes de automatización COM (Modelo de objetos componentes) como, por ejemplo, Microsoft Visual Basic®. Las aplicaciones codificadas con lenguajes .NET se pueden conectar con un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] mediante ADOMD.NET.  
  
 Las aplicaciones existentes pueden comunicarse con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] sin necesidad de ser modificadas utilizando simplemente uno de los proveedores de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Lenguaje de programación|Interfaz de acceso a datos|  
|--------------------------|---------------------------|  
|C++|OLE DB para OLAP|  
|Visual Basic 6|ADO MD|  
|Lenguajes .NET|ADO MD.NET|  
|Cualquier lenguaje que admita SOAP|XML for Analysis|  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tiene una arquitectura web con un nivel medio completamente escalable para implementación en organizaciones pequeñas y medianas. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ofrece una amplia compatibilidad de nivel medio para servicios web. Las aplicaciones ASP son compatibles con OLE DB para OLAP y ADO MD, las aplicaciones ASP.NET son compatibles con ADOMD.NET. El nivel medio, que se muestra en la siguiente ilustración, se puede escalar a muchos usuarios simultáneos.  
  
 ![Diagrama lógico de arquitectura de nivel intermedio](../../../analysis-services/dev-guide/media/as-midtierarch9.gif "diagrama lógico de arquitectura de nivel intermedio")  
  
 Las aplicaciones cliente y de nivel medio pueden comunicarse directamente con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] sin necesidad de ningún proveedor. Las aplicaciones cliente y de nivel medio pueden enviar XML for Analysis en paquetes SOAP sobre TCP/IP, HTTP o HTTPS. El cliente puede estar codificado con cualquier lenguaje compatible con SOAP. La comunicación se administra mucho más fácilmente en este caso a través de Internet Information Services (IIS) mediante HTTP, aunque también puede codificarse una conexión directa con el servidor mediante TCP/IP. Se trata de la solución de cliente más ligero para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="analysis-services-in-tabular-or-sharepoint-mode"></a>Analysis Services en el modo de SharePoint o tabular  
 En [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], el servidor puede iniciarse en el modo del motor de análisis en memoria xVelocity (VertiPaq) para bases de datos tabulares y libros de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] publicados en un sitio de SharePoint.  
  
 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] y [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] son los únicos entornos del cliente que se admiten para crear y consultar las bases de datos en memoria que utilizan el modo SharePoint o tabular, respectivamente. La base de datos PowerPivot incrustada que cree mediante el uso de Excel y [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] herramientas se encuentra dentro del libro de Excel y se guarda como parte del archivo .xlsx de Excel.  
  
 Sin embargo, un libro de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] puede utilizar datos almacenados en un cubo tradicional si los datos del cubo se importan en el libro. También se pueden importar datos de otro libro de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] si se ha publicado en un sitio de SharePoint.  
  
> [!NOTE]  
>  Al utilizar un cubo como origen de datos para un libro de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)], los datos que se obtienen del cubo se definen como una consulta MDX; sin embargo, los datos se importan como una instantánea plana. No se puede trabajar interactivamente con los datos ni actualizar los datos del cubo.  
  
### <a name="interfaces-for-powerpivot-client"></a>Interfaces para el cliente de PowerPivot  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] interactúa con el motor analítico en memoria xVelocity (VertiPaq) el motor de almacenamiento dentro del libro utilizando las interfaces y lenguajes establecidos para Analysis Services: AMO y ADOMD.NET, MDX y XMLA. Dentro del complemento, las medidas se definen utilizando un lenguaje de fórmulas parecido Excel, Expresiones de análisis de datos (DAX). Las expresiones DAX se insertan en los mensajes XMLA que se envían al servidor en proceso.  
  
### <a name="providers"></a>Proveedores  
 Las comunicaciones entre [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] y Excel utilizan el proveedor de MSOLAP OLEDB (versión 11.0). Dentro del proveedor MSOLAP hay cuatro módulos diferentes, o transportes, que se pueden utilizar para enviar mensajes entre el cliente y el servidor.  
  
 **TCP/IP** usado para las conexiones cliente-servidor normales.  
  
 **HTTP** utilizado para las conexiones HTTP a través del servicio de bombeo de datos SSAS, o mediante una llamada al componente de servicio de Web de PowerPivot de SharePoint (WS).  
  
 **INPROC** usado para las conexiones al motor en proceso.  
  
 **CANAL** reservado para las comunicaciones con el servicio de sistema de PowerPivot en la granja de SharePoint.  
  
## <a name="see-also"></a>Vea también  
 [Componentes de servidor del motor OLAP](olap-engine-server-components.md)  
  
  
