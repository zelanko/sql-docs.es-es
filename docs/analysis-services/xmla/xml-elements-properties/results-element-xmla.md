---
title: resultados de elemento (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: results Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.results
- urn:schemas-microsoft-com:xml-analysis#results
- http://schemas.microsoft.com/analysisservices/2003/engine#results
helpviewer_keywords: results element
ms.assetid: 3249a17a-7bfa-4753-b605-8f611ba7ae2b
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 06fc0651d4475d612bf2821bcca97c93c17d8633
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="results-element-xmla"></a>Elemento results (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contiene una colección de [raíz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) elementos devueltos por la [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método mediante el [lote](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) comando.  
  
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
  
  
