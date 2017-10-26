---
title: "Métodos (XMLA) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#
helpviewer_keywords:
- methods [XML for Analysis]
- XML for Analysis, methods
- XMLA, methods
ms.assetid: c6768dd4-ca06-4a85-93b7-5fd5700886ad
caps.latest.revision: 30
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d7e9b7f9ee860b8ff65664d15b17ca9ebe182e15
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="xml-elements---methods"></a>Elementos XML: métodos
  El protocolo XML for Analysis (XMLA) utiliza dos métodos, **Discover** y **Execute**, para proporcionar una manera estándar para las aplicaciones tener acceso a información en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Dado que estos métodos se invocan utilizando el Protocolo simple de acceso a objetos (SOAP), aceptan la entrada y entregan el resultado en XML. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa ambos métodos, conforme a la especificación de XML for Analysis 1.1.  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas siguientes describen los métodos XMLA implementados por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Método|Description|  
|------------|-----------------|  
|[Detectar método &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)|Recupera información, por ejemplo la lista de bases de datos disponibles o datos sobre un objeto concreto, desde una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los datos recuperados con el método **Discover** dependen de los valores de los parámetros que se le pasan.|  
|[Ejecutar método &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)|Envía comandos XMLA a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Están incluidas las solicitudes que conllevan transferencia de datos, como recuperar o actualizar los datos del servidor.|  
  
## <a name="see-also"></a>Vea también  
 [Elementos XML &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Tipos de datos XML &#40; XMLA &#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  

