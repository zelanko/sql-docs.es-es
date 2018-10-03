---
title: da como resultado del elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- results Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.results
- urn:schemas-microsoft-com:xml-analysis#results
- http://schemas.microsoft.com/analysisservices/2003/engine#results
helpviewer_keywords:
- results element
ms.assetid: 3249a17a-7bfa-4753-b605-8f611ba7ae2b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e99728941db468f361535fa675281f880ad3133a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091365"
---
# <a name="results-element-xmla"></a>Elemento results (XMLA)
  Contiene una colección de elementos [root](root-element-xmla.md) devuelta por el método [Execute](../xml-elements-methods-execute.md) utilizando el comando [Batch](../xml-elements-commands/batch-element-xmla.md) .  
  
 **Namespace** http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<return>  
   <results>  
      <root>...</root>  
   </results>  
</return>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[devolver](return-element-xmla.md)|  
|Elementos secundarios|[Raíz](root-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 Si el método `Batch` ejecuta un comando `Execute`, el elemento `return` contiene un elemento `results` único en lugar de un elemento `root` único. El contenido del elemento `results` depende de los valores usados para ejecutar el comando `Batch`.  
  
 Para los comandos `Batch` no transaccionales, el elemento `results` contiene un elemento `root` para cada comando ejecutado por el comando `Batch`, independientemente de si el comando se completa correctamente o sin éxito. Para los comandos `Batch` transaccionales, el elemento `results` contiene solamente un elemento `root`, que contiene la información de error del comando que no se ha ejecutado correctamente dentro del comando `Batch`.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
