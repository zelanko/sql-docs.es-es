---
title: resultados de elemento (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- results Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.results
- urn:schemas-microsoft-com:xml-analysis#results
- http://schemas.microsoft.com/analysisservices/2003/engine#results
helpviewer_keywords:
- results element
ms.assetid: 3249a17a-7bfa-4753-b605-8f611ba7ae2b
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 791512ba71ef92a9e220936b138faf9eff2a4872
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="results-element-xmla"></a>Elemento results (XMLA)
  Contiene una colección de elementos [root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) devuelta por el método [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) utilizando el comando [Batch](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) .  
  
 **Namespace**`http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults`  
  
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
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[valor devuelto](../../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
|Elementos secundarios|[raíz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 Si el método **Batch** ejecuta un comando **Execute** , el elemento **return** contiene un elemento **results** único en lugar de un elemento **root** único. El contenido del elemento **results** depende de los valores usados para ejecutar el comando **Batch** .  
  
 Para los comandos **Batch** no transaccionales, el elemento **results** contiene un elemento **root** para cada comando ejecutado por el comando **Batch** , independientemente de si el comando se completa correctamente o sin éxito. Para los comandos **Batch** transaccionales, el elemento **results** contiene solamente un elemento **root** , que contiene la información de error del comando que no se ha ejecutado correctamente dentro del comando **Batch** .  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

