---
title: Encabezados [XMLA] | Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b04b85e3267e7432f37c5f70e823c859a82a952
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37291301"
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
  
  
