---
title: Métodos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
- apinav
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#
helpviewer_keywords:
- methods [XML for Analysis]
- XML for Analysis, methods
- XMLA, methods
ms.assetid: c6768dd4-ca06-4a85-93b7-5fd5700886ad
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c1e073eae6637b726a473ea7bf95057ed1548982
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088595"
---
# <a name="methods-xmla"></a>Métodos (XMLA)
  El protocolo XML for Analysis (XMLA) utiliza dos métodos, `Discover` y `Execute`, para proporcionar una manera estándar para las aplicaciones tener acceso a información en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Dado que estos métodos se invocan utilizando el Protocolo simple de acceso a objetos (SOAP), aceptan la entrada y entregan el resultado en XML. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa ambos métodos, conforme a la especificación de XML for Analysis 1.1.  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas siguientes describen los métodos XMLA implementados por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Método|Descripción|  
|------------|-----------------|  
|[Método Discover &#40;XMLA&#41;](xml-elements-methods-discover.md)|Recupera información, por ejemplo la lista de bases de datos disponibles o datos sobre un objeto concreto, desde una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los datos recuperados con el método `Discover` dependen de los valores de los parámetros que se le pasan.|  
|[Método Execute &#40;XMLA&#41;](xml-elements-methods-execute.md)|Envía comandos XMLA a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Están incluidas las solicitudes que conllevan transferencia de datos, como recuperar o actualizar los datos del servidor.|  
  
## <a name="see-also"></a>Vea también  
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [Tipos de datos XML &#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)  
  
  
