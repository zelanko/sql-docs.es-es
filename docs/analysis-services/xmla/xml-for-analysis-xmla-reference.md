---
title: Referencia XML for Analysis (XMLA) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e8c3645175d8d1f3251fd621825f5a542669cbb
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34576767"
---
# <a name="xml-for-analysis--xmla-reference"></a>Referencia XML for Analysis (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]   

Azure Analysis Services y SQL Server Analysis Services usan XML para el protocolo de Analysis (XMLA) para las comunicaciones entre las aplicaciones cliente y una instancia de Analysis Services. En el nivel más básico, otras bibliotecas cliente, como ADOMD.NET y AMO, construyen las solicitudes y descodifican las respuestas de XMLA, actuando como intermediarias de una instancia de Analysis Services, que utiliza exclusivamente XMLA.  
  
 Para admitir la detección y manipulación de datos en modo tabular y multidimensional, la especificación XMLA define dos métodos generalmente accesibles, [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) y [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md)y un colección de tipos de elementos y los datos XML. Dado que XML permite una arquitectura de cliente y servidor de acoplamiento flexible, ambos métodos administran la información de entrada y de salida en formato XML. 

Analysis Services es compatible con la especificación XMLA 1.1., especificación, sino que se extiende para incluir la definición y manipulación de capacidad de datos, implementada como anotaciones en el **Discover** y **Execute** métodos. La sintaxis XML ampliadas son Tabular Model Scripting Language (TMSL) y Analysis Services Scripting Language (ASSL). 

TMSL se muestra la sintaxis de definición de modelo de comando y el objeto para las bases de datos de modelo tabular en el nivel de compatibilidad 1200 y versiones posterior. TMSL se comunica con Analysis Services a través del protocolo XMLA, donde el `XMLA.Execute` método acepta dos scripts de instrucción basada en JSON en TMSL, así como los scripts basados en XML tradicionales de Analysis Services Scripting Language (ASSL para XMLA). Para obtener más información, consulte [referencia de Tabular Model Scripting Language (TMSL)](../tabular-model-scripting-language-tmsl-reference.md).

ASSL es la sintaxis de definición de modelo de comando y objetos de bases de datos de modelo multidimensional y las bases de datos de modo tabular en el nivel de compatibilidad 1103 o inferior. Esta definición se basa en la especificación XMLA sin infringirla. La interoperabilidad basada en XMLA está garantizada cuando se usa solamente XMLA o XMLA y ASSL juntos. Para obtener más información, consulte [Analysis Services Scripting Language (ASSL para XMLA)](../scripting/analysis-services-scripting-language-assl-for-xmla.md).
  
 Como desarrollador, puede usar XMLA como una interfaz si los requisitos de la solución especifican protocolos estándar, como XML, SOAP y HTTP. Los desarrolladores y administradores también pueden utilizar el XMLA de forma "ad-hoc" para recuperar información desde el servidor o ejecutar comandos. 
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Tipos de datos XML (XMLA)](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)|Describe los tipos de datos de la especificación XMLA.|  
|[Elementos XML - comandos (XMLA)](../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)|Elementos que se pueden utilizar dentro del elemento de comando durante una llamada de método Execute.|  
|[Elementos XML - comandos (XMLA)](../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)|Elementos que se pueden utilizar dentro del elemento de comando durante una llamada de método Execute.|  
|[Elementos XML - encabezados (XMLA)](../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)| Elementos de encabezado implementados por Microsoft Analysis Services.|  
|[Elementos XML - propiedades (XMLA)](../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)| Elementos que representan información sobre las propiedades y valores para los tipos de encabezados, métodos, objetos, comandos y datos XMLA.|  
|[Elementos XML - métodos - detección (XMLA)](../../analysis-services/xmla/xml-elements-methods-discover.md)| Recupera información, como la lista de bases de datos disponibles o los detalles sobre un objeto concreto, de una instancia de Analysis Services.|  
|[Elementos XML - métodos - ejecutan (XMLA)](../../analysis-services/xmla/xml-elements-methods-execute.md)| Envía el XML para los comandos de Analysis (XMLA) a una instancia de Analysis Services.|  
|[XML elementos - objetos - DiscoverResponse (XMLA)](../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)| Contiene la información devuelta por una instancia de Analysis Services en respuesta a una llamada al método de detección.|  
|[XML elementos - objetos - ExecuteResponse (XMLA)](../../analysis-services/xmla/xml-elements-objects-executeresponse.md)| Contiene la información devuelta por una instancia de Analysis Services en respuesta a una llamada de método Execute.|  
|[Elementos XML - objetos (XMLA)](../../analysis-services/xmla/xml-elements-objects.md)| Objetos implementados por Analysis Services.|  
|[Compatibilidad con XML for Analysis (XMLA)](../../analysis-services/xmla/xml-for-analysis-compliance-xmla.md)|Describe el nivel de compatibilidad con la especificación XMLA 1.1.|  
  
## <a name="see-also"></a>Vea también
 [Conjuntos de filas de esquema de XML for Analysis](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
 [Desarrollo con ADOMD.NET](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
 [Desarrollar con Objetos de administración de análisis &#40;AMO&#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
