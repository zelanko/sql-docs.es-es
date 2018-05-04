---
title: Referencia XML for Analysis (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XML for Analysis, reference
- XMLA, reference
ms.assetid: 88045e05-ce47-4e28-999b-7f9c74af9faf
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: af98955728124e656ef78582b52ed495c9ca6fc0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="xml-for-analysis--xmla-reference"></a>Referencia XML for Analysis (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa el protocolo XML for Analysis (XMLA) para administrar todas las comunicaciones entre las aplicaciones cliente y una instancia de Analysis Services. En el nivel más básico, otras bibliotecas cliente, como ADOMD.NET y AMO, construyen las solicitudes y descodifican las respuestas de XMLA, actuando como intermediarias de una instancia de Analysis Services, que utiliza exclusivamente XMLA.  
  
 Para admitir la detección y manipulación de datos en formatos tabulares y multidimensionales, la especificación XMLA define dos métodos generalmente accesibles, [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) y [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md)y un colección de tipos de elementos y los datos XML. Dado que XML permite una arquitectura de cliente y servidor de acoplamiento flexible, ambos métodos administran la información de entrada y de salida en formato XML. Analysis Services es compatible con la especificación XMLA 1.1., especificación, sino que se extiende para incluir la definición y manipulación de capacidad de datos, implementada como anotaciones en el **Discover** y **Execute** métodos. La sintaxis XML ampliada se conoce como Lenguaje de scripting de Analysis Services (ASSL). ASSL se basa en la especificación XMLA sin infringirla. La interoperabilidad basada en XMLA está garantizada cuando se usa solamente XMLA o XMLA y ASSL juntos.  
  
 Como programador, puede usar XMLA como una interfaz de programación si los requisitos de la solución especifican protocolos estándar, como XML, SOAP y HTTP. Los programadores y administradores también pueden usar XMLA ad hoc para recuperar información del servidor o ejecutar comandos.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Elementos XML & #40; XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)|Describe los elementos de la especificación XMLA.|  
|[Tipos de datos XML &#40;XMLA&#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)|Describe los tipos de datos de la especificación XMLA.|  
|[Compatibilidad de análisis con XML for &#40;XMLA&#41;](../../analysis-services/xmla/xml-for-analysis-compliance-xmla.md)|Describe el nivel de compatibilidad con la especificación XMLA 1.1.|  
  
## <a name="related-sections"></a>Secciones relacionadas  
 [Desarrollar con Analysis Services Scripting Language & #40; ASSL & #41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
  
 [XML para conjuntos de filas de esquema de análisis](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
 [Desarrollar con ADOMD.NET](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
 [Desarrollar con objetos de administración de análisis & #40; AMO & #41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
  
## <a name="see-also"></a>Vea también  
 [Descripción de la arquitectura OLAP de Microsoft](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
