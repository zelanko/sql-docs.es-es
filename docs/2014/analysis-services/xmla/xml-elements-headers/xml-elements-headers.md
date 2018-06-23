---
title: Encabezados (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- XMLA, headers
- SOAP headers [XML for Analysis]
- XML for Analysis, headers
- headers [XML for Analysis]
ms.assetid: 36407b5c-d98d-47e4-8d36-d8896e15a748
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: bb2cff2e70ccd1ac0cf391f7832db4978a415f56
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199532"
---
# <a name="headers-xmla"></a>Encabezados [XMLA]
  El protocolo XML for Analysis (XMLA) utiliza los elementos XML dentro del encabezado SOAP para administrar las características del nivel de protocolo, como la compatibilidad de la sesión y la negociación de características compatibles.  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas siguientes describen los elementos de encabezado XMLA implementados por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Método|Descripción|  
|------------|-----------------|  
|[Elemento BeginSession &#40;XMLA&#41;](session-element-xmla.md)|Utiliza un encabezado SOAP en un mensaje de solicitud SOAP para iniciar una nueva sesión en una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento EndSession &#40;XMLA&#41;](endsession-element-xmla.md)|Utiliza el encabezado SOAP en un mensaje de solicitud SOAP para terminar una sesión existente en una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento de la sesión &#40;XMLA&#41;](session-element-xmla.md)|Utiliza el encabezado SOAP en un mensaje de solicitud SOAP para identificar una sesión explícita existente en una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento ProtocolCapabilities &#40;XMLA&#41;](protocolcapabilities-element-xmla.md)|Utiliza el encabezado SOAP en un mensaje de solicitud SOAP para identificar prestaciones de protocolo entre una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y una aplicación cliente.|  
  
## <a name="see-also"></a>Vea también  
 [Elementos XML &#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)   
 [Tipos de datos XML &#40;XMLA&#41;](../xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)  
  
  