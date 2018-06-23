---
title: Métodos (XMLA) | Documentos de Microsoft
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
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#
helpviewer_keywords:
- methods [XML for Analysis]
- XML for Analysis, methods
- XMLA, methods
ms.assetid: c6768dd4-ca06-4a85-93b7-5fd5700886ad
caps.latest.revision: 30
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: fe42e2330e3e108ad1ee0e09d1e1e1007eda9102
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204666"
---
# <a name="methods-xmla"></a>Métodos (XMLA)
  El protocolo XML for Analysis (XMLA) utiliza dos métodos, `Discover` y `Execute`, para proporcionar una manera estándar para las aplicaciones tener acceso a información en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Dado que estos métodos se invocan utilizando el Protocolo simple de acceso a objetos (SOAP), aceptan la entrada y entregan el resultado en XML. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa ambos métodos, conforme a la especificación de XML for Analysis 1.1.  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas siguientes describen los métodos XMLA implementados por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Método|Descripción|  
|------------|-----------------|  
|[Método Discover &#40;XMLA&#41;](xml-elements-methods-discover.md)|Recupera información, por ejemplo la lista de bases de datos disponibles o datos sobre un objeto concreto, desde una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los datos recuperados con el método `Discover` dependen de los valores de los parámetros que se le pasan.|  
|[Ejecutar el método &#40;XMLA&#41;](xml-elements-methods-execute.md)|Envía comandos XMLA a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Están incluidas las solicitudes que conllevan transferencia de datos, como recuperar o actualizar los datos del servidor.|  
  
## <a name="see-also"></a>Vea también  
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [Tipos de datos XML &#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)  
  
  