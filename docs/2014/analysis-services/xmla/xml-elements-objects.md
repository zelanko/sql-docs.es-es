---
title: Objetos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- objects [XML for Analysis]
- XML for Analysis, objects
- XMLA, objects
ms.assetid: 768188ef-85d4-432a-9390-be05c835137f
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3fdaa8cc81b642212c6aa404a8b6d39e3872c743
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37205905"
---
# <a name="objects-xmla"></a>Objetos (XMLA)
  El protocolo XML for Analysis (XMLA) utiliza dos métodos, `Discover` y `Execute`, para proporcionar una manera estándar para las aplicaciones tener acceso a información en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Dado que estos métodos se invocan mediante el protocolo del Protocolo Simple de acceso a objetos (SOAP), aceptan la entrada y entregar los resultados en XML.  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas siguientes describen los objetos XMLA implementados por [!INCLUDE[ssAS](../../includes/ssas-md.md)].  
  
|Método|Descripción|  
|------------|-----------------|  
|[Elemento DiscoverResponse &#40;XMLA&#41;](xml-elements-objects-discoverresponse.md)|Contiene la información devuelta por una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en respuesta a un [Discover](xml-elements-methods-discover.md) llamada al método.|  
|[Elemento ExecuteResponse &#40;XMLA&#41;](xml-elements-objects-executeresponse.md)|Contiene la información devuelta por una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en respuesta a una [Execute](xml-elements-methods-execute.md) llamada al método.|  
  
## <a name="see-also"></a>Vea también  
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [Tipos de datos XML &#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)  
  
  
