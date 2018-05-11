---
title: resultados de elemento (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a963b9128f6639ba9cd67bdfbd560d31f396ae41
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="results-element-xmla"></a>Elemento results (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene una colección de elementos [root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) devuelta por el método [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) utilizando el comando [Batch](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) .  
  
 **Namespace** `http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults`  
  
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
 [Propiedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
