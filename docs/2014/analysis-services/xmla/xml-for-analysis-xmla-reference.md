---
title: Referencia XML for Analysis (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, reference
- XMLA, reference
ms.assetid: 88045e05-ce47-4e28-999b-7f9c74af9faf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fde04360c7b6af1c9bf6aa906328e5031eb76c32
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164445"
---
# <a name="xml-for-analysis--xmla-reference"></a>Referencia XML for Analysis (XMLA)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa el protocolo XML for Analysis (XMLA) para controlar todas las comunicaciones entre las aplicaciones cliente y una instancia de Analysis Services. En el nivel más básico, otras bibliotecas cliente, como ADOMD.NET y AMO, construyen las solicitudes y descodifican las respuestas de XMLA, actuando como intermediarias de una instancia de Analysis Services, que utiliza exclusivamente XMLA.  
  
 Para admitir la detección y manipulación de datos en formatos tabulares y multidimensionales, la especificación XMLA define dos métodos generalmente accesibles, [Discover](xml-elements-methods-discover.md) y [Execute](xml-elements-methods-execute.md)y un colección de tipos de datos y elementos XML. Dado que XML permite una arquitectura de cliente y servidor de acoplamiento flexible, ambos métodos administran la información de entrada y de salida en formato XML. Analysis Services es compatible con la especificación XMLA 1.1., pero amplía también esta especificación para incluir funciones de definición y manipulación de datos, que se implementan como anotaciones de los métodos `Discover` y `Execute`. La sintaxis XML ampliada se conoce como Lenguaje de scripting de Analysis Services (ASSL). ASSL se basa en la especificación XMLA sin infringirla. La interoperabilidad basada en XMLA está garantizada cuando se usa solamente XMLA o XMLA y ASSL juntos.  
  
 Como programador, puede usar XMLA como una interfaz de programación si los requisitos de la solución especifican protocolos estándar, como XML, SOAP y HTTP. Los programadores y administradores también pueden usar XMLA ad hoc para recuperar información del servidor o ejecutar comandos.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)|Describe los elementos de la especificación XMLA.|  
|[Tipos de datos XML &#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)|Describe los tipos de datos de la especificación XMLA.|  
|[Compatibilidad de análisis con XML for &#40;XMLA&#41;](xml-for-analysis-compliance-xmla.md)|Describe el nivel de compatibilidad con la especificación XMLA 1.1.|  
  
## <a name="related-sections"></a>Secciones relacionadas  
 [Desarrollar aplicaciones con Analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
  
 [Conjuntos de filas de esquema de XML for Analysis](../schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
 [Desarrollo con ADOMD.NET](../multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
 [Desarrollar con objetos de administración de análisis &#40;AMO&#41;](../multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
  
## <a name="see-also"></a>Vea también  
 [Descripción de la arquitectura OLAP de Microsoft](../multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
